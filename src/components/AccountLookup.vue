<template>
  <div class="container">
    <!-- Account Lookup -->
    <div class="account-ui-wrapper">
      <AccountSearch @clicked="showSelectedAccount" 
                     @searched="findAccountMatch" 
                     :matchedAccounts="matchedAccounts" 
      />
      <div class="flex space-around">
        <AccountList @clicked="showSelectedAccount" :selectedAccountIndex="selectedAccountIndex" />
        <AccountProperties :selectedAccount="selectedAccount" />
      </div>
    </div>
    <!-- end Account Lookup -->
  </div>
</template>

<script>
  import AccountSearch     from './children/AccountSearch';
  import AccountList       from './children/AccountList';
  import AccountProperties from './children/AccountProperties';
  import ACCOUNT_DATA      from '../util/accounts.js';
      
  export default {
    name: 'AccountLookup',
    components: { 
      AccountSearch,
      AccountList,
      AccountProperties
    },
    data () {
      return {
        selectedAccount: [],
        searchTerm: '',
        allAccountData: ACCOUNT_DATA,
        matchedAccounts: [],
        selectedAccountIndex: 0
      };
    },
    methods: {
      
      showSelectedAccount( account, key ) {
        this.selectedAccount = [];
        this.selectedAccountIndex = key;
        // This gets the emitted payload from the AccountList Component
        this.selectedAccount = account;
      },
      
      findAccountMatch( query ) {
        // Start fresh on each function call
        this.searchTerm      = [];
        this.matchedAccounts = [];
        this.searchTerm = query;
        
        const data = this.allAccountData;
        
        let searchMatch = data.filter( ( name, index ) => {
          // Figure out if the account name matches the search term.
          const regex = new RegExp( query, 'gi' );
          // If it does, return the matching Account Array
          console.log( 'props', name.Properties.map( prop => prop ) );
          return name.AccountName.match( regex );
        });
        return this.matchedAccounts.push( searchMatch );
      }
      
    },
    created() {
      this.selectedAccount = ACCOUNT_DATA[0].Properties;
    }
  };
</script>

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

</style>
