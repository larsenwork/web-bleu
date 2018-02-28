<template>
  <section class="container bg-cat">
    <h1 class="title">
      Caniuse
    </h1>
    <no-ssr><script src="https://cdn.jsdelivr.net/gh/ireade/caniuse-embed/caniuse-embed.min.js"></script></no-ssr>
    <div class="ciu_embed" data-feature="web-bluetooth" data-periods="future_2,future_1,current,past_1,past_2" data-accessible-colours="false">
      <a href="http://caniuse.com/#feat=web-bluetooth">Can I Use web-bluetooth?</a> Data on support for the web-bluetooth feature across the major browsers from caniuse.com.
    </div>
  </section>
</template>

<script>
export default {
}
</script>

<style>
.ciu_embed {
  margin-bottom: -30px;
  display: flex;
}
</style>
