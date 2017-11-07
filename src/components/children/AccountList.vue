<template>
   <div class="account-list-wrapper">
       
       <h1 class="text-left">Accounts</h1>
       <ul class="account-list">
           <li :class="{ active : isActive == key }" @click="showClickedAccount(name, key)" class="account-list__item" v-for="( name, key ) in accountNames">
               {{ name }}
           </li>
       </ul>
       
   </div>
</template>

<script>
    import ACCOUNT_DATA from '../../util/accounts.js';
    
    export default {
        name: 'AccountList',
        data() {
            return {
                isActive: 0
            }
        },
        methods: {
            showClickedAccount( name, key ) {
                // Pass the index of the clicked name to set the active class.
                this.activateClass( key );
                // Retreive the clicked Array using filter
                const selectedAccount = ACCOUNT_DATA.filter( account => account.AccountName === name );
                // Grab only the properties from the clicked Name.
                let selectedPropsFromAccount = selectedAccount[0].Properties;
                // Emit event up to parent with the selectedAccount data.
                this.$emit( 'clicked', selectedPropsFromAccount );
            },
            activateClass( index ) {
                this.isActive = index;
            }
        },
        computed: {
            accountNames() {
                return ACCOUNT_DATA.map( item => item.AccountName )
            }
        }
    };
</script>

<style lang="scss">


</style>