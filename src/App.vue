<template>
  <div id="app">
    
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

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
}
</style>
