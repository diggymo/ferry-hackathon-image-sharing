<template>
  <div>
    <nav class="navbar  is-fixed-top" role="navigation" aria-label="main navigation">
      <div class="navbar-brand">
        <div class="navbar-item"><h3><b>さんふらわぁの旅</b>&nbsp;&nbsp;&nbsp;<small>aaaa年xx月yy日からbbbb年ii月jj日</small></h3></div>
      </div>
      <div class="navbar-end">
        <!-- <div class="navbar-item"><h3><b>さんふらわぁの旅</b></h3></div> -->
        <!-- <a class="navbar-item" href="https://bulma.io">
          <img src="https://bulma.io/images/bulma-logo.png" width="112" height="28">
        </a> -->

        <!-- <a role="button" class="navbar-burger burger" aria-label="menu" aria-expanded="false" data-target="navbarBasicExample">
          <span aria-hidden="true"></span>
          <span aria-hidden="true"></span>
          <span aria-hidden="true"></span>
        </a> -->
      </div>

      <div id="navbarBasicExample" class="navbar-menu">
        <div class="navbar-start">
          <a class="navbar-item">
            Home
          </a>

          <a class="navbar-item">
            Documentation
          </a>

          <div class="navbar-item has-dropdown is-hoverable">
            <a class="navbar-link">
              More
            </a>

            <div class="navbar-dropdown">
              <a class="navbar-item">
                About
              </a>
              <a class="navbar-item">
                Jobs
              </a>
              <a class="navbar-item">
                Contact
              </a>
              <hr class="navbar-divider">
              <a class="navbar-item">
                Report an issue
              </a>
            </div>
          </div>
        </div>

        <div class="navbar-end">
          <div class="navbar-item">
            <div class="buttons">
              <a class="button is-primary">
                <strong>Sign up</strong>
              </a>
              <a class="button is-light">
                Log in
              </a>
            </div>
          </div>
        </div>
      </div>
    </nav>
    <!-- <section class="hero is-primary">
      <div class="hero-body">
        <div class="container">
          <h1 class="title">
            さんふらわぁの旅
          </h1>
          <h2 class="subtitle">
            Primary subtitle
          </h2>
        </div>
      </div>
    </section> -->
    <section class="section">
      <div class="container">
        <div id="grid">
          <div v-for="image in images" :key="image.src"  class="grid-item image-radius" style="background-color: red;" :style="{width: columnWidth + 'px'}" >
            <thumbnail-image :image="image" @loaded="onLoaded" @click.native="onClickImage(image)" class="image-radius"/>
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

// @ is an alias to /src
export default {
  name: 'home',
  components: {
    thumbnailImage,
    imageCard
  },
  mounted() {
    // init with selector

    var grid = document.getElementById('grid');

    this.columnWidth = (window.innerWidth - 48 - 10)/2
  
    /* eslint-disable no-unused-vars */
    this.msnry = new Masonry(grid, {
        columnWidth: this.columnWidth,
        gutter: 10,
        itemSelector: '.grid-item',
    });
  },
  created() {
    /* eslint-disable no-console */
    console.log(window.innerWidth)

    this.columnWidth = window.innerWidth
  },
  data() {
    return {
      msnry: null,
      columnWidth: 500, 
      selectedImage: null,
      images: [
        {
          image: "http://placehold.jp/300x500.png", // 画像URL,
          created_at: "2018-10-10 11:22:33", // 撮影日時。できればほしい笑
          spot: {
            id: 4,
            name: "別府地獄巡り",
            description: "人気の温泉観光地。おどろおどろしい地獄の名が付けられ、柵で囲われたさまざまな湯だまりがある。動物たちも飼育されている。"
          }
        },
        {
          image: "http://placehold.jp/600x200.png", // 画像URL,
          created_at: "2018-10-11 22:33:44", // 撮影日時。できればほしい笑
          spot: {
              id: 1,
              name: "由布岳",
              description: "由布岳は、大分県由布市にある標高1,583mの活火山。山体が阿蘇くじゅう国立公園に指定されている。"
          }
        }, 
        {
          image: "http://placehold.jp/500x200.png", // 画像URL,
          created_at: "2018-10-11 22:33:44", // 撮影日時。できればほしい笑
          spot: {
              id: 1,
              name: "由布岳",
              description: "由布岳は、大分県由布市にある標高1,583mの活火山。山体が阿蘇くじゅう国立公園に指定されている。"
          }
        }, 
        {
          image: "http://placehold.jp/300x200.png", // 画像URL,
          created_at: "2018-10-11 22:33:44", // 撮影日時。できればほしい笑
          spot: {
              id: 1,
              name: "由布岳",
              description: "由布岳は、大分県由布市にある標高1,583mの活火山。山体が阿蘇くじゅう国立公園に指定されている。"
          }
        }, 
        {
          image: "http://placehold.jp/100x300.png", // 画像URL,
          created_at: "2018-10-11 22:33:44", // 撮影日時。できればほしい笑
          spot: {
              id: 1,
              name: "由布岳",
              description: "由布岳は、大分県由布市にある標高1,583mの活火山。山体が阿蘇くじゅう国立公園に指定されている。"
          }
        }, 
        {
          image: "http://placehold.jp/800x70.png", // 画像URL,
          created_at: "2018-10-11 22:33:44", // 撮影日時。できればほしい笑
          spot: {
              id: 1,
              name: "由布岳",
              description: "由布岳は、大分県由布市にある標高1,583mの活火山。山体が阿蘇くじゅう国立公園に指定されている。"
          }
        }, 
        {
          image: "http://placehold.jp/50x520.png", // 画像URL,
          created_at: "2018-10-11 22:33:44", // 撮影日時。できればほしい笑
          spot: {
              id: 1,
              name: "由布岳",
              description: "由布岳は、大分県由布市にある標高1,583mの活火山。山体が阿蘇くじゅう国立公園に指定されている。"
          }
        }, 
      ],
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
