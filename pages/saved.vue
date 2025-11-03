<template>
  <p class="px-10 pt-10 text-xl font-bold text-emerald-800"><nuxt-link to="/content" class=" hover:opacity-80 hover:underline">Home</nuxt-link> <span> / </span> Saved</p>
<div class=" px-10 mt-4 grid grid-cols-3 rounded-xl">
  <div v-for="recipe in saved" :key="recipe.idMeal">
   <div class="  p-4 w-96 border-2 border-green-900  flex gap-7 rounded-xl hover:shadow-lg mb-5">
    <nuxt-link :to="`/content/${recipe?.idMeal}`">
      <div class=" overflow-hidden rounded-2xl w-16">
        <img :src="recipe.strMealThumb" alt="" class=" object-cover w-56 opacity-95 hover:opacity-100">
      </div>
    </nuxt-link>
    <div class=" flex gap-4 ">
      <div class="">
        <p class="text-emerald-800 font-bold bg-opacity-80 w-89 py-1 text-sm w-44 truncate">{{recipe.strMeal}}-({{recipe.strCategory}})</p>
        <p class="text-emerald-800 bg-opacity-80 pb-1 text-xs truncate">{{recipe.strArea}}</p>
      </div>
      <div>
        <button class="bg-red-800 bg-opacity-80 p-2 rounded-xl hover:opacity-90 active:opacity-80" @click.prevent="deleteRecipie(recipe.idMeal)">
            <img width="20" height="10" src="https://img.icons8.com/fluency-systems-filled/48/1A1A1A/trash.png" alt="trash"/>
          </button>
      </div>
    </div>
   </div>
   
 </div>
</div>
</template>
<script setup>
const saved = ref('')
onMounted(() => {
 saved.value = JSON.parse(localStorage.getItem("saved"))
 console.log(saved.value);
})


const deleteRecipie = (id)=>{
 console.log(id);
 saved.value = saved.value.filter((item)=> item.idMeal !== id )
 localStorage.setItem("saved", JSON.stringify(saved.value))
 console.log(saved.value)
 }
</script>


<style>

</style>