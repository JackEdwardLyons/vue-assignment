<template>
    <div>
        <!-- Account Search -->
        <div class="search-wrapper">
            <div class="text-input-wrapper">
                <input type="search" 
                       @keyup="findAccountMatch" 
                       v-model="searchTerm" 
                       class="text-input-wrapper__search-input" 
                       placeholder="Search for an account" 
                />
                <!-- Hide and Show Dropdown based on user input -->
                <ul v-show="searchTerm.length" class="text-input-wrapper__matches account-list">
                    <li @click="clickedAccount( match, key )" 
                         class="account-list__item" 
                         v-for="( match, key ) in matchedAccountNames"
                    >
                        {{ match }}
                    </li>
                </ul>
            </div>
            
            <div class="button-wrapper flex">
                <select v-model="selectedOption" @change="postNewOption" class="text-uppercase text-input-wrapper__dropdown">
                    <option v-for="option in dropDownOptions">
                        {{ option }}
                    </option>
                </select>
            </div>
        </div>
        <!-- Account Search -->
    </div>
</template>

<script>
    export default {
        name: 'AccountSearch',
        props: [ 'matchedAccounts', 'allAccountData' ],
        data() {
            return {
                searchTerm: '',
                dropDownOptions: [ 'Accounts', 'Properties' ],
                selectedOption: 'Accounts',
                clickedAccountName: ''
            };
        },
        methods: {
            findAccountMatch() {
                this.$emit( 'searched', this.searchTerm );
            },
            clickedAccount( match, key ) {
                if ( this.selectedOption === 'Accounts' ) {
                    // Grab only the matching account properties & Iterate over all accounts
                    const accountNameProps = this.matchedAccounts[0].map( item => item.Properties );
                    const matchedIndex     = this.allAccountData.findIndex( item => item.AccountName.includes( match ) );
                    // Send payload with account name and index for toggling the "selected" class
                    this.$emit( 'clicked', accountNameProps[ matchedIndex ], matchedIndex );  
                    
                } else if ( this.selectedOption === 'Properties' ) {
                    const accountNameProps = this.matchedAccounts[0].map( item => item.Properties );
                    const regex = new RegExp( match, 'gi' );
                    
                    const matchedIndex = this.allAccountData
                      .map( account => account.Properties.map( prop => prop.Name ) )
                      .findIndex( ( name, index ) => name.indexOf( match ) > -1 );
                    // Send matched properties back to parent 
                    this.$emit( 'clicked', this.allAccountData[ matchedIndex ].Properties, matchedIndex ); 
                }
                // Empty searchTerm for next search
                this.searchTerm = '';
            },
            findPropIndex() {
                // This step is neccessarry in order to obtain the correct index
                // of the account Array which holds the searched Property Name
                const returnedProp = this.allAccountData.map( ( item, index ) => {
                    return item.Properties.filter( ( prop, key ) => {
                      if ( prop.Name.includes( this.searchTerm ) ) {
                        return item;
                      }
                    })
                })
                const propIndex = returnedProp.findIndex( item => item.length );
                return propIndex;
            },
            postNewOption() {
                // Reset tables back to original state.
                this.$emit( 'newDropDownOption', this.selectedOption );
                this.searchTerm = '';
            }
        },
        computed: {
            matchedAccountNames() {
                if ( this.matchedAccounts.length ) {
                  
                  switch( this.selectedOption ) {
                      case 'Accounts':
                        return this.matchedAccounts[0].map( item => item.AccountName );
                      case 'Properties':
                        const search = this.matchedAccounts[0].map( item => item.Name );
                        const regex = new RegExp( this.searchTerm, 'gi' );
                        return search.filter( prop => prop.match( regex ) );
                  }
                }
            }
        }
    };
</script>

<style lang="scss">

.search-wrapper {
    display: flex;
    justify-content: space-between;
    padding: 10px 10px 0;
}
.text-input-wrapper {
    width: 83%;
    position: relative;
    
    &__dropdown {
        max-height: 50px;
        @extend .search-input-base;
        text-transform: uppercase;
    }
    &__search-input {
        display: inline-block;
        overflow: hidden;
        width: 100%;
        height: 50px;
        @extend .search-input-base;
    }
    &__search-results {
        position: absolute; 
        top: 10px;
        display: none;
    }
    &__matches {
        margin-bottom: 0;
        background: #FFF;
        border-radius: 4px;
        position: relative;
        bottom: 14px;
        
        li:last-of-type {
            border-bottom-right-radius: 4px;
            border-bottom-left-radius: 4px;
        }
    }
}
    
.search-submit {
    @extend .search-input-base;
    color: #FFF;
    cursor: pointer;
    text-transform: uppercase;
    background: $primaryGreen;
    max-height: 50px;
    &:hover {
        background: lighten( $primaryGreen, 10% );
    }
}

@media screen and ( max-width: 700px ) {
    .search-wrapper {
        display: block;
    }
    .text-input-wrapper {
        width: 100%;
        
        &__dropdown {
            flex-grow: 1;
            margin-left: 0;
            margin-top: 10px;
        }
    }
}
@media screen and ( max-width: 600px ) {
    .search-submit {
        width: 40%;
    }
}
</style>