<template>
  <div class="modal" :class="{'is-active': isModalActive}">
    <div class="modal-background" @click="closeModal"></div>
    <div class="modal-content">
      <section class="section" v-if="isModalActive">
        <div class="box">
          <img :src="image.image">
          <h4>{{ image.spot.name }}</h4>
          <h4>{{ image.created_at }}</h4>
          <h4>{{ image.spot.description }}</h4>
          <span class="icon">
            <i class="fas fa-download"></i>
          </span>
          <span class="icon">
            <i class="fas fa-share-alt"></i>            
          </span>
        </div>
      </section>
    </div>
    <button class="modal-close is-large" aria-label="close" @click="closeModal"></button>
  </div>
</template>

<script>
export default {
  name: 'ThumbnailImage',
  props: {
    image: {
      type: Object,
      default: null
    }
  },
  computed: {
    isModalActive() {
      return this.image !== null
    }
  },
  methods: {
    closeModal() {
      this.$emit("close")
    },
  }
}
</script>

<style scoped>
img {
  max-width: 100%;
}

</style>
