<template>
  <div class="container min-vh-100 d-flex flex-column justify-content-center align-items-center">
    <div>
      <p class="h3">Entre com a sequência de DNA</p>
    </div>
    <div class="btn-group mb-2" role="group" aria-label="Basic radio toggle button group">
      <input type="radio" class="btn-check" v-model="radioCheck" value="frontend" name="btnradio" id="frontend" autocomplete="off" checked>
      <label class="btn btn-outline-primary" for="frontend">FRONT-END</label>

      <input type="radio" class="btn-check" v-model="radioCheck" value="backend" name="btnradio" id="backend" autocomplete="off">
      <label class="btn btn-outline-primary" for="backend">BACK-END</label>

      <input type="radio" class="btn-check" v-model="radioCheck" value="bd" name="btnradio" id="bd" autocomplete="off">
      <label class="btn btn-outline-primary" for="bd">BANCO DE DADOS</label>
    </div>
    <div class="input-group">
      <input type="text" class="form-control" v-model="sequenceDna" placeholder="['CTGAGA', 'CTATGC', 'TATTGT', 'AGAGGG', 'CCCCTA', 'TCACTG']" aria-label="Sequence dna" aria-describedby="button-addon2">
      <button class="btn btn-outline-secondary" @click="analyzeDna" type="button" id="button-addon2">Analisar</button>
    </div>
    <div>
      <p class="h3" v-if="species" style="color:red">{{species}}</p>
    </div>
  </div>
</template>

<script>
import sequenceSearch from "../../public/script/sequenceSearch"
import api from "../services/api"

export default {

  name: 'SearchSequenceBar',
  data() {
    return {
      sequenceDna: "",
      species: "",
      radioCheck: "frontend"
    }
  },
  methods: {
    analyzeDna() {
      this.species = '';
      if(this.radioCheck === 'frontend'){
        this.frontEndAnalyzeDna();
      }
      if(this.radioCheck === 'backend'){
        this.backEndAnalyzeDna();
      }
      if(this.radioCheck === 'bd'){
        this.backEndAnalyzeBdDna();
      }
    },
    frontEndAnalyzeDna() {
      let sanitized = this.sequenceDna.replace('[', "").replace(']', "").replace(/\s/g, '').replace(/["]/g, '').split(",")
      let result = sequenceSearch(sanitized)
      console.log(result);

      if(result.count > 0){
        this.species = 'SIGMANO'
      }
      if(result.count === 0){
        this.species = 'HUMAN'
      }
    },
    backEndAnalyzeDna() {
      let sanitized = this.sequenceDna.replace('[', "").replace(']', "").replace(/\s/g, '').replace(/["]/g, '').split(",")
      let data = {
        dna: sanitized
      }
      api.post("/analisyDna",data).then((response) => {
        if(response.data.count > 0){
          this.species = 'SIGMANO'
        }
        if(response.data.count === 0){
          this.species = 'HUMAN'
        }
      })
    },
    backEndAnalyzeBdDna(){
      let sanitized = this.sequenceDna.replace('[', "").replace(']', "").replace(/\s/g, '').replace(/["]/g, '').split(",")
      let data = {
        dna: sanitized
      }
      api.post("/analisyDnaBd",data).then((response) => {
        console.log('segue filipe', response.data.specie)
        this.species = `${response.data.specie}`
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
