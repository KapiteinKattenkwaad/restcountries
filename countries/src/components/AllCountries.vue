<template>
    <div class="all-countries text-white max-w-5xl px-4 my-12 mx-auto">
        <div class="top-wrapper flex justify-between content-center">
            <div class="search">
                <input
                        class="px-6 py-3 bg-dark-blue text-white text-sm rounded "
                        v-on:keyup="getNameCountry"
                        v-model="nameCountry"
                        placeholder="Search country">
            </div>
            <div class="region">
                <label for="region">Select your region:</label>
                <select @change="getRegion"
                        v-model="region"
                        name="region" id="region">
                    <option v-for="region in regions" :key="region.index"
                            :value="region">
                        {{ region }}
                    </option>
                </select>
            </div>
        </div>
        <div v-if="loading">

            <div class="globe-wrapper flex justify-center text-center">
                <img class="globe"
                     src="./../assets/icons/worldwide.svg" alt="globe">

                <p>
                    Loading
                </p>
            </div>
        </div>
        <div class="countries-list flex flex-wrap">
            <div v-for="country in countries" :key="country.name">

                <router-link :to="{ name: 'DetailCountry', params: { name: country.name }}">

                    <CountryCard
                            class="country-card flex flex-col flex-wrap  bg-dark-blue rounded shadow-lg mr-8 my-8"
                            :country=country
                    >
                    </CountryCard>
                </router-link>
            </div>
        </div>

    </div>
</template>

<style scoped lang="scss">
    .globe {
        width: 40vw;
        margin: 4rem auto;
        animation: spin-around 3s linear infinite alternate-reverse;
    }

    @keyframes spin-around {
        0% {
            transform: rotateZ(0deg);
        }
        40% {
            transform: scale(.75);
        }
        100% {
            transform: scale(.45);
            opacity: .6;
        }

    }

    .search {
        input {
            &::placeholder {
                color: white;
            }
        }
    }

    .country-card {
        transition: all .3s ease;
        &:hover {
            transform: translateY(-3px);
            box-shadow: none;
        }
    }
</style>

<script>
    import axios from 'axios'
    import CountryCard from "./CountryCard";
    import gsap from 'gsap'

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
                ],
                loading: true,
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
                .finally(() => this.loading = false)


        },
        created() {
            if (this.loading === false) {
                gsap.fromTo('.country-card',
                    {opacity: 0},
                    {
                        opacity: 1,
                        duration: 3
                    })
            }

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
                    .finally(() => this.loading = false)
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
