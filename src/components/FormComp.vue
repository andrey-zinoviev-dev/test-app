<template>
    <form novalidate @submit.prevent="this.addGood">
        <div class="div-error-span">
            <span class="required">Наименование товара</span>
            <InputComp @update:modelValue="this.checkForm" v-model="goodName" :type="'text'" :placeholder="'Введите наименование товара'" :name="'name'" :required="'required'"></InputComp>
            <span class="span-error">{{this.goodErrorValue}}</span>
        </div>
        <div>
            <span>Описание товара</span>
            <TextAreaComp @update:modelValue="this.checkForm" v-model="goodDescription" :name="'description'"></TextAreaComp>
            <!-- <textarea @update:modelValue="" v-model="goodDescription" name="description" id="" cols="30" rows="10" placeholder="Введите описание товара"></textarea> -->
        </div>
        <div class="div-error-span">
            <span class="required">Ссылка на изображение товара</span>
            <InputComp @update:modelValue="this.checkForm" v-model="url" :type="'text'" :placeholder="'Введите ссылку'" :name="'pic'" :required="''"></InputComp>
            <span class="span-error">{{this.urlErrorValue}}</span>
        </div>
        <div class="div-error-span">
            <span class="required">Цена товара</span>
            <InputComp @update:modelValue="this.checkForm" v-model="price" :type="'string'" :placeholder="'Введите цену'" :name="'price'" :required="'required'"></InputComp>
            <span class="span-error">{{this.priceErrorValue}}</span>
        </div>
        <button type="submit" :disabled="this.disabled" :class="{ disabled: this.disabled }">Добавить товар</button>
    </form>
</template>

<script>
    import InputComp from './InputComp.vue';
    import TextAreaComp from './TextAreaComp.vue';

    export default {
        name: 'FormComp',
        data() {
            return {
                // objectToSend: {},
                goodName: null,
                goodNameVailid: false,
                goodErrorValue:null,
                goodDescription: null,
                goodDescriptionValid: false,
                url: null,
                urlValid: false,
                urlErrorValue: null,
                price: null,
                priceValid: false,
                priceErrorValue: null,
                disabled: true,
            }
        },
        components: {
            InputComp,
            TextAreaComp,
        },
        methods: {
            checkForm(inputValue, inputName, inputValidity, inputError) {
                // const testObject = {};
                // testObject[inputName] = inputValue;

                // this.objectToSend = testObject;
                if(inputName === 'name') {
                    this.goodNameVailid = inputValidity;
                    inputError ? this.goodErrorValue = "Поле является обязательным" : this.goodErrorValue = null;
                }

                if(inputName === 'pic') {
                    this.goodDescriptionValid = inputValidity;
                    inputError ? this.urlErrorValue = "Поле является обязательным" : this.urlErrorValue = null;
                }

                if(inputName === 'price') {
                    this.priceValid = inputValidity;
                    inputError ? this.priceErrorValue = "Поле является обязательным" : this.priceErrorValue = null;
                }

                if(this.goodNameVailid && this.goodDescriptionValid && this.priceValid) {
                    return this.disabled = false;
                }
                
                return this.disabled = true;  
            },
            addGood(evt) {
                const objectToSend = {
                    name: this.goodName,
                    description: this.goodDescription,
                    price: this.price,
                    pic: this.url,
                };
                evt.target.reset();

                this.goodName = null;
                this.goodDescription = null;
                this.url = null;
                this.price = null;
                
                this.disabled = true;

                return this.$emit('addGood', objectToSend);
            }
            
        }
    }
</script>

<style scoped>
    @import url("https://fonts.googleapis.com/css2?family=Source+Sans+Pro:wght@400;600;700&display=swap");

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
    .div-error-span {
        margin: 0 0 8px 0;        
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
        outline: none;
    }
    input::placeholder, textarea::placeholder {
        font-family: 'Source Sans Pro', sans-serif;
    }
    input:focus-within, textarea:focus-within {
        border: 2px solid #acacac;
    }
    
    input {
        padding: 0 0 0 16px;
    }
    input, button {
        min-height: 36px;
    }
    textarea {
        padding: 10px 0 0 16px;
        max-height: 108px;
        resize: none;
        box-sizing: border-box;
    }
    textarea::placeholder {
        padding: 10px 0 0 16px;
    }
    span {
        font-size: 12px;
        line-height: 13px;
        letter-spacing: -0.02em;
        margin-bottom: 4px;
        position: relative;
    }
    .span-error {
        min-height: 10px;
        margin-top: 10px;
        font-weight: 400;
        font-size: 12px;
        line-height: 10px;
        letter-spacing: -0.02em;
        color: #FF8484;
        margin: 8px 0 0 0;
    }
    button {
        border-radius: 10px;
        background: #7BAE73;
        box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
        font-weight: 600;
        font-size: 12px;
        line-height: 15px;
        color: #FFFFFF;
        cursor: pointer;
        /* margin-top: 24px; */
    }
    .disabled {
        color: #B4B4B4;
        background: #EEEEEE;
        box-shadow: none;
    }
    @media screen and (max-width: 1023px) {
        form {
            margin: 0 0 16px 0;
        }
    }
</style>