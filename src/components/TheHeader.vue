<template>
  <h2>Актуальные новости {{ title }}</h2>
</template>

<script>
export default {
  props: ['title'],
  data () {
    return {

    }
  }
}
</script>

<style scoped>
  h2 {
    color: #2c3e50;
  }
</style>
