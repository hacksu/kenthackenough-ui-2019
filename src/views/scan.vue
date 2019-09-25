<template>
  <div id="scan-container">
    <h2>Scan the attendee's QR Code to allow them to redeem points.</h2>

    <qrcode-stream @decode="onDecode"></qrcode-stream>

    <h2>Choose the points to award.</h2>

    <select v-model="pid">
      <option v-for="code in codes" v-bind:key="code.pointID" :value="code.pointID">{{ code.name }}</option>
    </select>

    <p v-if="ok != ''" id="success">{{ ok }}</p>
    <p v-else id="err">{{ errors }}</p>
  </div>    
</template>

<script>
import { QrcodeStream } from 'vue-qrcode-reader'
import apiConfig from "@/config/config";
import axios from 'axios'

export default {
  name: 'Scan',
  components: {
      QrcodeStream
  },
  mounted() {
    this.sid = this.$route.query.sid
    console.log(apiConfig.api_base)
    axios.get(apiConfig.api_base + '/gamify/' + this.sid)
    .then((data) => {
      console.log('points', data)
      this.codes = data.data
      this.pid = this.codes[0].pointID
    })
  },
  methods: {
    onDecode(content) {
      console.log(content)
      this.uid = content
      axios.get(apiConfig.api_base + '/gamify/' + this.pid + '/' + 'TODO' + '/' + this.sid + '/' + this.uid)
      .then((res) => {
        this.ok = "Points added successfully"
        console.log(res)
      })
      .catch((err) => {
        console.log(err.response)
        this.errors = err.response.data
      })
    }
  },
  data() {
    return {
      uid: '',
      sid: '',
      pid: '',
      codes: [],
      errors: "",
      ok: ""
    }
  }
}
</script>

<style scoped lang="scss">
  @import '@/globalVars.scss';

  #scan-container {
    padding: 20px;
  }

  select {
    font-family: athelas;
    color: $dark-blue;
    background: $gold;
    border: solid $gold 1px;
    font-size: 20px;
    padding: 10px 20px;
    margin-bottom: 15px;
    cursor: pointer;
  }

  #success {
    color: green;
  }

  #err {
    color: red;
  }
</style>