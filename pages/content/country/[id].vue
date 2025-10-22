<template>
 <p class=" text-sm pt-8 px-10 text-green-800 font-bold "> <nuxt-link to="/content" class=" text-xl pt-16 font-serif  text-green-800 font-bold hover:opacity-80">Home</nuxt-link><span class=" text-xl pt-16 text-green-800 font-bold"> / </span><span class=" hover:opacity-80 text-xl pt-16 text-green-800 font-bold"> {{ id }} Country</span> </p>
<div class=" pt-4 px-10  grid grid-cols-4 rounded-xl">
  <div v-for="food in country">
   <div class=" shadow-xl p-6 h-36 w-72 border flex border-black rounded-2xl mt-6 hover:shadow-2xl ">
     <nuxt-link :to="`/content/${food?.idMeal}`">
      <div class=" overflow-hidden rounded-2xl">
          <img :src="food.strMealThumb" alt="" class=" object-cover w-56">
        </div>
      </nuxt-link>
      <nuxt-link :to="`/content/${food?.idMeal}`">
        <div class="  p-3 rounded-2xl">
          <div class="">
            <p class="text-emerald-800 font-bold bg-opacity-80 w-89 py-1 text-sm w-28 truncate hover:opacity-85"><nuxt-link :to="`/content/${food?.idMeal}`">{{food.strMeal}} </nuxt-link></p>
            <div class=" flex align-center flex-row py-1"> <p class=" text-emerald-700 text-xs font-bold bg-opacity-80 hover:opacity-85"><nuxt-link :to="`/content/${food?.idMeal}`">Click for More!</nuxt-link></p></div>
            <!-- <button class="bg-pink-800 bg-opacity-50 p-3 rounded-xl text-2xl hover:bg-pink-700 active:bg-pink-600" @click="favourite(food.idMeal)">❤</button> -->
          </div>
        </div>
      </nuxt-link>
   </div>
 </div>
</div>

</template>
<script setup>
const {id} = useRoute().params
const country = ref('')
const {data} = await useFetch(`https://www.themealdb.com/api/json/v1/1/filter.php?a=${id}`)
country.value = await data.value.meals
console.log(country.value);
</script>

<style>


</style>