<template>
   <nav id="nav">
    <router-link to="/" id="logo-url">
        <img :src="logo" id="logo" :alt="alt">
    </router-link>
         <router-link to="/">Home</router-link> 
        <router-link to="/pedidos">Pedidos</router-link>
     </nav>
</template>


<script>
   export default {
    name: "NavBar",

    props:  ["logo","alt"]
   }

</script>

<style scoped>

#nav{
   background-color: #222;
   border-bottom: 3px solid #111;
   padding: 15px 50px;
   display: flex;
   justify-content: flex-end;
   align-items: center;
}
#nav #logo-url{
   margin: auto;
   margin-left: 0;
}
#logo { 
    width: 100px;
}

#nav a{
    color: #fcba03;
    text-decoration: none;
    margin: 12px;
    transition: 0.1s ease-in;
    font-weight: bold;
    
}

#nav a:hover{
    color: white
}


</style>