<template>
  <div id="burger-table">
    <div>
      <div id="burger-table-heading">
        <div class="order-id">#:</div>
        <div>Cliente:</div>
        <div>Pão:</div>
        <div>Carne:</div>
        <div>Opcionais:</div>
      </div>
    </div>

    <div id="burger-table-rows">
      <div class="burger-table-row" v-for="burger in burgers" :key="burger.id"> <!--Repitição v-for -->
        <div class="order-number">{{burger.id}}</div>
        <div>{{burger.nome}}</div>
        <div>{{burger.pao}}</div>
        <div>{{burger.carne}}</div>

        <div>
          <ul>
            <li v-for="(opcional,index) in burger.opcionais" :key="index">{{ opcional }}</li>    <!--Repitição v-for -->
          </ul>
        </div>

        <div class="action-select">
          <select name="status" class="status">
            <option>Selecione</option>
            <option  v-for="Status in status" :key="Status.id" value="Status.tipo" :selected="burger.status == Status.tipo">{{Status.tipo}}</option>

          </select>
          <button class="delete-btn" @click="deleteBurger(burger.id)">Cancelar</button>
        </div>
      </div>
      
      
    </div>
  </div>

</template>



<script>
export default {
  name: "DashBoard",
  data(){
    return{
        burgers: null,
        burger_id: null,
        status: []
    }
  },
  methods: {
    async getPedidos(){
    const requisition = await fetch('http://localhost:3000/burgers')
    const data = await requisition.json();
    
    this.burgers = data;


        console.log(this.burgers)
    //resgatar status
        this.getStatus();
     },
     async getStatus() {

        const requisition = await  fetch('http://localhost:3000/status');
        const data = await requisition.json();
        
        this.status = data;

     },
     async deleteBurger(id){
       const requisition = await fetch(`http://localhost:3000/burgers/${id}`,{
        method: "DELETE"
       });

       const res = await requisition.json();

       //msg
       this.getPedidos();

     }
  },

  mounted(){ // chama a func
    this.getPedidos();
  }
};
</script>


<style scoped>
#burger-table {
  max-width: 1200px;
  margin: 0 auto;
}
#burger-table-heading,
#burger-table-rows,
.burger-table-row {
  display: flex;
  flex-wrap: wrap;
}

#burger-table-heading{
    font-weight: bold;
    padding: 12px;
    border-bottom: 3px solid #333;
}
#burger-table-heading div,
.burger-table-row div{
    width: 19%;
}

.burger-table-row{
    width: 100%;
    padding: 12px;
    border: 1px solid rgb(8, 8, 8);
  
}
#burger-table-heading .order-id,
.burger-table-row .order-number{
    margin-bottom: 10px;
}

.action-select select,button{
    margin: 10px;
    
}


</style>















