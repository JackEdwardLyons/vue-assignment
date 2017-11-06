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
    justify-content: space-between;
    padding: 10px;
    .search-input {
        width: 75%;
        @extend .search-input-base;
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