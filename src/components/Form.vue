<template>
  <div>
    <Msg :msg="msg" v-show="msg"/>
    <div>
      <form id="burger-form" @submit="creatBurger">
        <div class="input-container">
          <label for="Nome">Nome do cliente:</label>
          <input
            type="text"
            id="nome"
            name="nome"
            v-model="nome"
            placeholder="Digite o nome!"
          />
        </div>
        <div class="input-container">
          <label for="Pao">Escolha o Pao: </label>
          <select name="pao" id="pao" v-model="pao">
            <option value="">Selecione o seu pão</option>
            <option v-for="pao in paes" :key='pao.id' :value="pao.tipo">{{pao.tipo}}</option>
          </select>
        </div>
        <div class="input-container">
          <label for="carne">Escolha sua carne: </label>
          <select name="carne" id="carne" v-model="carne">
            <option value="">Selecione a sua carne</option>
            <option v-for="carne in carnes" :key='carne.id' :value="carne.tipo">{{carne.tipo}}</option>
          </select>
        </div>

        <div  id="opcionais-container" class="input-container">
          <label id="opcionais-tittle" for="opcionais" >Selecione os opcionais </label>
          <div class="checkbox-container" v-for="opcional in opcionaisdata" :key="opcional.id" :value="opcional.tipo">
            <input type="checkbox" name="opcionais"
            v-model="opcionais" :value="opcional.tipo">
            <span>{{opcional.tipo}}</span>
          </div>
        </div>


        <div  class="input-container">
          <input  type="submit" class="submit-btn" value="criar meu Burger!!" />
        </div>
      </form>
    </div>
  </div>
</template>


<script>    
import Msg from './Msg.vue';


export default {
  name: "ForM",
 
  data(){
    return{
    paes: null,
    carnes: null,
    opcionaisdata: null,
    nome: null,
    pao: null,
    carne: null,
    opcionais: [],
    msg: null,
    }
  },
  methods: {
    async getIngredients(){
        const req = await fetch("http://localhost:3000/ingredientes");
        const data = await req.json();

        this.paes = data.paes;
        this.carnes = data.carnes;
        this.opcionaisdata = data.opcionais;
    },
    async creatBurger(e){
        e.preventDefault();

        const data = {
            nome: this.nome,
            carne: this.carne,
            pao: this.pao,
            opcionais: Array.from(this.opcionais),
            status: "Solicitado"
        }

        const dataJson = JSON.stringify(data); 

        const req = await fetch("http://localhost:3000/burgers", {
        method: "POST",
        headers: { "Content-Type" : "application/json" },
        body: dataJson
      });
        const res = await req.json()
        

        // mensagem de sistema
        this.msg =`Pedido N- ${res.id} realizado com sucesso`;
        // limpando mensagem         segundos 
        setTimeout(() => this.msg="", 2000);

        //Limpar campos
        this.nome = "";
        this.carne = "";
        this.pao ="";
        this.opcionais ="";
        
    }
  },
  mounted() {
    this.getIngredients()
  },
  components: {
    Msg
  },
};
</script>


<style scoped>
#burger-form {
  max-width: 400px;
  margin: 0 auto;
}
.input-container {
  display: flex;
  flex-direction: column;
  margin-bottom: 20px;
}
label {
  font-weight: bold;
  font-size: 20px;
  margin-bottom: 15px;
  padding: 5px 10px;
  border-left: 4px solid var(--yellow);
}

input,
select {
  padding: 5px 10px;
  width: 300px;
}
#opcionais-container{
    flex-direction: row;
    flex-wrap: wrap;
}
.checkbox-container{
    display: flex;
    align-items: flex-start;
    width: 50%;
    margin-bottom: 30px;
}
.checkbox-container span,
.checkbox-container input{
    width: auto;
}

.checkbox-container span{
    margin-left: 6px;
    font-weight: bold;
}
.submit-btn{
    background-color: #222;
    color: var(--yellow);
    font-weight: bold;
    border: 2px solid #222;
    font-size: 16px;
    cursor: pointer;
    transition: .5s;
}

.submit-btn:hover{
    background-color: transparent;


}
</style>