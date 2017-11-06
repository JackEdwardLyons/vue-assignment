<template>
  <div id="app">
    <img width="100" src="./assets/logo.png">
    <h1>Account Search Demo</h1>
    
    <AccountLookup />
    
  </div>
</template>

<script>
import AccountLookup from './components/AccountLookup';

export default {
  name: 'app',
  components: {
    AccountLookup
  }
}
</script>

<style lang="scss">
$primaryColor: #2c3e50;

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: $primaryColor;
  margin-top: 60px;
}
</style>
