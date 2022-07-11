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
                if(this.name === 'price') {
                    // console.log(evt.target.value.length);
                    // if(evt.target.value.length >= 2) {
                    //     console.log(evt.target.value.slice(0, 2));
                    // }
                    if(evt.target.value.length >= 2) {
                        // console.log('yes');
                        evt.target.value.replace(evt.target.value, `${evt.target.value.slice(0,2)}`);
                    }
                }
                this.$emit('update:modelValue', evt.target.value, evt.target.name, evt.target.validity.valid);
            },
        }
    }
</script>
