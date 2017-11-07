<template>
    <div>
        
        <div class="search-wrapper">
            <div class="text-input-wrapper">
                <input @keyup="findAccountMatch" v-model="searchTerm" class="text-input-wrapper__search-input" type="search" placeholder="Search for an account" />
                <span class="text-input-wrapper__search-results">1 Result</span>
                <!-- Hide and Show Dropdown based on user input -->
                <ul v-show="searchTerm.length" class="text-input-wrapper__matches account-list">
                    <li class="account-list__item" v-for="match in matchedAccountNames">
                        {{ match }}
                    </li>
                </ul>
            </div>
            
            <button @click="findAccountMatch()" class="search-submit">Search</button>
        </div>
    
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
    padding: 10px;
}
.text-input-wrapper {
    width: 75%;
    position: relative;
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
    width: 22%;
    max-height: 50px;
    &:hover {
        background: lighten( $primaryGreen, 10% );
    }
}

/*.activeSearch {*/
/*  right: 40px;*/
/*  display: inline;*/
/*  transition: .3s ease-in;*/
/*:class="{ activeSearch: this.searchTerm.length > 2 }"*/
/*}*/
</style>