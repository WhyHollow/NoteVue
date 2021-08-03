<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <h1>NOTES APP</h1>
    <Notes />
  </div>
</template>

<script>
  import Notes from './components/Notes.vue';

  export default {
    name: 'App',
    components: {
      Notes,
    },
  };
</script>

<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
</style>
