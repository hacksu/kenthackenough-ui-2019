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
        let user = this.$parent.wrapper.userManager.getLocalUser()
        if (user != null) {
            // TODO: user.key is not the correct value. Need to get _id
            this.uId = user.key
            console.log("set uId", this.uId)
        }
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
