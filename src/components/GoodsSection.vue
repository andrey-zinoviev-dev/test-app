<template>
    <section>
        <h1>Добавление товара</h1>
        <div>
            <FormComp @addGood="this.addGood"></FormComp>
            <ListComp>
                <ListElement v-for="(good, index) in goods" :key="index">
                    <GoodComponent :good="good" @deleteGood="this.deleteGood"></GoodComponent>
                </ListElement>
            </ListComp>
        </div>
    </section>
</template>

<script>
    import ListComp from './ListComp.vue';
    import ListElement from './ListElement.vue';
    import GoodComponent from './GoodComponent.vue';
    import FormComp from './FormComp.vue';
    export default {
        name: "GoodsSection",
        data() {
            return {
                goodsToRender: this.goods,
            };
        },
        props: {
            goods: Array,
        },
        emits: ['deleteGood', 'addGood'],
        methods: {
            deleteGood(good) {
                this.$emit('deleteGood', good);
            },
            addGood(good) {
                this.$emit('addGood', good);
            }
        },
        components: {
            GoodComponent,
            ListComp,
            ListElement,
            FormComp,
        },
        mounted() {

        }
    } 
</script>

<style scoped>
    section {
        box-sizing: border-box;
        padding: 0 36px;
    }
    div {
        display: flex;
        justify-content: space-between;
        align-items: flex-start;
    }
    h1 {
        text-align: left;
    }
</style>