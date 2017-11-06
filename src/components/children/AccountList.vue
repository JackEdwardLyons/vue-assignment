<template>
   
   <div class="account-list-wrapper">
       <h1 class="text-left">Accounts</h1>
       <ul class="account-list">
           <li @click="showClickedAccount(name)" class="account-list__item" v-for="name in accountNames">
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
                // selectedAccount: []
            }
        },
        methods: {
            showClickedAccount( name ) {
                const selectedAccount = ACCOUNT_DATA.filter( account => account.AccountName === name );
                // Emit event up to parent with the selectedAccount data.
                this.$emit( 'clicked', selectedAccount )
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