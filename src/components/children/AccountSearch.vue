<template>
    <div class="search-wrapper">
        <input class="search-input" type="search" placeholder="Search for an account" />
        <button class="search-submit">Search</button>
    </div>
</template>

<script>
    export default {
        name: 'AccountSearch'
    };
</script>

<style lang="scss">
    
    .search-wrapper {
        border: 1px solid yellow;
        display: flex;
        padding: 10px;
        .search-input {
            width: 75%;
            padding: 10px;
        }
        .search-submit {
            width: 25%;
            padding: 10px;
        }
    }
</style>