<template>
    <div class="account-list-wrapper">
        
        <h1 class="text-left">Properties</h1>
        <ul class="account-list">
            <li class="account-list__item" v-for="property in selectedAccountProps">
                {{ property }}
            </li>
        </ul>
        
    </div>
</template>

<script>
    export default {
        name: 'AccountProperties',
        props: [ 'selectedAccount', 'dropDownOption', 'allAccountData', 'searchTerm' ],
        data() {
            return {
                propIndex: 0
            }
        },
        computed: {
            selectedAccountProps() {
                
                if ( this.dropDownOption === 'Accounts' ) {
                   return this.selectedAccount.map( account => account.Name );
                } else if (this.dropDownOption === 'Properties') {
                    
                    this.propIndex = this.allAccountData.map( ( item, index ) => {
                      return item.Properties.filter( ( prop, key ) => {
                        if ( prop.Name.includes( this.searchTerm ) ) {
                          return item;
                        }
                      })
                    })

                    var getCorrectIndex = this.propIndex.findIndex( item => item.length );
                    //this.allAccountData[ propIndex ][0].map( account => account.Name )
                    
                    
                }
            }
        }
    };
</script>

<style lang="scss">

</style>