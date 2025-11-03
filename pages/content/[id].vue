<template>
<div class=" p-8">
  <!-- <p class=" text-3xl"> id:{{ id }}</p> -->
   <p class=" text-emerald-900 text-xl font-bold p-2"><nuxt-link to="/content" class=" hover:opacity-75 hover:underline">Home</nuxt-link> / Instructions - {{recipe.strMeal}} </p>
 <div class=" p-4 border mb-8 shadow-2xl text-emerald-800 text-sm font-semibold"> <p>{{ recipe.strInstructions }}</p></div>
  <div class=" grid grid-cols-2 m-10">
    <div class="">
        <div class=" overflow-hidden idcard rounded-2xl relative hover:scale-105 transition-all duration-300">
          <img :src="recipe.strMealThumb" alt="" class=" object-contain">
          <div class=" absolute bg-black opacity-50 top-0 bottom-0 left-0 right-0"></div>
          <p class=" text-white text-lg font-bold absolute bottom-16 mb-2 left-4">{{recipe.strMeal}}</p>
        <div class=" absolute bottom-10 left-4 flex gap-2">
           <div >
          <button class="text-white bg-gray-300 bg-opacity-60 px-2 rounded-2xl font-bold hover:scale-105 active:scale-110 text-sm">{{ recipe?.strCategory}}</button>
        </div>
        <div>
          <button class="text-white bg-gray-300 bg-opacity-60 px-2  rounded-2xl font-bold hover:scale-105 active:scale-110" @click="favourite(recipe)">❤</button>
        </div>
        </div>
      </div>
      <div class="shadow-md mt-3 w-64 rounded-xl flex gap-3 p-2"> 
      <h2 class=" font-bold text-md text-red-500 hover:underline hover:text-blue-500 active:opacity-70 pt-2 "><a :href="recipe.strYoutube" target="_blank">click for a YouTube Tutorial</a></h2>
    </div>
    </div>
      <div class="grid grid-cols-3">
        <div class="" v-for="ingredient in ingredients" :key="ingredient">
          <div class="flex gap-2 p-2">
             <img :src="`https://www.themealdb.com/images/ingredients/${ingredient}.png`" alt="" class=" w-10">
             <p class=" text-emerald-800 cursor-pointer w-28 font-bold text-sm">{{ingredient}}</p>
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

const saved = useState('saved',()=>[])
const favourite = (meal)=>{
  saved.value.push(meal)
  console.log(saved.value)
 const fav = [...JSON.parse(localStorage.getItem('saved')),meal]
  localStorage.setItem('saved',JSON.stringify(fav))
}
</script>


<style>
  .idcard{
    width: 500px;
    height: 280px;
  }

</style>