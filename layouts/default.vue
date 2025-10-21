<template>
<div class="relative z-10">
  <div class=" nav_bar bg-green-900 fixed">
  <p class=" font-bold text-3xl text-center pt-1 text-lime-400"><nuxt-link to="/">Fine Dassh</nuxt-link></p>
  <div class=" relative">
    <input type="text" name="" id="" class="lg:input rounded-xl p-4 bg-green-800 placeholder-lime-300 border-lime-400 text-white text-xl" placeholder=" Search... " v-model="search" @input="searchedRecipe">
  </div>
   <div class="searchBar bg-green-800 border rounded-2xl top-24 h-64 bg-opacity-80 overflow-y-scroll z-50" v-if="showSearch"> 
        <div class="relative " v-if="isNoResult"><p class=" absolute right-56 top-24 font-bold text-lime-400">No results</p></div>
        <div class=" p-3 border-b hover:bg-green-700 hover:bg-opacity-55 active:bg-green-600 active:bg-opacity-55" v-for="meal in searched" :key="meal.idMeal" @click="searchedFoodClicked">
         <nuxt-link :to="`/content/${meal.idMeal}`" @click="removeSearch"><p class=" font-bold text-lime-400 block">{{meal.strMeal}}</p></nuxt-link>
        </div>
      </div>
    <div class="control mr-8" @click=" searchedFoodClicked">
      <nuxt-link to="/saved"><p class="text-xl text-white font-semibold hover:opacity-75 hover:underline">Saved</p></nuxt-link>
      <nuxt-link to="/content"><button class="btn text-xl text-white font-semibold hover:opacity-75 hover:underline" >Home</button></nuxt-link>
      <div class="user gap-2">
      <div class="shadow-lg p-2 rounded-full bg-green-800 ">
        <img width="30" height="30" src="https://img.icons8.com/material-rounded/50/1A1A1A/user.png" alt="user"/></div>
      <span class="text-2xl text-white font-bold">Hi {{user}}</span>
      </div>
    </div>
</div>
</div>
<div class=" pt-14 w-lvw h-lvh bg-lime-50" @click=" searchedFoodClicked">
  <slot />
</div>

</template>


<script setup>
 
 const user = useCookie('user')
// console.log(user.value);
 const showSearch = ref(false)
 const search = ref('')
 const searched = ref('')
 const isNoResult = ref(false)
 const searchedRecipe = async ()=>{
  if(search.value){
    showSearch.value = true
    const {data:searchedMeals } = await useFetch(`https://www.themealdb.com/api/json/v1/1/search.php?s=${search.value}`)
    searched.value = await searchedMeals.value.meals;
      if(!searched.value){
        isNoResult.value = true
      }
      else{
        isNoResult.value = false
      }
  }
  else{
     showSearch.value = false
  }
 }
 const searchedFoodClicked = ()=>{
  showSearch.value = false
  search.value = ""
 }

</script>


<style>

.nav_bar{
  width: 100vw;
  padding: 25px;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-content: center;
}
.control{
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  width: 350px;
}
.user{
  display: flex;
  flex-direction: row;
  /* justify-content: space-between; */
  align-items: center;
  width: 190px;
}
.btn{
  border: none;;
    padding: 0;
    margin: 0;
}
input{
  width: 550px;
  height: 50px;
}
body{
  background-color: #F7FEE7;
}
.searchBar{
  width: 550px;
  position: absolute;
  left: 30%;
}
</style>