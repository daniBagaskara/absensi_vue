<template>
  <nav class="bg-indigo-600 text-white shadow-sm">
    <div class="container mx-auto px-4 py-3 flex justify-between items-center">
      <div class="flex items-center">
        <i class="fas fa-fingerprint text-xl mr-2"></i>
        <span class="font-bold text-lg">AttendEase</span>
      </div>
      <button
        @click="logout"
        class="px-3 py-1 border border-white rounded-md text-sm hover:bg-indigo-700 transition"
      >
        <i class="fas fa-sign-out-alt mr-1"></i> Logout
      </button>
    </div>
  </nav>
</template>
<script setup lang="ts">
import { useRouter } from 'vue-router'

const router = useRouter()

const logout = () => {
  localStorage.removeItem('token')
  router.push('/login')
}
</script>
