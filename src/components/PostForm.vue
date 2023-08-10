<template>
    <form 
    @submit.prevent 
    class="form"
    >
        <h2 class="form__title">Создание поста</h2>
        <label for="">

            <myInput
            v-model="post.title"
            type="text"
            placeholder="Название"
            />
            <myInput
            v-model="post.body"
            type="text"
            placeholder="Описание"
            />
     
        <standart-button 
            @click="createPost"
        >
        Создать
        </standart-button>
      </label>
      </form>
</template>

<script>
import standartButton from "./UI/standart-button.vue";
import myInput from './UI/myInput.vue';

export default {
    components: {
        standartButton,
        myInput,
    },
    data(){
        return {
            post: {
                title:'',
                body: '',
            }
        }
    },
    methods:{
        createPost() {
            this.post.id = Date.now();
            this.$emit('create', this.post)
            this.post = {
                 title: '',
                 body: ''
            }
        }
    },
    // watch: {
    //     post: {
    //         handler(newVal) {
    //             console.log(newVal)
    //         },
    //         deep: true
    //     }
    // }
}
</script>

<style>


</style>