<template>
  <div>
    <ul class="category__list">
      <li
        v-for="category in categories"
        :key="category.id"
        class="category__item"
      >
        <a
          :href="'/' + category"
          class="category__link"
        >
          {{ category }}
        </a>
      </li>
    </ul>
    <a href="/recipes" class="underlined">Alle Kategorien</a>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'RecipesList',
  data() {
    return {
      categories: [],
    }
  },
  async mounted() {
    try {
      const categoryResponse = await axios.get('http://localhost:1337/api/content-type-builder/components/recipe-components.recipe-category')
      this.categories = categoryResponse.data.data.schema.attributes.Category.enum;
    } catch (error) {
      this.error = error
    }
  },
}
</script>

<style lang="scss">
  @import './CategoryList.scss';
</style>
