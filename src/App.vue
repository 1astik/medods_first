<template>
  <div id="app">
      <div class="main">
          <home></home>
      </div>

  </div>
</template>

<script>
import Home from './components/Form';

export default {
  name: 'App',
  components: {
      Home
  }
}
</script>

<style lang="sass">
.main
    font-family: 'Oxygen', sans-serif
    background: rgb(129,125,186);
    background: linear-gradient(180deg, rgba(129,125,186,1) 0%, rgba(179,179,214,1) 35%, rgba(245,245,245,1) 97%);
</style>
