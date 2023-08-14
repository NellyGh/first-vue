<template>
  <div class="post">
    <div class="close" @click="$emit('remove', post)">
      <svg width="14" height="14" viewBox="0 0 14 14" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path d="M14 1.41L12.59 0L7 5.59L1.41 0L0 1.41L5.59 7L0 12.59L1.41 14L7 8.41L12.59 14L14 12.59L8.41 7L14 1.41Z"
          fill="black" fillOpacity="0.7" />
      </svg>
    </div>
    <div class="title"><strong>Name: </strong> {{ post.title }}</div>
    <div class="body"><strong>Description: </strong>{{ post.body }}</div>
  </div>
</template>

<script>
export default {
  props: {
    post: {
      type: Object,
      required: true
    }

  }
}
</script>

<style lang="scss" scoped></style>