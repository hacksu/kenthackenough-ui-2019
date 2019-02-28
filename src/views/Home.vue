<template>
  <div class="home">
    <landing></landing>
    <about></about>
  </div>
</template>

<script>
// @ is an alias to /src
import Landing from '@/components/landing.vue';
import about from '@/components/about.vue';


export default {
  name: 'home',
  components: {
    Landing,
    about
  }
}
</script>

<style scoped lang="scss">

</style>