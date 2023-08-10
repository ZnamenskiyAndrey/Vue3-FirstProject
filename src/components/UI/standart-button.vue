<template>
<button class="btn">
  <slot></slot>  
</button>
</template>

<script>
 name:'standart-button'
</script>

<style scoped>
.btn {
    padding: 10px 15px;
    color: white;
    border-color: navy;
    border-radius: 3px;
    font-weight: 700;
    background: navy;
  }
</style>