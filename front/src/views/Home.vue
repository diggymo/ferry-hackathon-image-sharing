<template>
  <div>
    <section class="hero is-primary">
      <div class="hero-body">
        <div class="container">
          <h1 class="title">
            Primary title
          </h1>
          <h2 class="subtitle">
            Primary subtitle
          </h2>
        </div>
      </div>
    </section>
    <section class="section">
      <div class="container">
        <div class="columns is-mobile">
          <div v-for="image in images" :key="image.id" class="column is-half">
            <img src="https://bulma.io/images/placeholders/480x480.png">
          </div>
          <div class="column is-half">
            <img src="https://bulma.io/images/placeholders/480x640.png">
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
// @ is an alias to /src
export default {
  name: 'home',
  data() {
    return {
      images: [],
      
    }
  }
}
</script>
