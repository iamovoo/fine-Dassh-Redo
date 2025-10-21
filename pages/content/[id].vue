<template>
<div class=" p-16">
  <!-- <p class=" text-3xl"> id:{{ id }}</p> -->
   <p class=" text-emerald-900 text-3xl font-bold p-2"><nuxt-link to="/content" class=" hover:opacity-75 hover:underline">Home</nuxt-link> / Instructions</p>
 <div class=" p-4 border mb-8 shadow-2xl text-emerald-800 text-lg font-semibold"> <p>{{ recipe.strInstructions }}</p></div>
  <div class=" grid grid-cols-2 m-10">
    <div class="">
        <div class=" overflow-hidden idcard rounded-2xl relative hover:scale-105 transition-all duration-300">
          <img :src="recipe.strMealThumb" alt="" class=" object-contain">
          <div class=" absolute bg-black opacity-50 top-0 bottom-0 left-0 right-0"></div>
          <p class=" text-white text-3xl font-bold absolute bottom-20 left-6">{{recipe.strMeal}}</p>
        <div class=" absolute bottom-10 left-4 ">
          <button class="text-white bg-gray-300 bg-opacity-60 w-28 h-8 rounded-2xl font-bold hover:scale-105 active:scale-110">{{ recipe?.strCategory}}</button>
        </div>
        <!-- <div  class=" absolute bottom-10 left-36" >
          <button class="text-white bg-gray-300 bg-opacity-60 w-24 rounded-2xl font-bold hover:scale-105 active:scale-110">{{ recipe?.strArea}}</button>
        </div> -->
        <div  class=" absolute bottom-10 left-36" >
          <button class="text-white bg-gray-300 bg-opacity-60 w-24 h-8 rounded-2xl font-bold hover:scale-105 active:scale-110" @click="favourite(recipe.idMeal)">❤</button>
        </div>
      </div>
      <div class="shadow-xl mt-5 w-80 rounded-md flex gap-3 p-4"> 
        <div class="w-10 overflow-hidden ">
         <a href="" target="_blank"><img src="" alt="" class="w-32 opacity-70 object-contain"></img></a>
       </div>
      <h2 class=" font-bold text-md text-red-500 hover:underline hover:text-blue-500 active:opacity-70 pt-3 "><a href=" " target="_blank">click for a YouTube Tutorial</a></h2>
    </div>
    </div>
      <div class="grid grid-cols-4 ">
        <div class=" p-2" v-for="ingredient in ingredients" :key="ingredient">
          <div class="flex gap-2 w-64 p-2">
             <img :src="`https://www.themealdb.com/images/ingredients/${ingredient}.png`" alt="" class=" w-10">
             <p class=" text-emerald-800 cursor-pointer w-20 font-bold">{{ingredient}}</p>
          </div>
        </div>
      </div>
  </div>
</div>
</template>
<script setup>

const url = 'https://www.themealdb.com/api/json/v1/1'
const {id} = useRoute().params
const recipe = ref('');
const ingredients = ref([])


const { data  } = await useFetch(`${url}/lookup.php?i=${id}`)
recipe.value = data.value.meals[0];
for (let i = 1 ; i <= 20 ; i++){
  console.log(recipe.value[`strIngredient${i}`]);
  // const ingredient = [recipe.value[`strIngredient${i}`]]
  if(recipe.value[`strIngredient${i}`]){
    ingredients.value.push(recipe.value[`strIngredient${i}`])
  //  console.log(ingredients.value);
  }
}
console.log(data , data.value.meals[0]);
const saved = useCookie('saved', {default:()=>''})
  const favourite = (id)=>{
   saved.value = id
}
</script>


<style>
  .idcard{
    width: 600px;
    height: 380px;
  }

</style>