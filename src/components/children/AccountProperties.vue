<template>
    <div class="account-list-wrapper">
        <h1>Properties</h1>
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
        props: [ 'selectedAccount' ],
        data() {
            return { };
        },
        computed: {
            selectedAccountProps() {
                return this.selectedAccount.map( account => account.Name );
            }
        }
    };
</script>

<style lang="scss">

</style>