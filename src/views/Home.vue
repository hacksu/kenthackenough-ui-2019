<template>
  <div class="home">
    <landing></landing>
    <about></about>
    <faq></faq>
  </div>
</template>

<script>
// @ is an alias to /src
import Landing from '@/components/landing.vue';
import about from '@/components/about.vue';
import faq from '@/components/faq.vue';


export default {
  name: 'home',
  components: {
    Landing,
    about,
    faq
  }
}
</script>

<style scoped lang="scss">

</style>