<template>
  <div class="bg-white rounded-xl shadow-sm overflow-hidden">
    <div class="px-4 py-3 border-b border-gray-200">
      <h5 class="font-medium text-gray-800">
        <i class="fas fa-history text-indigo-600 mr-2"></i> Recent Attendance
      </h5>
    </div>
    <div class="p-0">
      <div class="attendance-table">
        <table class="w-full">
          <thead class="bg-gray-50">
            <tr class="text-left text-gray-600 text-sm">
              <th class="px-4 py-3">Date</th>
              <th class="px-4 py-3">Check-in</th>
              <th class="px-4 py-3">Status</th>
            </tr>
          </thead>
          <tbody class="divide-y divide-gray-200">
            <tr v-for="(record, index) in attendanceRecords" :key="index" class="hover:bg-gray-50">
              <td class="px-4 py-3 text-gray-700">{{ record.date }}</td>
              <td class="px-4 py-3 text-gray-700">{{ record.time }}</td>
              <td class="px-4 py-3">
                <span
                  class="px-2 py-1 rounded-md text-sm"
                  :class="{
                    'bg-green-100 text-green-800': record.status === 'On time',
                    'bg-red-100 text-red-800': record.status === 'Late',
                    'bg-blue-100 text-blue-800': record.status === 'Leave',
                  }"
                >
                  {{ record.status }}
                </span>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>
<script setup lang="ts">
import { ref } from 'vue'

const attendanceRecords = ref([
  { date: '2023-04-01', time: '08:00 AM', status: 'On time' },
  { date: '2023-04-02', time: '08:05 AM', status: 'Late' },
  { date: '2023-04-03', time: '08:10 AM', status: 'Leave' },
])
</script>
