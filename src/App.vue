<template>
    <Navbar :logo="logo_src"  :alt="app_name"/>
    <router-view/>
    <Footer/>
</template>

<script>
  import Navbar from './components/Navbar.vue';
  import Footer from './components/Footer.vue'



 export default {
  components: {
    Navbar,Footer,
  },
    data(){
      return{
        logo_src: "/img/logo.png",
        app_name: "Escolha seu Hamburguer"
      }
    }

 }

</script>



<style>
:root{
  --yellow: #FCBA03;
}

*{
  font-family: 'Courier New', Courier, monospace;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.main-container{
  margin: 50px;
  min-height: 660px;
  margin-left: 150px ;

}

h1{
  display: flex;
  justify-content: center;
  text-align: center;
  font-size: 42px;
  margin-bottom: 20px;
}

</style>
