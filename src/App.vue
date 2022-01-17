<template>
  <div id="app">
    <Header />
    <Main />
    <Footer />
  </div>
</template>

<script>
import Header from './components/Header.vue';
import Main from './components/Main.vue';
import Footer from './components/Footer.vue';

export default {
  name: 'App',
  components: {
    Header,
    Main,
    Footer,
  },
  data() {
    return {
      msg: 'Welcome ',
    };
  },
};
</script>

<style lang="scss">
@import "~bootstrap/scss/bootstrap";
body  {
  background-image:
    linear-gradient(
      to left,
      transparent 0px,
      transparent 20px,
      rgba(0, 0, 0, 0.02) 20px,
    rgba(0, 0, 0, 0.02) 40px),
    linear-gradient(
      to bottom, transparent 0px,
      transparent 20px,
      rgba(0, 0, 0, 0.02) 20px,
      rgba(0, 0, 0, 0.02) 40px
      );
    background-size: 40px, 100% 40px;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
