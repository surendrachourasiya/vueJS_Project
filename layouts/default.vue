<template>
  <div >
    <top-header/>
    <main id="main" role="main" class="container">
      <nuxt/>
    </main>
    <bottom-footer/>
  </div>
</template>

<script>
import TopHeader from '~/components/TopHeader.vue'
import BottomFooter from '~/components/BottomFooter.vue'

export default {
  components: {
    TopHeader,
    BottomFooter
  }
}
</script>

<style>
* {
  box-sizing: border-box;
}

body {
  font-family: "Lato",sans-serif;
}
</style>