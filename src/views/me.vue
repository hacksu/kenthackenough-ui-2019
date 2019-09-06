<template>
    <div>
        <!-- This is where the QR code will go -->
        <div id="id-qr"></div>
    </div>
</template>

<style>

</style>

<script>
export default {
    name: 'Me',
    mounted() {
        let user = this.$parent.wrapper.userManager.getLocalUser()
        if (user != null) {
            // TODO: Display a qrcode using legacy js
        }
    }
}



</script>