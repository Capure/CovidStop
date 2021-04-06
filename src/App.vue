<template>
  <Header/>
  <ToggleMode @toggled="(newValue) => {this.global = newValue}" />
  <DisplayData :global="global" />
</template>

<script>
import DisplayData from './components/DisplayData.vue';
import Header from './components/Header.vue';
import ToggleMode from './components/ToggleMode.vue';

export default {
  name: 'App',
  data() {
    return {
      global: true
    }
  },
  components: {
    Header,
    ToggleMode,
    DisplayData
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Raleway:wght@100;200;300;400;500;600;700;800;900&display=swap');

body {
  margin: 0;
  font-family: 'Raleway', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background-color: #000;
  color: white;
}
</style>
