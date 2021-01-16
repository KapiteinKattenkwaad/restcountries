<template>
  <div class="home">
  <Navbar/>
  <AllCountries />
  </div>
</template>

<script>
// @ is an alias to /src
import Navbar from "../components/NavBar";
import AllCountries from "../components/AllCountries";

export default {
  name: 'Home',
  components: {
    AllCountries,
    Navbar,
  }
}
</script>
