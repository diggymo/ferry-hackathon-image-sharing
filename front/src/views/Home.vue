<template>
  <div>
    <nav class="navbar is-fixed-top is-primary" role="navigation" aria-label="main navigation">
      <div class="navbar-brand">
        <div class="navbar-item"><h3><b>さんふらわぁの旅</b>&nbsp;&nbsp;&nbsp;<small>aaaa年xx月yy日からbbbb年ii月jj日</small></h3></div>
      </div>
    </nav>
    <section class="section">
      <div class="container">
        <div id="grid">
          <div v-for="image in images" :key="image.src"  class="grid-item image-radius" :style="{width: columnWidth + 'px'}" >
            <thumbnail-image :image="image" @loaded="onLoaded" @click.native="onClickImage(image)" class="image-radius"/>
          </div>
          <div class="grid-item image-radius" :style="{width: columnWidth + 'px'}" >
            <thumbnail-image :image="sunFlowerImage" @loaded="onLoaded" @click.native="onClickFerryThumbnail" class="image-radius"/>
          </div>
        </div>
      </div>
    </section>
    <image-card :image="selectedImage" @close="onCloseModal"/>
  </div>
</template>

<script>
import thumbnailImage from "@/components/ThumbnailImage"
import imageCard from "@/components/ImageCard"

import Masonry from "masonry-layout"

import axios from "axios"

import mockImages from "@/mock/images"

// @ is an alias to /src
/* eslint-disable no-console */
export default {
  name: 'home',
  components: {
    thumbnailImage,
    imageCard
  },
  async mounted() {
    var grid = document.getElementById('grid');

    this.columnWidth = (window.innerWidth - 48 - 10)/2
  
    /* eslint-disable no-unused-vars */
    this.msnry = new Masonry(grid, {
        columnWidth: this.columnWidth,
        gutter: 10,
        itemSelector: '.grid-item',
    });
  },
  async created() {
    /* eslint-disable no-console */
    console.log(window.innerWidth)

    this.columnWidth = window.innerWidth
    
    const spotId = this.$route.params.spot_id
    const qrId = this.$route.query.qrid
    console.log("SPOT", spotId)
    console.log("QR", qrId)
    this.images = mockImages
    this.images = await this.getImages(spotId, qrId)
  },
  data() {
    return {
      msnry: null,
      columnWidth: 500, 
      selectedImage: null,
      sunFlowerImage: {
        image: "/sun_flower.jpg", // 画像URL,
        created_at: "2018-10-10 11:22:33", // 撮影日時。できればほしい笑
        spot: {
          id: 4,
          name: "さんふらわぁ",
          description: "人気の温泉観光地。おどろおどろしい地獄の名が付けられ、柵で囲われたさまざまな湯だまりがある。動物たちも飼育されている。"
        }
      },
      images: []
    }
  },
  watch: {
    images() {
      this.onLoaded()
    }
  },
  methods: {
    onLoaded() {
      // 画像のサイズリセットする
      this.msnry.layout()
    },
    onClickImage(image) {
      this.selectedImage = image
    },
    onCloseModal() {
      this.selectedImage = null
    },
    onClickFerryThumbnail() {
      console.log("SUN_FLOEWR!!!!")
    },
    getImages(spotId, qrId) {
      return axios.get(`/api/hogehoge/?qrid=${qrId}`).then(res => {
        return res.data
      }).catch(err => {
        console.log("NETWORK_ERR", err)
        return mockImages
      })
    }
  }
}
</script>


<style>
.grid-item {
  margin-bottom: 10px;
}

.image-radius {
  border-radius: 8px;
}
</style>
