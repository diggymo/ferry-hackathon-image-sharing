<template>
  <div class="image-wrapper image-radius">
    <img :src="image.image" @load="$emit('loaded')" class="image-radius">
    <small style="margin-bottom: 6px;">{{ image.spot.name }}</small>
    <!-- <small>{{ image.spot.name }}</small> -->
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
  }
}
</script>

<style scped>
.image-wrapper {
  position: relative;
}
.image-wrapper small{
	position: absolute;
	left: 0;
	bottom: 0;
  color: #fff;
  height: 2rem;
  line-height: 2rem;
	margin: 0;
  width: 100%;
	background: linear-gradient(rgba(0,0,0,0), rgba(0,0,0,0.8));
	filter: Alpha(opacity=70);
	opacity: 0.7;
  border-radius: 0 0 8px 8px;
}

.image-wrapper img {
  box-shadow: 0px 0px 5px 5px rgba(0,0,0,0.15);
}
</style>
