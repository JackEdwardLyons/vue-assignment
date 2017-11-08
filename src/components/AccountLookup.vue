<template>
  <div class="container">
    <!-- Account Lookup -->
    <div class="account-ui-wrapper">
      <AccountSearch @clicked="showSelectedAccount" 
                     @searched="findAccountMatch" 
                     @newDropDownOption="getNewCategory"
                     :matchedAccounts="matchedAccounts" 
                     :allAccountData="allAccountData"
      />
      <div class="flex space-around">
        <AccountList @clicked="showSelectedAccount" :selectedAccountIndex="selectedAccountIndex" />
        <AccountProperties :allAccountData="allAccountData" 
                           :dropDownOption="dropDownOption" 
                           :selectedAccount="selectedAccount" 
                           :searchTerm="searchTerm" />
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
        searchTerm: '',
        selectedAccount: [],
        matchedAccounts: [],
        selectedAccountIndex: 0,
        dropDownOption: 'Accounts',
        allAccountData: ACCOUNT_DATA,
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
        /* Tricky Code Alert!
         * In order to retreive all the Property Names from each account
         * I have created an array flatten function which iterates through
         * each account and it's corresponding 'Properties'.
         * This is done by concatenating all the Property Arrays using reduce
         */
         
         // This could be refactored into a computed prop...
        const props = data.map( account => account.Properties );
        const flattenArr = ( arr ) => arr.reduce((a, b) => {
            return a.concat( Array.isArray( b ) ? flattenArr(b) : b )
        }, [])
        // Finally just iterate over the Array list and grab the Names
        let allProps     = flattenArr( props );

        let matchingNames = data.filter( ( name, index ) => {
          // Figure out if the account name matches the search term.
          const regex = new RegExp( query, 'gi' );
          return name.AccountName.match( regex );
        });
        // Do the same for the account Property
        let matchingProperties = allProps.filter( property => {
          const regex = new RegExp( query, 'gi' );
          return property;
        })
        
        if ( this.dropDownOption === 'Accounts' ) {
          return this.matchedAccounts.push( matchingNames );
        } else {
          return this.matchedAccounts.push( matchingProperties );
        }
      },
      
      getNewCategory( payload ) {
        this.dropDownOption = payload;
        this.selectedAccountIndex = 0;
        this.selectedAccount = ACCOUNT_DATA[0].Properties;
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