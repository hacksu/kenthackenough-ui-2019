<template>
    <div>
        <qrcode-stream @decode="onDecode"></qrcode-stream>
    </div>    
</template>

<script>
import { QrcodeStream} from 'vue-qrcode-reader'

export default {
    name: 'Scan',
    components: {
        QrcodeStream,
    },
    methods: {
        onDecode(content) {
            console.log(content)

            // TODO: Make request to backend
        }
    }
}
</script>

<style>

</style>