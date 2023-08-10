<template>
    <input
        v-bind:modelValue="modelValue"
        @input="updateInput"
        class="form__input"
        type="text" 
    >
</template>

<script>

export default {
    props: {
        modelValue: [String, Number]
    },
    methods: {
        updateInput(event) {
            this.$emit('update:modelValue', event.target.value)
        }
    }
}
</script>

<style>
.form__input {
    width: 100%;
    border-color: navy;
    border-radius: 3px;
    padding: 10px 20px;
    font-size: 16px;
    margin: 15px 0;
  }
</style>