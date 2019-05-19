<template>
  <section class="container">
    <SeatingView />
  </section>
</template>

<script>
import SeatingView from '~/containers/SeatingView.vue'

export default {
  components: {
    SeatingView
  }
}
</script>

<style>
body {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  color: #35495e;
  letter-spacing: 1px;
}
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  text-align: center;
}
</style>
