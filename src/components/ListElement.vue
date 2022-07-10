<template>
    <li>
        <slot></slot>
    </li>
</template>

<script>
    export default {
        name: "ListElement",
    }
</script>

<style>
    li {   
        max-width: 332px;
        min-height: 423px;
    }
</style>