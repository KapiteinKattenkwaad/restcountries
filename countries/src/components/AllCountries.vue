<template>
    <div class="hello">
        <h2>
            All Countries
        </h2>
      <label for="region">Select your region:</label>
        <select @change="getRegion" v-model="region" name="region" id="region">
            <option v-for="region in regions" :key="region.index" :value="region">
                {{ region }}
            </option>
        </select>
      <br>

      <input v-on:keyup="getNameCountry" v-model="nameCountry" placeholder="Search country">
      <p>Message is: {{ nameCountry }}</p>

        <div v-for="country in countries" :key="country.name">
          <router-link  :to="'/country/' + country.name">
            <CountryCard
              :country=country
            >
              <h6>
                {{ country.name }}
              </h6>
            </CountryCard>
          </router-link>

        </div>


    </div>
</template>

<script>
    import axios from 'axios'
    import CountryCard from "./CountryCard";

    export default {
        name: 'AllCountries',
      components: {CountryCard},
      props: {},
        data() {
            return {
                countries: null,
                region: null,
                nameCountry: null,
                regions: [
                    'Africa', 'Americas', 'Asia', 'Europe', 'Oceania'
                ]
            }
        },

        mounted() {
            axios
                .get('https://restcountries.eu/rest/v2/all')
                .then(response => {
                    console.log(response.data[0])
                    this.countries = response.data
                })
                .catch(function (error) {
                    console.log(error);
                })


        },
        methods: {
            getRegion() {
                axios
                    .get(`https://restcountries.eu/rest/v2/region/${this.region}`)
                    .then(response => {
                        this.countries = response.data
                    })
                    .catch(function (error) {
                        console.log(error)
                    })
            },
            getNameCountry() {
              axios
                      .get(`https://restcountries.eu/rest/v2/name/${this.nameCountry}`)
                      .then(response => {
                        console.log('response', response.data)
                        this.countries = response.data
                      })
                      .catch(function (error) {
                        console.log(error)
                      })
            }
        },

    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
