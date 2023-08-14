<template>
  <div class="app">
    <div class="add-post">
      <h1 class="post-title">Post's Page</h1>
      <div class="btns">
        <Button @click="showModal">Create Post</Button>
        <MySelect @update:modelValue="changeOption" :options="sortOptions"></MySelect>
      </div>
      <Input v-model="seacrhQuery" placeholder="Search Posts"></Input>
    </div>
    <MyDialog v-model:show="isShow">
      <PostForm @create="addPost" />
    </MyDialog>
    <PostList :posts="seacrhAndSortPosts" @remove="delItem" v-if="!postsLoading"/>
    <div class="lds-roller" v-else><div></div><div></div><div></div><div></div><div></div><div></div><div></div><div></div></div>
  </div>
  <div class="pages">
    <div v-for="page in totalPages" :key="page">{{ page }}</div>
  </div>
</template>

<script>
import PostList from '@/components/PostList.vue'
import PostForm from '@/components/PostForm.vue'
import axios from 'axios'

export default {
  name:"AppComponent",
  components: {
    PostList, PostForm
   
    
  },

  data() {
    return {
      posts: [],
      isShow: false,
      modificatorValue:'',
      postsLoading: false,
      selectedSort: "",
      sortOptions: [
        {value: "title", name:"By Title"},
        {value:"body", name:"By Description"}
      ],
      seacrhQuery:'',
      page: 1,
      limit: 10,
      totalPages: 0
    }

  },
  methods: {
    addPost(post) {
      this.posts.push(post)
      this.isShow = false
    },
    delItem(post) {
      this.posts = this.posts.filter(el => el.id !== post.id)
    },
    showModal() {
      this.isShow = !this.isShow
    },
   async fetchPosts() {
      try {
        this.postsLoading = true;
        setTimeout(async ()=> {
          const {data:postsData,headers:headers} = await axios.get("https://jsonplaceholder.typicode.com/posts", {
            params: {
              _page: this.page,
              _limit: this.limit
            }
            
          })
          // console.log(headers['x-total-count'])
          // this.totalPages = Math.ceil(headers['x-total.count']/ this.limit)
          this.posts = postsData
          console.log(postsData)
        this.postsLoading = false
        },1000)
      
      } catch(e) {
        alert("Somehthing went wrong")
      } 
    },
    changeOption(value){
      // console.log(value);
      this.selectedSort = value

    },
   
  },
  mounted() {
      this.fetchPosts();

    },
  computed: {
    sortedPosts() {
      return [...this.posts].sort((a,b)=> {
        return(a[this.selectedSort] > b[this.selectedSort]? 1 : -1)
      })
    },
    seacrhAndSortPosts(){
      return this.sortedPosts.filter(post => post.title.toLowerCase().includes(this.seacrhQuery.toLowerCase()))
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.add-post {
  display: flex;
  flex-direction: column;
  gap:30px;
  align-items: center;
  max-width: 300px;
  width: 100%;
  margin: 20px auto
}

.lds-roller {
  display: inline-block;
  position: relative;
  width: 80px;
  height: 80px;
}
.lds-roller div {
  animation: lds-roller 1.2s cubic-bezier(0.5, 0, 0.5, 1) infinite;
  transform-origin: 40px 40px;
}
.lds-roller div:after {
  content: " ";
  display: block;
  position: absolute;
  width: 7px;
  height: 7px;
  border-radius: 50%;
  background: #000;
  margin: -4px 0 0 -4px;
}
.lds-roller div:nth-child(1) {
  animation-delay: -0.036s;
}
.lds-roller div:nth-child(1):after {
  top: 63px;
  left: 63px;
}
.lds-roller div:nth-child(2) {
  animation-delay: -0.072s;
}
.lds-roller div:nth-child(2):after {
  top: 68px;
  left: 56px;
}
.lds-roller div:nth-child(3) {
  animation-delay: -0.108s;
}
.lds-roller div:nth-child(3):after {
  top: 71px;
  left: 48px;
}
.lds-roller div:nth-child(4) {
  animation-delay: -0.144s;
}
.lds-roller div:nth-child(4):after {
  top: 72px;
  left: 40px;
}
.lds-roller div:nth-child(5) {
  animation-delay: -0.18s;
}
.lds-roller div:nth-child(5):after {
  top: 71px;
  left: 32px;
}
.lds-roller div:nth-child(6) {
  animation-delay: -0.216s;
}
.lds-roller div:nth-child(6):after {
  top: 68px;
  left: 24px;
}
.lds-roller div:nth-child(7) {
  animation-delay: -0.252s;
}
.lds-roller div:nth-child(7):after {
  top: 63px;
  left: 17px;
}
.lds-roller div:nth-child(8) {
  animation-delay: -0.288s;
}
.lds-roller div:nth-child(8):after {
  top: 56px;
  left: 12px;
}
@keyframes lds-roller {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

.btns {
  min-width: 500px;
  width: 100%;
  display: flex;
  flex-direction: row;
  justify-content: space-around;
}
</style>