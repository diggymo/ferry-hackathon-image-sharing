<template>
  <div class="modal" :class="{'is-active': isModalActive}">
    <div class="modal-background" @click="closeModal"></div>
    <div class="modal-content">
      <section class="section" v-if="isModalActive">
        <div class="box">
          <img :src="image.image">
          <p class="title is-4 has-text-left is-marginless">{{ image.spot.name }}</p>
          <p class="subtitle is-6 has-text-left is-marginless has-text-secondary">{{ image.created_at }}</p>
          <h4 class="has-text-left has-text-secondary" style="margin-bottom: 1rem;">{{ image.spot.description }}</h4>
          <a :href="image.image" target="_blank" class="is-pulled-left" >
            <span class="icon is-medium">
              <i class="fas fa-2x fa-download"></i>
            </span>
          </a>
          <a class="is-pulled-right" :href="sharingUrl">
            <span class="icon  is-medium">
              <i class="fas fa-2x fa-share-alt"></i> 
            </span>
          </a>
          <div class="is-clearfix"/>
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
  data() {
    return {
      sharingUrl: "https://twitter.com/intent/tweet?text=&hashtags=ferry_hack"
    }
  },
  computed: {
    isModalActive() {
      return this.image !== null
    },
  },
  methods: {
    closeModal() {
      this.$emit("close")
    }
  }
}
</script>

<style scoped>
img {
  width: 100%;
}

</style>
