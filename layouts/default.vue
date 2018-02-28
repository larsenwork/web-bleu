<template>
  <div class="page-content">
    <nuxt/>
    <bt/>
  </div>
</template>

<script>
import bt from '~/components/bt'

export default {
  components: {
    bt,
  },
  created() {
    if (process.browser) {
      window.addEventListener('keyup', function(event) {
        if (event.keyCode == 39 && $nuxt._router) {
          if (parseFloat($nuxt._router.history.current.name) < 19) {
            $nuxt._router.push(`${parseFloat($nuxt._router.history.current.name) + 1}`)
          }
        }
        if (event.keyCode == 37 && $nuxt._router) {
          if (parseFloat($nuxt._router.history.current.name) > 0) {
            $nuxt._router.push(`${parseFloat($nuxt._router.history.current.name) - 1}`)
          }
        }
      })
    }
  }
}
</script>

<style>
@import '~/assets/styles.css';
.page-content {
  display: flex;
  width: 100%
}

.page-content > .container {
  position: relative;
  width: 100%;
  margin-right: -100%;
}
</style>
