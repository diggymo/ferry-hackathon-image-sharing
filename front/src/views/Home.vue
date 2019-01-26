<template>
  <div>
    <nav class="navbar is-fixed-top is-primary" role="navigation" aria-label="main navigation">
      <div class="navbar-brand">
        <div class="navbar-item has-text-left"><div><h3><b>さんふらわぁの旅</b><br><small>{{ startDate | formatToDate }}から{{ endDate | formatToDate }}</small></h3></div></div>
      </div>
    </nav>
    <section class="section" id="main-section">
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
import { format } from 'date-fns'

import Masonry from "masonry-layout"

import axios from "axios"

// import mockImages from "@/mock/images"

// @ is an alias to /src
/* eslint-disable no-console */
export default {
  name: 'home',
  components: {
    thumbnailImage,
    imageCard
  },
  mounted() {
    var grid = document.getElementById('grid');

    this.columnWidth = (window.innerWidth - 48 - 10)/2
  
    /* eslint-disable no-unused-vars */
    this.msnry = new Masonry(grid, {
        columnWidth: this.columnWidth,
        gutter: 10,
        itemSelector: '.grid-item',
    });
  },
  computed: {
    startDate() {
      if (this.images.length == 0) {
        return "-----"
      }
      return this.images.slice(0,this.images.length).sort((a,b) => {
        return a.created_at > b.created_at
      })[0].created_at;
    },
    endDate() {
      if (this.images.length == 0) {
        return "-----"
      }
      return this.images.slice(0,this.images.length).sort((a,b) => {
        return a.created_at < b.created_at
      })[0].created_at;
    },
  },
  filters: {
    formatToDate(value) {
      return format(value, "YYYY年M月D日")
    }
  },
  async created() {
    /* eslint-disable no-console */
    console.log(window.innerWidth)

    this.columnWidth = window.innerWidth
    
    const spotId = this.$route.params.spot_id
    const qrId = this.$route.query.qrid
    console.log("SPOT", spotId)
    console.log("QR", qrId)
    // this.images = mockImages
    this.images = await this.getImages(spotId, qrId)
    this.onLoaded()
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
    async getImages(spotId, qrId) {
      if (spotId === undefined || qrId === undefined) {
        // return mockImages
        return []
      }

      console.log(`http://ferry-sunflower.ga/api/hogehoge/?qrid=${qrId}`)
      return axios.get(`http://ferry-sunflower.ga/api/hogehoge/?qrid=${qrId}`).then(res => {
        console.log("hogeee", res.data)
        return res.data
      }).catch(err => {
        console.log("NETWORK_ERR", err)
        // console.log(mockImages)
        // return mockImages
        return []
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

#main-section {
  padding-top: 24px;
  background-image: url("/bg.jpg");
  background-attachment: fixed;
}
</style>
