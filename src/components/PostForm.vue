<template>
  <div class="form" @submit.prevent>
    <form action="#">
      <Input type="text" v-model="post.title" placeholder="Post Title"></Input>
      <Input type="text" v-model="post.body" placeholder="Post Description"></Input>
      <Button type="submit" @click="addPost">Add new Post</Button>
    </form>
  </div>
</template>

<script>


export default {

  data() {
    return {
      post: {
        title: '',
        body: ''
      }
    }
  },
  methods: {
    addPost() {
      this.post.id = new Date().getTime().toString()
      this.$emit('create', this.post)
      this.post = {
        title: '',
        body: ""
      }

    }
  }
}
</script>

<style>
.form {
  margin-top: 50px;
}

form {
  display: flex;
  flex-direction: column;
  max-width: 400px;
  width: 100%;
  gap: 20px;
  margin: 0 auto;
  align-items: center;
}
</style>