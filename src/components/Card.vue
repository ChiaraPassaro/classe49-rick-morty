<template>
  <div

    class="col-3 p-3 border-0 card"
  >
    <img
      class="rounded-circle shadow mb-3"
      :src="image"
      :alt="name"
    >
    <h2>
      {{ name }}
    </h2>
    <h3 class="fs-6 fw-normal divider-top">
      {{ origin }}
    </h3>
    <h4 class="fs-5">
      {{ species }}
    </h4>
  </div>
</template>

<script>
export default {
  name: 'Card',
  // props: ['card'], // array
  props: [
    'image',
    'name',
    'origin',
    'species',
  ], // array
};
</script>

<style>

</style>
