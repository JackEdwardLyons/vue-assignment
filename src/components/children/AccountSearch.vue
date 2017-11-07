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
                <select class="text-input-wrapper__dropdown">
                    <option>ACCOUNTS</option>
                    <option>PROPERTIES</option>
                </select>
                <button @click="findAccountMatch()" class="search-submit">Search</button>
            </div>
        </div>
        <!-- Account Search -->
    </div>
</template>

<script>
    export default {
        name: 'AccountSearch',
        props: [ 'matchedAccounts' ],
        data() {
            return {
                searchTerm: '',
                userInput: false,
               
            };
        },
        methods: {
            findAccountMatch() {
                this.$emit( 'searched', this.searchTerm );
            },
            clickedAccount( match, key ) {
                console.log('match: ', match, 'key: ', key )
                // Grab only the matching account properties
                const accountNameProps = this.matchedAccounts[0].map( item => item.Properties );
                // Send payload with account name and index for toggling the "selected" class
                this.$emit( 'clicked', accountNameProps[ key ], key );
                // Empty searchTerm for next search
                this.searchTerm = '';
            }
        },
        computed: {
            matchedAccountNames() {
                if ( this.matchedAccounts.length ) {
                   return this.matchedAccounts[0].map( item => item.AccountName ); 
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
    width: 75%;
    position: relative;
    
    &__dropdown {
        max-height: 50px;
        @extend .search-input-base;
        margin: 0 20px;
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
        }
    }
}
@media screen and ( max-width: 600px ) {
    .search-submit {
        width: 40%;
    }
}
</style>