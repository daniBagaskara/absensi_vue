<template>
  <div
    v-if="props.showScanner"
    class="fixed inset-0 bg-black/50 flex items-center justify-center z-50"
  >
    <div class="bg-white rounded-lg w-11/12 max-w-md overflow-hidden">
      <div class="px-4 py-3 border-b border-gray-200 flex justify-between items-center">
        <h5 class="font-medium">Scan QR Code</h5>
        <button @click="closeScanner" class="text-gray-500 hover:text-gray-700">
          <i class="fas fa-times"></i>
        </button>
      </div>

      <!-- SCANNER AREA -->
      <div class="p-4 text-center">
        <qrcode-stream @decode="onDecode" @init="onInit">
          <div class="text-gray-500" v-if="!props.showScanner">Camera is loading...</div>
        </qrcode-stream>
        <p class="text-gray-500 text-sm mt-2">Point your camera at the QR code to check in/out</p>
      </div>

      <div class="px-4 py-3 border-t border-gray-200 flex justify-end">
        <button @click="closeScanner" class="px-4 py-2 bg-gray-200 hover:bg-gray-300 rounded-md">
          Cancel
        </button>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { QrcodeStream } from 'vue-qrcode-reader'

interface Props {
  showScanner: boolean
}
const props = defineProps<Props>()
const emit = defineEmits(['close-scanner', 'scanned'])

const closeScanner = () => {
  emit('close-scanner')
}

const onDecode = (result: string) => {
  // Kirim hasil QR ke parent
  emit('scanned', result)
  closeScanner()
}

const onInit = (promise: Promise<MediaStream>) => {
  promise.catch((err) => {
    console.error('Camera initialization failed:', err)
  })
}
</script>
