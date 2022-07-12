<template>
    <input :type="type" :placeholder="placeholder" :name="name" :required="required" :value="modelValue" @input="this.sendInputText">
</template>

<script>
    export default {
        name: "InputComp",
        props: {
            type: String,
            placeholder: String,
            required: String,
            name: String,
            modelValue: String,
            updateModelValue: Function,
        },
        methods: {
            sendInputText(evt) {
                // console.log(evt.target.validity);
                if(this.name === 'price') {
                    let matched = evt.target.value.match(/([0-9]{2})([0-9]{3})/);
                    if(matched) {
                        // console.log(matched[1]);
                        evt.target.value = `${matched[1]} ${matched[2]}`;
                    }
                    // if(evt.target.value.length >= 2) {
                    //     evt.target.value.replace(evt.target.value, `${evt.target.value.slice(0,2)}`);
                    // }
                }
                this.$emit('update:modelValue', evt.target.value, evt.target.name, evt.target.validity.valid, evt.target.validity.valueMissing);
            },
        }
    }
</script>
