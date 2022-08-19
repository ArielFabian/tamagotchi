<template class="imgcon">
  <div class="container mt-5 imgcon">
    <div class="row">
      <h1 v-if="estadoActual == 0">Tranquilo</h1>
      <h1 v-if="estadoActual == 1">Hambriento</h1>
      <h1 v-if="estadoActual == 2">Enojado</h1>
      <h1 v-if="estadoActual == 3">Con sueño</h1>
      <h1 v-if="estadoActual == 4">Dormido</h1>
      <h1 v-if="estadoActual == 5">Cansado</h1>
      <h1 v-if="estadoActual == 6">Triste</h1>
      <h1 v-if="estadoActual == 7">Fuera de combate!</h1>
    </div>
    <div class="row mt-5 justify-content-center">
      <div class="col-3"></div>
      <div class="col-6">
        <img class="img-dimensions" v-if="estadoActual == 0" src="~assets/pikachu_tranquilo.jpg">
        <img class="img-dimensions" v-if="estadoActual == 1" src="~assets/pikachu_hambriento.jpg">
        <img class="img-dimensions" v-if="estadoActual == 2" src="~assets/pikachu_enojado.jpg">
        <img class="img-dimensions" v-if="estadoActual == 3" src="~assets/pikachu_sueño.jpg">
        <img class="img-dimensions" v-if="estadoActual == 4" src="~assets/pikachu_dormido.jpg">
        <img class="img-dimensions" v-if="estadoActual == 5" src="~assets/pikachu_pereza.jpg">
        <img class="img-dimensions" v-if="estadoActual == 6" src="~assets/pikachu_triste.jpg">
        <img class="img-dimensions" v-if="estadoActual == 7" src="~assets/pikachu_muerto.jpg">
      </div>
      <div class="col-3"></div>
    </div>
    <div class="row mt-5 justify-content-center">
      <div class="col-3"></div>
      <div class="col-6">
        <b-button pill class="pokemon-btn mx-1" @click="cambiarEstado(estadoActual, comer)">Dar de comer</b-button>
        <b-button pill class="pokemon-btn mx-1" @click="cambiarEstado(estadoActual, acariciar)">Acariciar</b-button>
        <b-button pill class="pokemon-btn mx-1" @click="cambiarEstado(estadoActual, despertar)">Despertar</b-button>
        <b-button pill class="pokemon-btn mx-1" @click="cambiarEstado(estadoActual, dormir)">Dormir</b-button>
        <p>Cuenta para inactividad {{countDown}}</p>
      </div>
      <div class="col-2"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  data(){
    return {
      tablaTransicion: [
        [1,8,3,8,8],
        [2,0,8,8,8],
        [7,8,0,8,8],
        [6,8,8,8,4],
        [0,8,8,5,8],
        [6,8,3,8,8],
        [7,8,3,8,8],
        [8,8,8,8,8]
      ],
      //Estado
      tranquilo: 0,
      hambriento: 1,
      enojado: 2,
      sueño: 3,
      dormido: 4,
      pereza: 5,
      triste : 6,
      muerto: 7,
      //Acciones
      nada: 0,
      comer: 1,
      acariciar: 2,
      despertar: 3,
      dormir: 4,
      //Generales
      estadoActual : 0,
      countDown : 10,
      sinAccion: false,
    }
  },
  methods : {
    cambiarEstado(estadoActual,accion){
      const dato = this.tablaTransicion[estadoActual][accion]
      if(dato == 8)
      {
        this.$bvToast.toast("Quizas pikachu desea otra cosa")
        return this.estadoActual
      } else {
        this.estadoActual = dato
        this.countDown = 10
        return this.estadoActual
      }
    },
    inactivo(){
      this.cambiarEstado(this.estadoActual, this.nada)
      return console.log("set timer");
    },
    countDownTimer() {
      if(this.countDown > 0) {
        setTimeout(() => {
            this.countDown -= 1
            this.countDownTimer()
        }, 1000)
      }
    },
  },
  mounted() {
    this.countDownTimer()
  },
  watch : {
    countDown : function(){
      if(this.countDown <= 1){
        this.inactivo()
      }
    },
  },
}
</script>

<style>
.img-dimensions{
  width: 500px;
  height: 500px;
}
.pokemon-btn{
  outline-color: black;
  color: black;
  background-color: gold;
}
template
{
    background-image: url("~assets/pikachu_dormido.jpg");
 width: 1600px;
 height: 1200px;
    background-repeat: no-repeat;
    background-size: 100% auto;
    background-position: center top;
    background-attachment: fixed;
 color:white;

}
</style>
