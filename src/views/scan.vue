<template>
    <div>
        <p>{{ sid }}</p>

        <qrcode-stream @decode="onDecode"></qrcode-stream>
        <p>{{ uid }}</p>

        <select v-model="pid">
            <option v-for="code in codes" v-bind:key="code.pointID" :value="code.pointID">{{ code.name }}</option>
        </select>

        <p id="success">{{ ok }}</p>
        <p id="err">{{ errors }}</p>
    </div>    
</template>

<script>
import { QrcodeStream} from 'vue-qrcode-reader'
import apiConfig from "@/config/config";
import axios from 'axios'

export default {
    name: 'Scan',
    components: {
        QrcodeStream,
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
            this.ok = ""
            this.errors = ""

            axios.get(apiConfig.api_base + '/gamify/' + this.pid + '/' + 'TODO' + '/' + this.sid + '/' + this.uid)
            .then((res) => {
                console.log(res)
                this.ok = "Points Redeemed!"
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

<style>
#success {
    color: green;
}
#err {
    color: red;
}
</style>