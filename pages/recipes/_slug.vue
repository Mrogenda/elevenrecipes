<template>
  <div v-if="error != null">
    <h1>Error File not found</h1>
  </div>
  <div v-else-if="recipe != null">
    <h2>{{ recipe.attributes.Name }}</h2>
    <img :src="'http://localhost:1337' + image.data.attributes.url" alt="" height="150px">
    <div>{{ recipe.attributes.Ingredients }}</div>
    <p>{{ recipe.attributes.Instruction }}</p>
  </div>
  <div v-else>
    ...loading
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'RecipeDetail',
  async asyncData({ params }) {
    const slug = params.slug // When calling /abc the slug will be "abc"
    try {
      const response = await axios.get(
        'http://localhost:1337/api/recipes?filters[slug][$eq]=' + slug + '&populate=Media'
      )
      return {
        recipe: response.data.data[0],
        image: response.data.data[0].attributes.Media, };
    } catch (error) {
      return { error };
    }
  },
  data() {
    return {
      error: null,
    }
  },
}
</script>
