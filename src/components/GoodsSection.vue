<template>
    <section>
        <div class="heading-block">
            <h1>Добавление товара</h1>
            <div class="select-background">
                <select name="filter" id="" v-model="selected">
                    <option value="default">По умолчанию</option>
                    <option value="min">По возрастанию</option>
                    <option value="max">По убыванию</option>
                </select>
            </div>
        </div>
        
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
                selected: "default",
                goodsToRender: this.goods,

            };
        },
        watch: {
            selected(newSlectedValue) {
                // console.log(oldSelectedValue);
                if(newSlectedValue === 'default') {
                    // return this.goodsToRender;
                    this.filterName(this.goodsToRender);
                }
                if(newSlectedValue === 'min') {
                    this.filterMinToMax(this.goodsToRender);
                }
                if(newSlectedValue === 'max') {
                    this.filterMaxToMin(this.goodsToRender);
                }
            }
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
            },
            filterMinToMax (array) {
                return array.sort((a, b) => {
                    return a.price - b.price;
                });
            },
            filterMaxToMin(array) {
                return array.sort((a, b) => {
                    return b.price - a.price;
                });
            }, 
            filterName(array) {
                return array.sort((a, b) => {
                    let aString = a.name;
                    let bString = b.name;
                    return aString === bString ? 0 : aString > bString ? 1 : -1;
                    // return a.name.toUpperCase() - b.name.toUpperCase();
                });
            }
        },
        components: {
            GoodComponent,
            ListComp,
            ListElement,
            FormComp,
        },
        // mounted() {
            
        // }
    } 
</script>

<style scoped>
    @import url("https://fonts.googleapis.com/css2?family=Source+Sans+Pro:wght@400;600;700&display=swap");
    section {
        box-sizing: border-box;
        padding: 32px 36px 0 32px;
        font-family: 'Source Sans Pro', sans-serif;
    }
    div {
        display: flex;
        justify-content: space-between;
        align-items: flex-start;
    }

    h1 {
        text-align: left;
        font-weight: 600;
        font-size: 28px;
        line-height: 35px;
        /* margin: 32px 0 16px 0; */
        margin: 0;
    }
    .select-background {
        min-width: 120px;
        background: #FFFEFB;
        box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
        border-radius: 4px;
        border: 2px solid transparent;
        overflow: hidden;
        background: url('../assets/arrow-down.png') no-repeat calc(100% - 12px) #fff;
        outline: none;
        cursor: pointer;
    }
    .select-background:focus-within {
        border: 2px solid #acacac;
    }
    select {
        box-sizing: border-box;
        padding: 0 0px;
        appearance: none;
        -webkit-appearance: none;
        -moz-appearance: none;
        background: transparent;
        font-weight: 400;
        font-size: 12px;
        line-height: 15px;
        color: #B4B4B4;
        border: none;
        min-height: 36px;
        width: 100%;
        box-sizing: border-box;
        padding: 0 16px;
        cursor: pointer;
        outline: none;
    }

    .heading-block {
        margin: 0 0 16px 0;
    }
</style>