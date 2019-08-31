<template>
  <div class="home">
    <landing></landing>
    <about></about>
    <faq></faq>
    <kentmap></kentmap>
  </div>
</template>

<script>
// @ is an alias to /src
import Landing from '@/components/landing.vue';
import about from '@/components/about.vue';
import faq from '@/components/faq.vue';
import kentmap from '@/components/map.vue';

export default {
  name: 'home',
  components: {
    Landing,
    about,
    faq,
    kentmap
  }
}
</script>

<style scoped lang="scss">

</style>