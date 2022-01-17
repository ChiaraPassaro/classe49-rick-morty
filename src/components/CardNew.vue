<template>
  <div

    class="col-3 p-3 border-0 card"
  >
    <img
      class="rounded-circle shadow mb-3"
      :src="image"
      :alt="imageAlt"
    >
    <h2>
      {{ heading2 }}
    </h2>
    <h3
      v-if="heading3"
      class="fs-6 fw-normal divider-top"
    >
      {{ heading3 }}
    </h3>
    <h4
      v-if="heading4"
      class="fs-5"
    >
      {{ heading4 }}
    </h4>
  </div>
</template>

<script>
export default {
  name: 'CardNew',
  props: {
    image: {
      type: String,
      required: true,
    },
    imageAlt: {
      type: String,
      required: true,
    },
    heading2: {
      type: String,
      required: true,
    },
    heading3: {
      type: String,
      default: null,
    },
    heading4: {
      type: String,
      default: null,
    },

  },
};
</script>

<style>

</style>
