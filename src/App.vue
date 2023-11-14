<script>
import { RouterLink, RouterView } from 'vue-router'
import './style.css'
export default{
  mounted(){
    if(window.localStorage.login){
      import.meta.env.VITE_LOGIN = window.localStorage.login
    }
    import.meta.env.VITE_LOGIN == "false"? this.$router.push("/auth"): false
  }
}
</script>

<template>

  <RouterView />
</template>

<style>
*{
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  caret-color: transparent;
}
</style>
