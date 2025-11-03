<template>
<div class="grid grid-cols-2 p-8">
  <div class="flex flex-col z-100
">
    <div class="">
      <div>
        <p class=" font-bold cursor-pointer text-emerald-900 text-2xl pt-3">Feeling adventurous?</p>
        <p class=" cursor-pointer text-emerald-600 pt-1 text-sm">Find a random meal to make.</p>
      </div>
      <div @click="refresh" class="py-4">
        <button @click="refresh" class=" text-center w-36 border p-2 rounded-lg bg-green-800 font-bold hover:bg-green-900 hover:scale-105  justify-center border-lime-400 text-lime-400 active:bg-green-700" >
        Randomize
       </button>
      </div>
    </div>

    <div class=" card mt-3 relative group overflow-hidden mb-6 transition-all duration-700 hover:scale-105">
      <nuxt-link :to="`/content/${randomFood?.idMeal}`">
        <img :src="randomFood?.strMealThumb" alt="" class="object-cover w-full h-full absolute top-0 left-0 ">
        <div class="absolute left-0 right-0 top-0 bottom-0 bg-black bg-opacity-50"></div>
        <h2 class="text-lg text-white absolute bottom-16 font-bold ml-5 pb-3 cursor-pointer group-hover:scale-110 w-44 transition-all duration-700">{{ randomFood?.strMeal }}</h2>
      </nuxt-link>
     <div class=" absolute bottom-10 left-4 flex gap-3">
       <nuxt-link :to="`/content/category/${randomFood?.strCategory}`">
        <div  class=" ">
          <button class="text-white bg-gray-300 bg-opacity-60 px-2 text-xs rounded-2xl font-bold hover:scale-105 active:scale-110">{{ randomFood?.strCategory}}</button>
        </div>
        </nuxt-link>
        <nuxt-link :to="`/content/country/${randomFood?.strArea}`">
        <div  >
          <button class="text-white bg-gray-300 bg-opacity-60 px-2 text-xs rounded-2xl font-bold hover:scale-105 active:scale-110">{{ randomFood?.strArea}}</button>
        </div>
        </nuxt-link>
        <div   >
          <button class="text-white bg-gray-300 bg-opacity-60 px-2  text-xs rounded-2xl font-bold hover:scale-105 active:scale-110" @click="favourite(randomFood)">❤</button>
        </div>
     </div>
    </div>
    <div class="p-3 flex flex-row gap-3 ">
      <nuxt-link :to="`/content/${mealOfTheDay?.idMeal}`">
        <div class="rounded-3xl  h-36 px-5 w-64 pt-3 shadow-2xl ">
          <p class=" p-1 font-bold text-sm font-sans cursor-pointer text-emerald-900">Meal of the day</p>
          <div class=" h-20 w-54 border-2  overflow-hidden rounded-3xl  mx-2 my-2 relative hover:scale-110 transition-all duration-300 " >
            <img :src="mealOfTheDay.strMealThumb" alt="" class=" object-contain opacity-70 hover:opacity-100">
            <div class=" absolute bg-black bg-opacity-50 left-0 right-0 top-0 bottom-0"></div>
            <p class=" absolute top-8 left-10 font-bold text-white cursor-pointer text-sm">{{ mealOfTheDay.strMeal }}</p>
          </div>
        </div>
      </nuxt-link>
      <nuxt-link :to="`/content/${category?.idMeal}`">
        <div class="bg-green-800 rounded-3xl  h-36 px-3 w-64 pt-3">
          <p class=" p-1 font-bold text-sm font-sans cursor-pointer text-lime-400 ">Category of the day</p>
          <div class=" h-20 w-54  overflow-hidden rounded-3xl mx-2 my-2 relative hover:scale-110 transition-all duration-300" >
            <img :src="category.strMealThumb" alt="" class=" object-contain opacity-80 hover:opacity-100">
            <div class=" absolute bg-black bg-opacity-50 left-0 right-0 top-0 bottom-0"></div>
            <p class=" absolute top-8 left-10 font-bold text-white cursor-pointer text-sm">{{ category.strMeal }}</p>
          </div>
        </div>
      </nuxt-link>
    </div>
  </div>
   <div class=" shadow-2xl p-8">
    <div class=" flex gap-3 p-2">
     <button :class="isActive('Category')"  class="w-28 text-sm p-3 rounded-xl text-lime-400 bg-green-700 font-bold" @click="isBtnClicked('Category')"> Category</button>
     <button :class="isActive('Country')"  class="w-28 p-3 rounded-xl text-sm text-lime-400 bg-green-700 font-bold" @click="isBtnClicked('Country')">Country</button>
     <button :class="isActive('ingredient')" class="w-28 p-3 rounded-xl text-sm text-lime-400 bg-green-700 font-bold" @click="isBtnClicked('ingredient')">Ingredients</button>
    </div>

      <div v-if=" activeTab === 'Category'">
        <div>
          <p class=" text-emerald-900 font-bold text-sm p-2">{{total}} results</p>
        </div>
        <div class=" overflow-y-scroll scroll p-4 border-t border-black shadow-xl">
          <div class=" border-b p-3 mb-2 rounded-xl bg-green-800 hover:bg-green-800 hover:bg-opacity-55 active:bg-green-700 active:bg-opacity-55 hover:border-0" v-for="category in listOfCategory" :key="category.strCategory">
          <nuxt-link :to="`/content/category/${category.strCategory}`">
            <p class=" font-bold text-lime-400 cursor-pointer text-sm ">{{category.strCategory}}</p>
          </nuxt-link>
          </div>
        </div>
      </div>

        <div v-if=" activeTab === 'Country'">
        <div>
          <p class=" text-emerald-900 font-bold text-sm p-2">{{total}} results</p>
        </div>
        <div class=" overflow-y-scroll scroll p-4 border-t border-black shadow-xl">
          <div class=" border-b p-3 mb-2 rounded-xl bg-green-800 hover:bg-green-800 hover:bg-opacity-55 active:bg-green-700 active:bg-opacity-55 hover:border-0" v-for="country in countries" :key="country.strArea">
          <nuxt-link :to="`/content/country/${country.strArea}`">
            <p class=" font-bold text-lime-400 cursor-pointer text-sm">{{country.strArea}}</p>
          </nuxt-link>
          </div>
        </div>
      </div>

        <div v-if=" activeTab === 'ingredient'">
        <div>
          <p class=" text-emerald-900 font-bold text-sm p-2"> {{total}} results</p>
        </div>
        <div class=" overflow-y-scroll scroll p-4 border-t border-black shadow-xl">
          <div class=" border-b p-3 mb-2 rounded-xl bg-green-800 hover:bg-green-800 hover:bg-opacity-55 active:bg-green-700 active:bg-opacity-55 hover:border-0" v-for="ingredient in ingredients" :key="ingredient.strIngredient">
          <nuxt-link :to="`/content/ingredient/${ingredient.strIngredient}`">
            <p class=" font-bold text-lime-400 cursor-pointer text-sm">{{ingredient.strIngredient}}</p>
          </nuxt-link>
          </div>
        </div>
      </div>
  </div> 
