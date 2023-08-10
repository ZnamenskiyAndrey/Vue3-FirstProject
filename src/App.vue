<template>
  <div class="app">
    <h1>Сраница с постами</h1>

    <MyInput
      v-model="searchQiery"
      placeholder="Поиск"
    />
    <div class="app__btns">
      <standart-button
        @click="showDialog"
      >
      Создать пост
      </standart-button> 
      <my-select
      
      v-model="selectedSort"
      :options = "sortOptions"
      /> 
    </div>
  <myDialog v-model:show="dialogVisible">
    <PostForm
      @create="createPost"
    />
  </myDialog>
    <PostList 
    :posts="sortedAndSearchedPosts"
    @remove=removePost
    v-if="!isPostsLoading"
    />
    <div class="spin-wrapper" v-else>
        <div 
        class="spinner"
        >
      </div>
    </div>
  </div>
 

  </template>
  
  <script>
  import mySelect from "./components/UI/mySelect.vue"
  import PostForm from "./components/PostForm.vue"
  import PostList from "./components/PostList.vue"
  import myDialog from "./components/UI/myDialog.vue"
  import standartButton from "./components/UI/standart-button.vue"

  import axios from 'axios'
import MyInput from "./components/UI/myInput.vue"


  export default {
    components: {
    PostList,
    PostForm,
    myDialog,
    standartButton,
    mySelect,
    MyInput
},

    data() {
      return{
        posts:[],
        dialogVisible: false,
        isPostsLoading: false,
        selectedSort: '',
        searchQiery: '',
        sortOptions: [
          {value: 'title', name: 'По названию'},
          {value: 'body', name: 'По содержимому'}
        ]
      }
    },
    methods: {
     createPost(post) {
      this.posts.push(post);
      this.dialogVisible = false;
     },
     removePost(post) {
      this.posts = this.posts.filter(p => p.id !==post.id)
     },
     showDialog() {
      this.dialogVisible = true;
     },
    async fetchPosts() {
      try {
        this.isPostsLoading = true;
        setTimeout(async() => {
           const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10');
          this.posts = response.data;
          this.isPostsLoading = false;
        }, 1000);
         
      } catch(e) {
        alert('Ошибка');
      } 
    },
    
  },
     mounted() {
      this.fetchPosts();
     },
     computed: {
      sortedPosts() {
        return [... this.posts].sort((post1, post2)=> post1[this.selectedSort]?.localeCompare(post2[this.selectedSort])
           )
      },
      sortedAndSearchedPosts() {
        return this.sortedPosts.filter(post => post.title.includes(this.searchQiery))
        return this.sortedPosts.filter(post => post.body.includes(this.searchQiery))
      }
     },
     watch: {
        // selectedSort(newValue) {
        //    this.posts.sort((post1, post2)=> {
        //     return post1[newValue]?.localeCompare(post2[newValue])
        //    })
        // }
    }
}
  </script>
  
  <style>
  *{
    box-sizing: border-box;
  }
  .app{
    padding: 15px;
  }
  .spin-wrapper{
    position: relative;

  
    .spinner{
      position: absolute;
      height: 60px;
      width: 60px;
      border: 3px solid transparent;
      border-top-color: #A04668;
      top: 50%;
      left: 50%;
      margin: -30px;
      border-radius: 50%;
      animation: spin 2s linear infinite;
      
      &:before, &:after{
        content:'';
        position: absolute;
        border: 3px solid transparent;
        border-radius: 50%;
      }
      
      &:before{
        border-top-color: #254E70;
        top: -12px;
        left: -12px;
        right: -12px;
        bottom: -12px;
        animation: spin 3s linear infinite;
      }
      
      &:after{
        border-top-color: #000;
        top: 6px;
        left: 6px;
        right: 6px;
        bottom: 6px;  
        animation: spin 4s linear infinite;
      }
    }
  }
  
  @keyframes spin{
    0% {transform: rotate(0deg);}
    100% {transform: rotate(360deg);}
  }

  .app__btns {
    display: flex;
    justify-content: space-between;
  }
  </style>