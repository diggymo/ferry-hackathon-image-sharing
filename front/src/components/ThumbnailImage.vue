<template>
  <div>
    <img :src="src" @load="$emit('loaded')">
  </div>
</template>

<script>
export default {
  name: 'ThumbnailImage',
  props: {
    src: {
      type: String,
      default: "http://placehold.jp/300x500.png"
    }
  }
}
</script>