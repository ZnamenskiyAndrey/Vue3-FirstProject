<template>
<div class="dialog" v-if="show" @click="hideDialog">
    <div @click.stop class="dialog__content">
        <slot></slot>
    </div>
</div>
</template>

<script>
    export default {
        props: {
            show: Boolean,
            default: false
        },
        methods:{
        hideDialog() {
            this.$emit('update:show', false)
        }
    }
    }
</script>

<style scoped>
.dialog{
    position: fixed;
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
    background: rgba(0, 0, 0, 0.5);
    display: flex;
     
}
.dialog__content {
    margin: auto;
    background-color: #fff;
    border-radius: 15px;
    min-height: 100px;
    min-width: 300px;
    padding: 20px 30px;
}
</style>