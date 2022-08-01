<template>
  <div
    v-if="info"
    class="hero__container"
    >
    <img
      :src="'http://localhost:1337' + media.url"
      :alt="media.alternativeText"
      height="400px"
      class="hero__image"
    >
    <h1 class="hero__headline">{{ info.LandingPageTitle }}</h1>
    <p class="hero__text">{{ info.IntroDescription }}</p>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'HeroTeaser',
  data() {
    return {
      info: [],
      media: [],
      error: null,
    }
  },
  async mounted() {
    try {
      const response = await axios.get('http://localhost:1337/api/landing-page?populate[1]=HeroTeaser')
      this.info = response.data.data.attributes;
      this.media = response.data.data.attributes.HeroTeaser.data.attributes;
    } catch (error) {
      this.error = error
    }
  },
}
</script>

<style lang="scss">
  @import './HeroTeaser.scss';
</style>
