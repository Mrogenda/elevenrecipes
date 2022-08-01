<template>
  <footer>
    <p>© 2022 Marie Mrogenda. Alle Rechte vorbehalten.</p>
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
  </footer>
</template>

<script>
  export default {
    data() {
      return {
        list: [
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
    @import './Footer.scss';
</style>
