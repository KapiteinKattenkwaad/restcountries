<template>
    <div class="country-card ">
        <img width="220px" height="160px" :src=country.flag :alt=country.name>
        <div class="country-card-wrapper p-4 px-6">
            <p class="font-semibold">
                {{ country.name }}
            </p>
        </div>
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
