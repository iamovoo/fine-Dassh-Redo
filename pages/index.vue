<template>
<div class=" flex flex-col justify-center items-center text-center gap-16 ">
  <div class="content bg-green-800 p-6 rounded-2xl shadow-lg dashboard">
    <h1 class="text-3xl font-bold text-lime-400 mb-2">Welcome {{user}}</h1>
    <p class="text-lime-400 mb-4">Enter your name to explore amazing recipes</p>
    <form @submit.prevent="getUsername" class="flex gap-2 justify-center">
      <input type="text" v-model="usernameInp" placeholder="Your name" class="px-4 py-2 rounded-lg border-none bg-green-700 text-lime-400 placeholder:text-lime-200 w-96 h-10"/>
      <button type="submit" class="bg-greeb-500 hover:bg-green-600 text-lime-400 shadow-2xl font-semibold px-4 py-2 rounded-lg border-lime-400 border">Start &#8593;</button>
    </form>
  </div>
  <div>
    <h3 class=" font-bold font-serif text-green-900 text-4xl" > Welcome to <br/> <span class=" text-7xl">Fine Dassh</span></h3>
      <p class=" text-lime-500 py-3 text-xl font-bold">Find fun recipes for meals from around the world. <br /> Whether you're a seasoned chef or just starting your cooking journey,
      these recipes are your key <br />to creating mouthwatering masterpieces in your very own kitchen. <br /> Help us to help you !! Bless</p>
    </div>
</div>
</template>
<script setup>
definePageMeta({
  layout: false,
  middleware: function(to,from){
    const savedRecipies = useCookie('savedRecipies', {default: ()=> []})
    savedRecipies .value = null
    const saved = useCookie('saved', {default:()=>''})
    saved.value = null
    const user = useCookie('user', {default: ()=>""})
    user.value = null
  }
})
const user = useCookie('user', {default: ()=>""})
const usernameInp = ref('')

const getUsername = ()=>{
  user.value = usernameInp.value[0].toLocaleUpperCase() + usernameInp.value.slice(1)
  setTimeout(()=>{
     return navigateTo('/content')
  },2000)
 
}
</script>
<style>
.dashboard{
  width: 650px;
}
</style>