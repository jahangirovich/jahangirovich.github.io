<template>
  <div class="custom_button">
      {{ item }}
  </div>
</template>

<script>
export default {
    name:"Pagination",
    props:["item"]
}
</script>

<style lang="sass" scoped>
    @import '../styles/Pagination.sass'
</style>