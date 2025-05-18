<template>
  <div class="flex-grow flex items-center justify-center p-4 bg-gray-100 min-h-screen">
    <div class="login-card bg-white rounded-xl w-full max-w-md overflow-hidden">
      <div class="bg-indigo-600 text-white p-6 text-center">
        <h1 class="text-2xl font-bold">Welcome Back</h1>
        <p class="opacity-90 mt-1">Please login to your account</p>
      </div>

      <form @submit.prevent="login" class="p-6">
        <!-- Email Field -->
        <div class="mb-4">
          <label for="email" class="block text-gray-700 text-sm font-medium mb-2">
            <i class="fas fa-envelope text-indigo-600 mr-1"></i> Email Address
          </label>
          <input
            v-model="email"
            type="email"
            id="email"
            required
            class="input-field w-full px-4 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-1 focus:ring-indigo-500"
            placeholder="your@email.com"
          />
        </div>

        <!-- Password Field -->
        <div class="mb-6">
          <label for="password" class="block text-gray-700 text-sm font-medium mb-2">
            <i class="fas fa-lock text-indigo-600 mr-1"></i> Password
          </label>
          <input
            v-model="password"
            type="password"
            id="password"
            required
            class="input-field w-full px-4 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-1 focus:ring-indigo-500"
            placeholder="••••••••"
          />
        </div>

        <!-- Remember Me & Forgot Password -->
        <div class="flex items-center justify-between mb-6">
          <div class="flex items-center">
            <input
              v-model="rememberMe"
              type="checkbox"
              id="remember"
              class="h-4 w-4 text-indigo-600 focus:ring-indigo-500 border-gray-300 rounded"
            />
            <label for="remember" class="ml-2 block text-sm text-gray-700"> Remember me </label>
          </div>
          <a href="#" class="text-sm text-indigo-600 hover:text-indigo-500"> Forgot password? </a>
        </div>

        <!-- Login Button -->
        <button
          type="submit"
          class="login-btn w-full bg-indigo-600 hover:bg-indigo-700 text-white font-medium py-2 px-4 rounded-md"
        >
          <span v-if="!Loading"> <i class="fas fa-sign-in-alt mr-2"></i> Login </span>
          <span v-else>Loading...</span>
        </button>

        <!-- Error Message -->
        <div v-if="errorMessage" class="mt-4 p-3 bg-red-50 text-red-700 rounded-md text-sm">
          <i class="fas fa-exclamation-circle mr-2"></i> {{ errorMessage }}
        </div>
      </form>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const email: string = ref('')
const password: string = ref('')
const router = useRouter()
const errorMessage: string = ref('')
const Loading: boolean = ref(false)

const login = () => {
  Loading.value = true
  // Simulate login
  if (email.value === 'admin@admin.com' && password.value === 'password') {
    localStorage.setItem('token', '1234567890')
    router.push('/')
  } else {
    errorMessage.value = 'Invalid credentials'
  }
  Loading.value = false
}
</script>
