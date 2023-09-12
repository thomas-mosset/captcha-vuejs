<template>
  <Captcha />
</template>

<script>
import Captcha from './components/Captcha.vue'

export default {
  name: 'App',
  components: {
    Captcha
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Open+Sans:wght@400;500;700&display=swap');

#app {
  font-family: 'Open Sans', sans-serif;
  text-align: center;
  margin-top: 60px;
}
</style>
