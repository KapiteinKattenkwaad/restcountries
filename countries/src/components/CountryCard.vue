<template>
  <div class="hello">
    <h2>
      Detail
    </h2>
    <br>

    <br>

   {{ country.numericCode }}
    <p>
      {{ country.name }}
    </p>

    <img width="150px" height="200px" :src=country.flag :alt=country.name>
  </div>
</template>

<script>
export default {
  name: 'DetailCountry',
  props: {
    country: Object,

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
