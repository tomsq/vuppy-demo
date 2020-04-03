<template>
  <div>
    <vuppy v-model="images" locale="cs_CZ"></vuppy>
  </div>
</template>

<script>

import vuppy from 'vuppy'

export default {
  components: {
    vuppy
  },

  data() {
    return {
      images: []
    }
  }

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
