<template>
    <div>
        <p></p>
        <qrcode-vue :value="uId"></qrcode-vue>
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
        // TODO: verify logged in

        this.$parent.wrapper.applicationManager.getApplication()
        .then((app) => {
            console.log("_id: ", app._id)
            this.uId = app._id
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
