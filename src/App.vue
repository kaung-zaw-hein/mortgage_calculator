<template>
 <h3>Mortgage Calculator</h3>
  <Result @reset="reset" :data="data"></Result>
  <Main @result="results"></Main>
  <img src="./assets/logo.png" alt="">
</template>

<script>

import Result from './components/Result'
import Main from './components/Main'
import {ref} from 'vue'
export default {
  name: 'App',
  components: {
    Result,
    Main,
  },
  setup(){
    const data = ref();
    const results = (a) => {
      data.value = a;  
    };
    const reset =() => {
      data.value = null;
    }
    return {data,results,reset};
  }
}
</script>

<style>
*{
  padding:0;
  margin:0;
}
body{
  background-color:#333;
  display: flex;
  align-items: center;
  justify-content:center;
  height:100vh;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #ffffff;
  display: flex;
  align-items: center;
  justify-content:flex-start;
  flex-direction:column;
  width:80%;
  height:75vh;
  border-radius: 10px;
  padding: 20px;
}
#app img{
  position:absolute;
  top:0;
  left:0;
  width:190px;
  height: 60px;
}
#app h3{
  font-size:3em;
  font-weight:800;
  padding-bottom: 20px;
}
</style>
