<script setup>
import SplashScreen from "./components/SplashScreen.vue"
import { defineAsyncComponent, ref} from "vue";

const Home = defineAsyncComponent(()=>{
  return new Promise((resolve) => {
    
      setTimeout(() => {
        resolve(import("./components/Home.vue"))
      }, 2500)
  })
})

</script>

<template>
  <Suspense>
    <template #default>
      <Home/>
    </template>
    <template #fallback>
      <SplashScreen class="splash-hide" />
    </template>
  </Suspense>
</template>
<style>
  html,
  body,
  .app {
    min-height: 100vh;
    margin: 0;
    font-family: Arial, Helvetica, sans-serif;
  }
  * {
    --brand-green: #04b500;
    --brand-blue: #0689b0;
  }

  .scr-enter-from {
  opacity: 1;
  }
  .scr-enter-to {
  opacity: 0;
  }

  .scr-enter-active{
        transition: opacity 5s ease;
    }

    .splash-hide{
      animation: hiden 1s normal;
      animation-delay: 1.5s;
      animation-fill-mode: forwards;
    }

    @keyframes hiden {
     from { opacity:1}
     to{opacity: 0;} 
    }

</style>