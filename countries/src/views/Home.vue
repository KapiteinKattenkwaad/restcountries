<template>
  <div class="home">

  <AllCountries />
  </div>
</template>

<script>
// @ is an alias to /src
import AllCountries from "../components/AllCountries";

export default {
  name: 'Home',
  components: {
    AllCountries,

  }
}
</script>
