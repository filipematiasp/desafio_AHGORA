<template>
  <div class="container min-vh-100 d-flex flex-column justify-content-center align-items-center">
    <div>
      <p class="h3">Entre com a sequência de DNA</p>
    </div>
    <div class="input-group">
      <input type="text" class="form-control" placeholder="Entre com a sequência: EX:['CTGAGA', 'CTATGC', 'TATTGT', 'AGAGGG', 'CCCCTA', 'TCACTG']" aria-label="Sequence dna" aria-describedby="button-addon2">
      <button class="btn btn-outline-secondary" type="button" id="button-addon2">Analisar</button>
    </div>
    <div>
      <p class="h3">{{species}}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'SearchSequenceBar'
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
