<template>
  <div v-if="error != null">
    <h1>Error File not found</h1>
  </div>
  <div v-else-if="recipe != null">
    <h2>{{ recipe.attributes.Name }}</h2>
    <img :src="'http://localhost:1337' + image.data.attributes.url" alt="" height="150px">
    <p>{{ recipe.attributes.ShortDescription }}</p>
    <div>{{ recipe.attributes.PreparationTime }}</div>
    <p>{{ recipe.attributes.Category }}</p>
    <ul class="ingredients__container">
      <li
        v-for="ingredient in ingredients"
        :key="ingredient.id"
        class="ingredients__item"
      >
        <p>
          <span class="ingredients__ingredient">
            {{ ingredient.Ingredient }}
          </span>
          <span class="ingredients__amount">
            {{ ingredient.Amount }}
          </span>
          <span class="ingredients__unit">
            {{ ingredient.unit }}
          </span>
        </p>
      </li>
    </ul>
    <ul>
      <li
        v-for="instruction in instructions"
        :key="instruction.id"
      >
        <h3>{{ instruction.Title }}</h3>
        <p>{{ instruction.Instruction }}</p>
      </li>
    </ul>
    <NuxtLink to="/recipes">
      Zurück zur Übersicht
    </NuxtLink>
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
        'http://localhost:1337/api/recipes?filters[slug][$eq]=' + slug + '&populate=Media&populate=Ingredient&populate=Instruction'
      )
      return {
        recipe: response.data.data[0],
        image: response.data.data[0].attributes.Media,
        instructions: response.data.data[0].attributes.Instruction,
        ingredients: response.data.data[0].attributes.Ingredient,
        };
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


