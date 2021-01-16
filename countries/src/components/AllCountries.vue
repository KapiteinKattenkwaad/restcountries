<template>
    <div class="hello">
        <h2>
            All Countries
        </h2>
      <div v-for="country in countries" :key="country.index">
        <p>
          {{ country.name }}
        </p>
        <img width="300px" height="500px" :src=country.flag :alt=country.name>
      </div>

    </div>
</template>

<script>
    import axios from 'axios'

    export default {
        name: 'AllCountries',
        props: {},
        data() {
            return {
                countries: null
            }
        },
            mounted() {
                axios
                    .get('https://restcountries.eu/rest/v2/all')
                    .then(response =>  {
                      console.log(response.data[0])
                      this.countries = response.data
                    })
                    .catch(function (error) {
                        console.log(error);
                    })
            }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
