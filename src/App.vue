<template>
  <div class="landing-page">
    <ProductSelector/>
  </div>
</template>

<script>
import ProductSelector from "@/components/ProductSelector.vue";

export default {
  name: 'App',
  components: {ProductSelector},
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.landing-page {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 100vh;
}

</style>