</div>
<footer>
 <div class=" bg-green-900 text-lime-100 py-2 text-center">
  <p class=" p-3 pt-2 cursor-pointer text-sm"><span class=" font-bold ">Fine Dassh</span> is a practice app created by <span class=" font-bold">Ovo</span> in Oct, 2025. <br>
  This app was built around the API from <span class=" opacity-70 hover:underline">TheMealDB.com</span></p>
 </div>
</footer>
</template>
<script setup>
// import { useStorage } from "@vueuse/core"
const url = 'https://www.themealdb.com/api/json/v1/1'
const randomFood = ref('')
const category = ref('')
const ingredients = ref('')
const mealOfTheDay = ref('')
const countries = ref('')
const activeTab = ref('Category')


const {data, refresh, error} = await useFetch(`${url}/random.php`)
watchEffect( ()=>{
  randomFood.value = data.value?.meals[0];
  console.log(randomFood.value)
    console.log( `new value : ${randomFood.value}`)
})
const {data:meal} = await useFetch(`${url}/filter.php?i=beef`)
const date = new Date()
console.log(date.getDay())
 mealOfTheDay.value = await meal.value?.meals[date.getDay()];
console.log(mealOfTheDay.value );

const {data:dataRecommend} = await useFetch(`${url}/filter.php?i=chicken`)
 category.value = await dataRecommend.value?.meals[date.getDay()];
console.log(dataRecommend.value );

 const listOfCategory = ref('')
const {data:listCategories} = await useFetch(`${url}/list.php?c=list`)
listOfCategory.value = await listCategories.value?.meals;
// total.value = [...listCategories.value.meals].length
// console.log(listOfCategory.value , total.value);

const {data:listCountries} = await useFetch(`${url}/list.php?a=list`)
countries.value = await listCountries.value?.meals;
// totalCountries.value = [...listCountries.value.meals].length
// console.log(countries.value, totalCountries.value, listCountries.value);

const {data:Ingredients} = await useFetch(`${url}/list.php?i=list`)
ingredients.value = await Ingredients.value?.meals;
// totalIngredients.value = [...Ingredients.value.meals].length
// console.log(ingredients.value, totalIngredients.value, Ingredients.value);
const total = ref('')
total.value = [...listCategories.value.meals].length
const isBtnClicked = (name)=>{
 console.log(name)
activeTab.value = name
if(activeTab.value ==='ingredient'){
  total.value = [...Ingredients.value.meals].length
  console.log('help')
  }else if (activeTab.value ==='Category'){
    total.value = [...listCategories.value.meals].length
  }else if(activeTab.value ==='Country')
  total.value = [...listCountries.value.meals].length
  }
const isActive= (name)=>{
  if(activeTab.value === name){
    return 'bg-green-900'
  }
}  
const saved = useState('saved', ()=>[])
const favourite = (meal)=>{
  saved.value.push(meal)
  localStorage.setItem('saved',JSON.stringify(saved.value))
}
</script>



<style>
  .card{
    height:280px;
    width:480px;
    /* background-color: rgba(9, 14, 1, 0.5); */
    border-radius: 30px;
  }
  .scroll{
    height: 500px;
  }

</style>