<template>
  <MailGenerator/>
</template>

<script>
import MailGenerator from './components/MailGenerator.vue'

export default {
  name: 'App',
  components: {
    MailGenerator
  }
}
</script>

<style>
#app {

  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 30px;
}
</style>
