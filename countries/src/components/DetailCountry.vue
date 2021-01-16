<template>
    <div class="hello">
        <h2>
            Detail
        </h2>

        <p>
            {{ singleCountry.name }}
        </p>



    </div>
</template>

<script>
    import axios from 'axios'

    export default {
        name: 'DetailCountry',
        props: {
            country: String,

        },
        data() {
            return {
                singleCountry: {}
            }
        },
        methods: {
            getSingleCountry() {
                axios.get(`https://restcountries.eu/rest/v2/name/${this.$route.params.name}`)
                    .then(response => {
                        console.log(response)
                        this.singleCountry = response.data[0]
                    }).catch(error => {
                    console.log(error)
                })
            }
        },
        created() {
            this.getSingleCountry()
        }
    }
</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
