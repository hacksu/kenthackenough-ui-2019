<template>
  <div class="home">
    <landing></landing>
    <about></about>
  </div>
</template>

<script>
// @ is an alias to /src
import landing from '@/components/landing.vue';
import about from '@/components/about.vue';


export default {
  name: 'home',
  components: {
    landing,
    about
  }
}
</script>

<style scoped lang="scss">

</style>