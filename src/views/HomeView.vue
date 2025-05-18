<script setup lang="ts">
import { ref } from 'vue'
import Navbar from '../components/Navbar.vue'
import TableAttandence from '../components/TableAttandence.vue'
import CardStatusAttandence from '../components/CardStatusAttandence.vue'
import ModalScanner from '../components/ModalScanner.vue'

const userName = ref('John Doe')
const attendanceStatus = ref('Not yet scanned')
const checkInTime = ref('')
const showScanner = ref(false)

const openScanner = () => {
  showScanner.value = true
}

const closeScanner = () => {
  showScanner.value = false
}

const submitQRCode = async (code: string) => {
  // Kirim ke Laravel API
  await axios.post('/api/absensi', { qr_code: code })
}
</script>

<template>
  <Navbar />
  <div class="min-h-screen container mx-auto px-4 py-6 bg-gray-100">
    <h1 class="text-2xl font-bold text-gray-800">Hi, {{ userName }}!</h1>
    <p class="text-gray-600">Welcome to your attendance dashboard</p>
    <CardStatusAttandence :attendanceStatus="attendanceStatus" :checkInTime="checkInTime" />
    <div class="text-center mb-8">
      <button
        @click="openScanner"
        class="bg-indigo-600 hover:bg-indigo-700 text-white font-medium rounded-full py-3 px-6 w-full scan-btn"
      >
        <i class="fas fa-qrcode mr-2"></i> Scan QR
      </button>
    </div>
    <TableAttandence />
    <ModalScanner
      :showScanner="showScanner"
      @close-scanner="closeScanner"
      @scanned="submitQRCode"
    />
  </div>
</template>
