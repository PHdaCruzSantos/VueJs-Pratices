<template>
  <div id="app">
    <header>
      <Navbar />
    </header>
  </div>
</template>

<script>
import Navbar from './components/Navbar.vue';

export default {
  components: { Navbar }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'montserrat', sans-serif;
}
header {
  width: 100vw;
  background-color: #303030;
  padding: 15px;
}

</style>
