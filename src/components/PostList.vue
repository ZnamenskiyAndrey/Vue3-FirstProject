<template>
    <div v-if="posts.length > 0">
        <h3>Список постов</h3>
        <TransitionGroup name="posts-list">
             <post-item
            v-for="post in posts"
            :post="post"
            :key="post.id"
            @remove="$emit('remove', post)"
        />
        </TransitionGroup>
    </div>
    <h2 v-else class="danger">Список постов пуст</h2>
</template>

<script>
import PostItem from './PostItem.vue';

export default {
    components: { 
        PostItem 
    },
    props: {
        posts: {
            type: Array,
            required: true
        }
    },
}
</script>

<style scoped>
    .danger{
        color: red;
        font-size: 30px;
    }
    .posts-list-item {
        display: inline-block;
        margin-right: 10px;
      }
      .posts-list-enter-active,
      .posts-list-leave-active {
        transition: all 0.5s ease-in-out;
      }
      .posts-list-enter-from,
      .posts-list-leave-to {
        opacity: 0;
        transform: rotate(90deg);
      }
      .posts-list-move {
        transition: transform 0.5s ease;
      }
</style>