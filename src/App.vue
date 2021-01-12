<template>
  <div id="app">
  <img src="./assets/moldura.png" alt="" class="img">
  <a class="timer">{{numero}}</a>
    <div class="areaBtn">
      <button class="botao" @click="vai" >{{botao}}</button>  
      <button class="botao" @click="limpar" >LIMPAR</button>  
    </div>
    <div class="list" v-show="historico.length > 0">
      <ul>
        <li v-for="item in historico" :key="item">VOCÊ FEZ UMA PAUSA EM {{item}}</li>
      </ul>
      <button @click="historico = []">Limpar Histórico</button>
    </div>    
  </div>
</template>

<script>


export default {
  name: 'App',
  data(){
    return{
      numero: 0,
      botao: 'VAI',
      timer: null,
      ss: 0,
      mm: 0,
      hh: 0,
      historico: []
    }
  },
  methods:{
    vai(){
      if(this.timer !== null){
        //AQUI TEM ALGO RODANDO NO TIMER...
        clearInterval(this.timer);
        this.timer = null;
        this.botao = 'VAI';
        if(this.ss !== 0){
          this.historico.push(this.numero);
        }

      }else{
        //O TIME ESTA ZERADO OU PARADO...
        this.timer = setInterval(() => {
          this.rodarTime();
        }, 100); //1 segundo = 1000 milisegundos
        this.botao = 'PAUSAR';
      }
    },
    limpar(){
      if(this.timer !== null){
        clearInterval(this.timer);
        this.timer = null;
      }
      this.ss = 0;
      this.mm = 0;
      this.hh = 0;
      this.numero = 0;
      this.botao = 'VAI';
    },
    rodarTime(){
      this.ss++;
      if(this.ss == 59) {
        //Deu 59 segundos
        this.ss = 0;
        this.mm++;
      }

      if(this.mm ==59) {
        //chegou a 59 minutos
        this.mm = 0;
        this.hh++;
      }

      let format = (this.hh < 10 ? '0'+this.hh : this.hh) + ':'
      + (this.mm < 10 ? '0'+this.mm : this.mm) + ','
      + (this.ss < 10 ? '0'+this.ss : this.ss);

      return this.numero = format;
    }
  }
  
}
</script>

<style>
  #app{
    display: flex;
    width: 100%;
    align-items: center;
    justify-content: center;
    flex-direction: column;
  }
  .img{
    width: 440px;
    height: 630px;
    padding-top: 40px;
  }
  .timer{
    color: blueviolet;
    font-size: 70px;
    margin-top: -57  0px;
  }
  .areaBtn{
    margin-top: 15px;
    display: flex;
  }
  .botao{
    -webkit-user-select: none;
    -moz-user-select: none;
    width: 100px;
    background-color: rgb(135, 155, 222);
    font-size: 20px;
    text-align: center;
    margin: 0 15px;
    border: none;
    border-radius: 8px;
    padding: 7px;
    cursor: pointer;
  }
  .botao:hover{
    opacity: 0.6;
    transition: all 0.50s;
  }

  ul{
    text-align: center;
    padding: 0;
  }
  ul li{
    margin-top: 4px;
    padding: 15px;
    background-color: coral;
    list-style: none;
    color: #fff;
    font-size: 12px;
    border-radius: 6px;
  }
  .list button{
    cursor: pointer;
    border: 0;
    background-color: #fff;
    padding: 8px;
    border-radius: 8px;
    margin-bottom: 12px;
  }
</style>
