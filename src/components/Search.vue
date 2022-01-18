<template>
  <div class="search">
    <input
      id="search"
      v-model="inputText"
      type="text"
      name="search"
    >
    <button
      class="btn btn-primary"
      type="submit"
      @click="$emit('doSearch', inputText)"
    >
      Cerca
    </button>
  </div>
</template>

<script>
export default {
  name: 'Search',
  data() {
    return {
      inputText: '',
    };
  },
};
</script>

<style>

</style>
