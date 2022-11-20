<template>
<footer id="footer">
    <p>Make Your Burger&copy; 2022</p>
</footer>
    

</template>


<script>
export default {
    name: 'Footer'

}

 

</script>

<style scoped>
#footer{
    height: 100px;
    background-color: #222;
    border-top: 4px solid #222;
    color: var(--yellow);
    display: flex;
    justify-content: center;
    align-items: center;
    text-align: center;
    width: 100%;
    bottom: 0;
   
}

#footer p{
    margin-left: 20pxpx;
}


</style>