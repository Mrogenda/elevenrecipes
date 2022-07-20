<template>
  <div
    v-if="recipes.length > 0"
    class="recipes--list"
    >
    <h1>dies sind die rezepte</h1>
    <ul>
      <li v-for="recipe in recipes" :key="recipe.id">
        <a
          :href="'/recipes/' + recipe.attributes.slug"
        >
        <img v-bind:src="'http://localhost:1337' + recipe.attributes.Media.data.attributes.url" alt="" height="150px">
        <p>{{ recipe.attributes.Name }}</p>
        </a>
      </li>
    </ul>
    <p v-if="meta.pagination && meta.pagination.page && meta.pagination.pageCount">Seite {{ meta.pagination.page }} von {{ meta.pagination.pageCount }}</p>
  </div>
  <div  v-else-if="error == null">loading...</div>
  <div v-else>
    error
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'RecipesList',
  data() {
    return {
      recipes: [],
      meta: {},
      error: null,
    }
  },
  async mounted() {
    try {
      const response = await axios.get('http://localhost:1337/api/recipes?fields[0]=Name&fields[1]=slug&populate[2]=Media')
      this.recipes = response.data.data;
      this.meta = response.data.meta;
    } catch (error) {
      this.error = error
    }
  },
}
</script>

<!-- in response.data stehen die meta informationen wie pagination und anzahl der objekte, in data.data sind die attribute der einzelnen rezepte -->
