<template>
 <p class=" text-4xl pt-20 px-14 text-green-800 font-bold "> <nuxt-link to="/content" class=" text-4xl pt-16 font-serif  text-green-800 font-bold hover:opacity-80">Home</nuxt-link><span class=" text-4xl pt-16 text-green-800 font-bold"> / </span><span class=" hover:opacity-80 text-4xl pt-16 text-green-800 font-bold">Category</span> </p>
<div class=" pt-6 px-14  grid grid-cols-3 rounded-xl border-2 border-black">
  <div v-for="food in category">
   <div class=" shadow-xl p-6 container w-42 border border-black rounded-2xl mt-8">
     <nuxt-link :to="`/content/${food?.idMeal}`">
      <div class=" overflow-hidden rounded-2xl">
          <img :src="food.strMealThumb" alt="" class=" object cover w-56">
        </div>
      </nuxt-link>
      <nuxt-link :to="`/content/${food?.idMeal}`">
        <div class="  p-4 rounded-2xl">
          <div class="">
            <p class="text-emerald-800 font-bold bg-opacity-80 w-89 py-2 text-2xl w-64 truncate hover:opacity-85"><nuxt-link :to="`/content/${food?.idMeal}`">{{food.strMeal}} </nuxt-link></p>
            <div class=" flex align-center flex-row py-2"> <p class=" text-emerald-700 font-bold bg-opacity-80 hover:opacity-85"><nuxt-link :to="`/content/${food?.idMeal}`">Click for More!</nuxt-link></p></div>
            <!-- <button class="bg-pink-800 bg-opacity-50 p-3 rounded-xl text-2xl hover:bg-pink-700 active:bg-pink-600" @click="favourite(food.idMeal)">❤</button> -->
          </div>
        </div>
        </nuxt-link>
      </div>
 </div>
</div>

<!-- <div class="  p-14"><p>id {{ id }}</p></div> -->
</template>
<script setup>
const {id} = useRoute().params
const category = ref('')
const {data} = await useFetch(`https://www.themealdb.com/api/json/v1/1/filter.php?c=${id}`)
category.value = await data.value.meals
console.log(category.value);

const saved = useCookie('saved', {default:()=>''})
 const favourite = (id)=>{
   saved.value = id
}
</script>

<style>
.container{
  display: grid;
  grid-template-columns: 155px 1fr;
  row-gap: 25px;
  width: 550px;
}

</style>