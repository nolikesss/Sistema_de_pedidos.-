<template>
    <div id="main-banner">
        <h1>Make Your Burger</h1> 
    </div>
</template>

<script>
export default {
    name: "BAnner"
}

</script>


<style scoped>
    #main-banner{
        background-image: url("@/assets/b.jpg");
        background-size: cover;
        background-repeat: no-repeat;
        background-position:  0 -500px;
        height: 500px;
        display: flex;
        align-items: center;
        color: antiquewhite;
    }
    #main-banner h1{
        margin-left: 50px;
    }

</style>