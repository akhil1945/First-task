<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <TopHeader/>
    <MainHeader/>
    <Product/>
    <!-- <Pagination/> -->
    <Footer/>
    
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import TopHeader from './components/TopHeader.vue'
import MainHeader from './components/MainHeader.vue'
import Footer from './components/Footer.vue'
import Product from './components/Product.vue'
// import Pagination from './components/Pagination.vue'

export default {
  name: 'App',
  components: {
    // HelloWorld,
    TopHeader,
    MainHeader,
    Footer,
    Product,
    // Pagination
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  /* margin-top: 60px; */
}
</style>
