<template>
<div class="message-container">

    <p>{{ msg }}</p>
</div>


</template>

<script>
export default {
    name: "Message",
    props: {
        msg: String
    }
}

</script>


<style>
.message-container{
  background-color: rgb(149, 186, 221);
  height: 30px;
  text-align: center;
  width:22%;
  margin-left: 630px;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 20px;
  color: rgb(2, 131, 182);
  font-weight: bold;
}

</style>