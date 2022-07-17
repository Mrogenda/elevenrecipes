<template>
  <div v-if="error != null">
    <h1>Error File not found</h1>
  </div>
  <div v-else-if="recipe != null">
    <h1>{{ recipe.attributes.Name }}</h1>
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
        'http://localhost:1337/api/recipes?filters[slug][$eq]=' + slug
      )
      return { recipe: response.data.data[0] };
    } catch (error) {
      return { error };
    }
  },
  /* data() {
    return {
      recipe: [],
      meta: {},
      error: null,
    }
  }, */
}
</script>
