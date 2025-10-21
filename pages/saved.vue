<template>
<div class=" p-14 grid grid-cols-3 rounded-xl">
  <div v-for="recipe in savedRecipies" :key="recipe.idRecipe">
   <div class=" shadow-xl p-8 container w-42 h-38 " v-if="food">
      <div class=" overflow-hidden rounded-2xl">
        <img :src="recipe.image" alt="" class=" object cover w-56">
      </div>
      <div class=" shadow-lg p-4 rounded-2xl">
        <div class="">
          <p class="text-emerald-800 font-bold bg-opacity-80 w-89 py-1 text-xl w-64 truncate">{{recipe.name}}</p>
          <p class="text-emerald-800 font-bold bg-opacity-80 w-89 pb-1 text-xl w-64 truncate">{{recipe.category}}</p>
        <button class="bg-red-800 bg-opacity-80 p-3 rounded-xl text-2xl hover:opacity-90 active:opacity-80" @click="deleteRecipie(recipe.idRecipe)">
          <img width="30" height="30" src="https://img.icons8.com/fluency-systems-filled/48/1A1A1A/trash.png" alt="trash"/>
        </button>
      </div>
    </div>
   </div>
 </div>
</div>
</template>
<script setup>
 
const url = 'https://www.themealdb.com/api/json/v1/1'
const selectedRecipe = ref('');
let food = ref(false)
const savedRecipies = useCookie('savedRecipies', {default: ()=> []})
const saved = useCookie('saved', {default:()=>''})
console.log(saved.value)

if(saved.value){console.log('no item')
food.value = true
const { data  } = await useFetch(`${url}/lookup.php?i=${saved.value}`)
selectedRecipe.value = await data.value.meals[0];
const check = savedRecipies.value.some((recipie)=>recipie.idRecipe === selectedRecipe.value?.idMeal)
if(!check ){
savedRecipies.value.push({name: selectedRecipe.value.strMeal, image:selectedRecipe.value.strMealThumb , category:selectedRecipe.value.strCategory, idRecipe:selectedRecipe.value.idMeal})
console.log(selectedRecipe.value,savedRecipies.value)
}
}else{food.value = false}
const deleteRecipie = (id)=>{
savedRecipies.value = savedRecipies.value.filter((recipe)=>{
return recipe.idRecipe !== id
})
}
</script>


<style>
.container{
  display: grid;
  grid-template-columns: 155px 1fr;
  row-gap: 25px;
  column-gap: 15px;
  width: 550px;
}

</style>