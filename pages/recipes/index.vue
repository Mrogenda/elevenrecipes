<template>
  <div>
    <PreviewList />
    <PreviewListCategory category-variable="Kuchen" />
    <PreviewListCategory category-variable="Hauptspeise" />
    <PreviewListCategory category-variable="Kuchen" />
  </div>
</template>

<script>
import PreviewListCategory from '~/components/Recipes/PreviewListCategory.vue';
import PreviewList from '~/components/Recipes/PreviewList.vue';
export default {
    name: "IndexPage",
    components: { PreviewListCategory, PreviewList }
}
</script>
