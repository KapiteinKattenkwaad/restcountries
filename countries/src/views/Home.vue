<template>
  <div class="home">
    <Navbar />
  <AllCountries />
  </div>
</template>

<script>
// @ is an alias to /src
import AllCountries from "../components/AllCountries";
import Navbar from "../components/NavBar";

export default {
  name: 'Home',
  components: {
      Navbar,
    AllCountries,

  }
}
</script>
