<template>
    <ul>
        <slot></slot>
    </ul>
</template>

<script>
    export default {
        name: 'ListComp',
    }
</script>

<style>
    ul {
        padding: 0;
        list-style: none;
        margin: 0;
        display: grid;
        grid-template-columns: repeat(3, 1fr);
        grid-gap: 16px;
    }
    @media screen and (max-width: 1439px) {
        ul {
            grid-template-columns: repeat(2 ,1fr);
        }
    }
    @media screen and (max-width: 1100px) {
        ul {
            grid-template-columns: repeat(1, 1fr);
            justify-items: center;
        }
    }
</style>