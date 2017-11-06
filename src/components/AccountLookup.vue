<template>
  <div class="container">
    
    <div class="account-ui-wrapper">
      <AccountSearch />
      <div class="flex">
        <AccountList @clicked="showSelectedAccount" />
        <AccountProperties :selectedAccount="selectedAccount" />
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
      selectedAccount: []
    };
  },
  methods: {
    showSelectedAccount( account ) {
      this.selectedAccount = account;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

.container {
  width: 75%;
  margin: 0 auto;
}

.account-ui-wrapper {
  padding: 10px;
  border: none;
  background: #D6DCDB;
  box-shadow: 0 3px 6px rgba(0,0,0,0.16), 0 3px 6px rgba(0,0,0,0.23);
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
