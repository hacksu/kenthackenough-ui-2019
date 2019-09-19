<template>
  <div>
    <div class="me" align="center" v-if="$parent.user._id != ''">
      <qrcode-vue :value="uId" :size="size"></qrcode-vue>
      <h2>Get the QR code above scanned at a sponsor table, one of our activities, or at the JP Morgan hacker space. The more you participate, the more likely you are to win cool prizes!</h2>
    </div>

    <div class="me" v-if="$parent.user._id == ''">
      <h2>You must login to earn points.</h2>
      <router-link tag="button" to="/login" class="buttonInput">
        Login
      </router-link>
    </div>
  </div>
</template>

<script>
import QrcodeVue from 'qrcode.vue'

export default {
  name: 'Me',
  components: {
    QrcodeVue
  },
  mounted() { 
    this.$parent.wrapper.applicationManager.getApplication()
    .then((app) => {
      console.log("_id: ", app._id)
      this.uId = app._id
    })
  }, 
  data() {
    return {
      uId: '',
      size: 200
    }
  }
}
</script>

<style scoped lang="scss">
  @import '@/globalVars.scss';

  .me {
    width: 100%;
    padding: 4em 0;
  }

  h2 {
    padding: 0 20px;
  }

  canvas {
    height: 200px;
    width: 200px;
  }

  button {
    position: relative;
    text-align: center;
    display: inline-block;
    border: 2px solid $gold;
    background-color: #fff;
    width: 200px;
    height: 50px;
    font-size: 20px;
    cursor: pointer;
  }

  @media only screen and (min-width: 850px) {
    .me {
      width: 50%;
      margin: 0 auto;
    }
  }
</style>
