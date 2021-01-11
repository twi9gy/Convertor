<template>
    <b-dropdown-item v-on:click="$emit('change_unit', [unit, type])">{{unit}}</b-dropdown-item>
</template>

<script>
    export default {
        name: "Item_unit",
        props: ['unit', 'type']
    }
</script>

<style scoped>

</style>
