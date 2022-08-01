<template>
  <header>
    <span>Rezepte von der 11</span>
    <div class="menu">
      <ul class="menu__list">
        <li
        v-for="listItem in list"
        :key="listItem.id">
          <a
          :href="listItem.path"
          >{{ listItem.name }}</a>
        </li>
      </ul>
    </div>
  </header>
</template>

<script>
  export default {
    data() {
      return {
        list: [
          {
            name: 'Start',
            path: '/'
          },
          {
            name: 'Rezepte',
            path: '/recipes'
          },
          {
            name: 'Über Uns',
            path: '/about'
          },
          {
            name: 'Impressum',
            path: '/impressum'
          }
        ]
      }
    }
  }
</script>

<style lang="scss">
  @import './Header.scss';
</style>
