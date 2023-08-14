<template>
  <div v-if="posts.length > 0">
    <transition-group name="list">
      <PostItem v-for="post in posts" :post='post' :key="post.id" @remove="$emit('remove', post)" />
    </transition-group>
  </div>
  <h2 class="no-post" v-else>Please Add Some Post</h2>
</template>

<script>
import PostItem from '@/components/PostItem.vue'
export default {
  components: {
    PostItem
  },

  props: {
    posts: {
      type: Array,
      required: true
    }
  }


}
</script>

<style >
.post {
  max-width: 800px;
  width: 100%;
  margin: 70px auto;
  border: 2px solid green;
  margin-top: 15px;
  position: relative
}

.title,
.body {
  border: 1px solid yellow;
  max-width: 200px;
  width: 100%;
  margin: 30px auto;
  text-align: center;
  padding: 8px;
  font-size: 17px;
}

.body {
  max-width: 400px;
  width: 100%;
}

.close {
  position: absolute;
  top: 0;
  right: 0;
  padding: 20px;
  cursor: pointer
}

.no-post {
  text-align: center;
  margin-top: 40px;
  color: teal
}

.list-enter-active,
.list-leave-active {
  transition: opacity 0.5s ease;
}

.list-enter-from,
.list-leave-to {
  opacity: 0;
}
</style>