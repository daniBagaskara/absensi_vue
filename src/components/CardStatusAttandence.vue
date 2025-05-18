<template>
  <div class="bg-white rounded-xl shadow-sm overflow-hidden my-6">
    <div
      class="p-4"
      :class="{
        'bg-green-50': props.attendanceStatus === 'Checked in',
        'bg-yellow-50': props.attendanceStatus === 'Not yet scanned',
        'bg-red-50': props.attendanceStatus === 'Late',
      }"
    >
      <div class="flex items-center">
        <div class="mr-3">
          <div class="bg-indigo-100 p-3 rounded-full flex items-center justify-center">
            <i class="fas fa-calendar-check text-indigo-600 text-xl"></i>
          </div>
        </div>
        <div>
          <h5 class="font-medium text-gray-800 mb-1">Today's Status</h5>
          <p class="text-sm">
            <span
              class="px-2 py-1 rounded-md"
              :class="{
                'bg-green-100 text-green-800': props.attendanceStatus === 'Checked in',
                'bg-yellow-100 text-yellow-800': props.attendanceStatus === 'Not yet scanned',
                'bg-red-100 text-red-800': props.attendanceStatus === 'Late',
              }"
            >
              {{ props.attendanceStatus }}
            </span>
            <span v-if="props.checkInTime" class="text-gray-600 ml-2"
              >at {{ props.checkInTime }}</span
            >
          </p>
        </div>
      </div>
    </div>
  </div>
</template>
<script setup lang="ts">
interface Props {
  attendanceStatus: string
  checkInTime: string
}

const props = defineProps<Props>()
</script>
