<template>
  <div class="home">
    <landing></landing>
    <about></about>
    <faq></faq>
    <sponsor></sponsor>
  </div>
</template>

<script>
// @ is an alias to /src
import Landing from '@/components/landing.vue';
import about from '@/components/about.vue';
import faq from '@/components/faq.vue';
import sponsor from '@/components/sponsor.vue';


export default {
  name: 'home',
  components: {
    Landing,
    about,
    faq,
    sponsor
  }
}
</script>

<style scoped lang="scss">

</style>