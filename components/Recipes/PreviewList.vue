<template>
  <div
    v-if="recipes.length > 0"
    class="recipe__container"
    >
    <h2>Neueste Rezepte</h2>
    <ul class="recipe__list">
      <li
        v-for="recipe in recipes.slice(0, 5)"
        :key="recipe.id"
        class="recipe__block"
      >
        <a :href="'/recipes/' + recipe.attributes.slug">
          <img :src="'http://localhost:1337' + recipe.attributes.Media.data.attributes.url" alt="" height="150px">
        </a>
        <a :href="'/recipes/' + recipe.attributes.Category">
          <p class="recipe__category">{{ recipe.attributes.Category }}</p>
        </a>
        <a :href="'/recipes/' + recipe.attributes.slug">
          <h3 class="recipe__name">{{ recipe.attributes.Name }}</h3>
          <p class="recipe__description">{{ recipe.attributes.ShortDescription }}</p>
        </a>
        <a :href="'/recipes/' + recipe.attributes.slug" class="underlined">
          weiterlesen..
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
      const response = await axios.get('http://localhost:1337/api/recipes?fields[0]=Name&fields[1]=slug&populate[2]=Media&fields[3]=Category&fields[4]=ShortDescription')
      this.recipes = response.data.data;
      this.meta = response.data.meta;
    } catch (error) {
      this.error = error
    }
  },
}
</script>

<!-- in response.data stehen die meta informationen wie pagination und anzahl der objekte, in data.data sind die attribute der einzelnen rezepte -->

<style lang="scss">
  @import './RecipeList.scss';
</style>
