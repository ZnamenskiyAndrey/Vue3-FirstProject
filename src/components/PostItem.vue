<template>
    <div class="post">
        <div>
            <div><strong>Название: </strong>{{ post.title }}</div>
            <div><strong>Описание: </strong>{{ post.body }}</div>
        </div>
        <div class="post-btns">
            <standart-button
            @click="$emit('remove', post)"
            >
            Удалить
            </standart-button>
        </div>
    </div>
</template>

<script>
import standartButton from './UI/standart-button.vue';
    export default {
        components: {
            standartButton,
        },
        props: {
            post: {
                tupe: Object,
                required: true,
            }

        }
    }
</script>

<style scoped>
.post {
    padding: 10px 15px;
    border: 2px solid navy;
    font-size: 20px;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  .post:not(:last-child) {
    margin-bottom: 20px;
  }
</style>