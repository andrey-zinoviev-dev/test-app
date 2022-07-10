<template>
    <form novalidate>
        <div>
            <span class="required">Наименование товара</span>
            <InputComp @update:modelValue="this.checkForm" v-model="goodName" :type="'text'" :placeholder="'Введите наименование товара'" :name="'name'" :required="'required'"></InputComp>
            <!-- <input type="text" placeholder="Введите наименование товара" name="name" required /> -->
        </div>
        <div>
            <span>Описание товара</span>
            <textarea name="description" id="" cols="30" rows="10" placeholder="Введите описание товара"></textarea>
        </div>
        <div>
            <span class="required">Ссылка на изображение товара</span>
            <InputComp @update:modelValue="this.checkForm" v-model="url" :type="'text'" :placeholder="'Введите ссылку'" :name="'url'" :required="''"></InputComp>
            <!-- <input type="text" name="url" id="" required placeholder="Введите ссылку"> -->
        </div>
        <div>
            <span class="required">Цена товара</span>
            <InputComp @update:modelValue="this.checkForm" v-model="price" :type="'string'" :placeholder="'Введите цену'" :name="'price'" :required="'required'"></InputComp>
            <!-- <input type="number" name="price" id="" placeholder="Введите цену"> -->
        </div>
        <button type="submit" :disabled="this.disabled" @click.prevent="this.addGood(this.objectToSend)" :class="{ disabled: this.disabled }">Добавить товар</button>
    </form>
</template>

<script>
    import InputComp from './InputComp.vue'
    export default {
        name: 'FormComp',
        data() {
            return {
                objectToSend: {},
                goodName: null,
                goodNameVailid: false,
                goodDescription: null,
                goodDescriptionValid: false,
                url: null,
                urlValid: false,
                price: null,
                priceValid: false,
                disabled: true,
            }
        },
        components: {
            InputComp,
        },
        methods: {
            checkForm(inputValue, inputName, inputValidity) {
                this.objectToSend[inputName] = inputValue;
                if(inputName === 'name') {
                    this.goodNameVailid = inputValidity;
                }

                if(inputName === 'url') {
                    this.goodDescriptionValid = inputValidity;
                }

                if(inputName === 'price') {
                    this.priceValid = inputValidity;
                }

                if(this.goodNameVailid && this.goodDescriptionValid && this.priceValid) {
                    return this.disabled = false;
                }
                
                return this.disabled = true;  
            },
            addGood(object) {
                return this.$emit('addGood', object);
            }
            
        }
    }
</script>

<style scoped>
    form {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: flex-start;
        min-width: 332px;
        min-height: 440px;
        background: #FFFEFB;
        box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
        border-radius: 4px;
        margin: 0 16px 0 0;
    }
    div {
        display: flex;
        flex-direction: column;
        align-items: flex-start;
        margin-bottom: 16px;
    }
    div:last-of-type {
        margin-bottom: 24px;
    }
    .required::after {
        content:'';
        background: #FF8484;
        border-radius: 4px;
        min-height: 4px;
        min-width: 4px;
        position: absolute;
        top: 0;
        right: -5px;
    }
    input, textarea, button {
        min-width: 284px;
        box-sizing: border-box;
    }
    input, textarea {
        background: #FFFEFB;
        box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
        border-radius: 4px;
        border: none;
    }
    input, button {
        min-height: 36px;
    }
    textarea {
        max-height: 108px;
    }
    span {
        font-size: 12px;
        line-height: 13px;
        letter-spacing: -0.02em;
        margin-bottom: 4px;
        position: relative;
    }
    button {
        border-radius: 10px;
        background: #7BAE73;
        box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
        font-weight: 600;
        font-size: 12px;
        line-height: 15px;
        color: #FFFFFF;
        /* margin-top: 24px; */
    }
    .disabled {
        color: #B4B4B4;
        background: #EEEEEE;
        box-shadow: none;
    }
</style>