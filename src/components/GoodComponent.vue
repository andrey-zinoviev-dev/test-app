<template>
    <article @mouseover="this.hoverGood" @mouseleave="this.unhoverGood">
        <button  @click="this.deleteGood(good)" :class="{isHovered: this.isHovered}">
            <img :src="require('../assets/delete.svg')" alt="">
        </button>
        <img class="good-pic" :src="good.pic" alt="">
        <div>
            <h3>{{good.name}}</h3>
            <p>{{good.description}}</p>
            <span>{{good.price}}</span><span> руб.</span>
        </div>
    </article>
</template>

<script>
    // import deleteSvg from '../assets/delete.svg';

    export default {
        data() {
            return {
                isHovered: false,
            }
        },
        props: {
            good: Object,
        },
        methods: {
            deleteGood(good) {
                this.$emit('deleteGood', good);
            },
            hoverGood() {
                this.isHovered = true;
            },
            unhoverGood() {
                this.isHovered = false;
            },
        },
        emits: ['deleteGood'],
    };
</script>

<style scoped>
    article {
        position: relative;
        background: #FFFEFB;
        box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
        border-radius: 4px;
        height: 100%;
        cursor: pointer;
        border: 2px solid transparent;
        transition: border 0.35s ease-in-out, box-shadow 0.35s ease-in-out 0.01s;
        display: flex;
        flex-direction: column;
        /* overflow: hidden; */
        /* text-align: left; */
    }
    article:hover {
        border: 2px solid #acacac;
        box-shadow: 0 20px 30px #d95e5e, 0 6px 10px #d95e5e;
    }
    .good-pic {
        max-width: 332px;
        max-height: 200px;
        min-height: 200px;
        object-fit: cover;
        border-radius: 4px 4px 0 0;
    }
    button {
        position: absolute;
        top: -2%;
        right: -2%;
        background-color: #FF8484;
        min-width: 32px;
        min-height: 32px;
        box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
        border-radius: 10px;
        border: none;
        cursor: pointer;
        visibility: hidden;
        opacity: 0;
    }
    .isHovered {
        visibility: visible;
        opacity: 1;
    }
    div {
        box-sizing: border-box;
        padding: 0 16px;
        text-align: left;
    }
    h3 {
        font-weight: 600;
        font-size: 20px;
        line-height: 25px;
        margin: 16px 0;
    }
    p {
        font-weight: 400;
        font-size: 16px;
        line-height: 20px;
        margin: 0 0 32px 0;
        min-height: 80px;
        max-height: 80px;
        overflow-y: auto;
    }
    span {
        font-weight: 600;
        font-size: 24px;
        line-height: 30px;
    }
</style>