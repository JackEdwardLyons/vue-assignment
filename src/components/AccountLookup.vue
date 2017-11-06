<template>
  <div class="container">
    
    <div class="account-ui-wrapper">
      <AccountSearch />
      <div class="flex">
        <AccountList />
        <AccountProperties />
      </div>
    </div>
    
  
  </div>
</template>

<script>
import AccountSearch     from './children/AccountSearch';
import AccountList       from './children/AccountList';
import AccountProperties from './children/AccountProperties';

export default {
  name: 'AccountLookup',
  components: { 
    AccountSearch,
    AccountList,
    AccountProperties
  },
  data () {
    return {
      
    };
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

.container {
  width: 75%;
  margin: 0 auto;
  border: 1px solid black;
}

.account-ui-wrapper {
  padding: 10px;
  background: goldenrod;
}

.flex {
  display: flex;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
