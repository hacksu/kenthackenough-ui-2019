<template>
    <div>
        <p></p>
        <qrcode-vue :value="uId"></qrcode-vue>
        {{ uId }}
    </div>
</template>

<script>
import QrcodeVue from 'qrcode.vue'
import apiConfig from "@/config/config";
import axios from 'axios'

export default {
    name: 'Me',
    components: {
        QrcodeVue
    },
    mounted() { 
        // TODO: verify logged in

        this.$parent.wrapper.applicationManager.getApplication()
        .then((app) => {
            console.log("_id: ", app._id)
            this.uId = app._id
            axios.get(apiConfig.api_base + '/gamify/game_intro/TODO/intro/' + this.uId)
        })
    }, 
    data() {
        return {
            uId: ''
        }
    }
}
</script>

<style>

</style>
