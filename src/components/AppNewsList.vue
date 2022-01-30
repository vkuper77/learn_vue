<template>
  <hr/>
  <h4>{{ title }}</h4>
  <ul>
    <li v-for="item in news">
      {{ item.title }}
      <span v-if="item.wasRead">!!!</span>
    </li>
  </ul>
</template>

<script>
export default {
  inject: ['news', 'title']
}
</script>

<style scoped>

</style>
