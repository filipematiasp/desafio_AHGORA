<template>
  <div class="container min-vh-100 d-flex flex-column justify-content-center align-items-center">
    <div>
      <p class="h3">Entre com a sequência de DNA</p>
    </div>
    <div class="input-group">
      <input type="text" class="form-control" v-model="sequenceDna" placeholder="['CTGAGA', 'CTATGC', 'TATTGT', 'AGAGGG', 'CCCCTA', 'TCACTG']" aria-label="Sequence dna" aria-describedby="button-addon2">
      <button class="btn btn-outline-secondary" @click="analisyDna" type="button" id="button-addon2">Analisar</button>
    </div>
    <div>
      <p class="h3" v-if="species" style="color:red">{{species}}</p>
    </div>
  </div>
</template>

<script>
import sequenceSearch from "../../public/script/sequenceSearch"

export default {

  name: 'SearchSequenceBar',
  data() {
    return {
      sequenceDna: "",
      species: ''
    }
  },
  methods: {
    analisyDna() {
      let sanitized = this.sequenceDna.replace('[', "").replace(']', "").replace(/\s/g, '').replace(/["]/g, '').split(",")
      let result = sequenceSearch(sanitized)
      console.log(result);

      if(result.count > 0){
        this.species = 'SIGMANO'
      }
      if(result.count === 0){
        this.species = 'HUMAN'
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
