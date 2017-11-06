<template>
    <div>
        
        <div class="search-wrapper">
            <div class="text-input-wrapper">
                <input v-model="searchTerm" class="search-input" type="search" placeholder="Search for an account" />
                <span class="search-results" :class="{ activeSearch: this.searchTerm.length > 2 }">1 Result</span>
            </div>
            <button @click="searchAccounts()" class="search-submit">Search</button>
        </div>
    
    </div>
</template>

<script>
    export default {
        name: 'AccountSearch',
        data() {
            return {
                searchTerm: '',
                userInput: false
            }
        },
        methods: {
            searchAccounts() {
                console.log( this.searchTerm );
            }
        }
    };
</script>

<style lang="scss">

.search-wrapper {
    display: flex;
    justify-content: space-between;
    padding: 10px;
    .text-input-wrapper {
        width: 75%;
        position: relative;
        .search-input {
            display: inline-block;
            overflow: hidden;
            width: 100%;
            @extend .search-input-base;
        }
        .search-results {
            position: absolute; 
            top: 10px;
            display: none;
        }
        .activeSearch {
          right: 40px;
          display: inline;
          transition: .3s ease-in;
        }
    }
    
    .search-submit {
        @extend .search-input-base;
        color: #FFF;
        cursor: pointer;
        text-transform: uppercase;
        background: $primaryGreen;
        width: 22%;
        &:hover {
            background: lighten( $primaryGreen, 10% );
        }
    }
}
</style>