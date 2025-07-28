<template>
  <button
      :type="type"
      class="bg-blue-600 hover:bg-blue-700 text-white font-medium py-2 px-4 rounded transition cursor-pointer"
  >
    <slot/>
  </button>
</template>

<script setup>
defineProps({
  type: {
    type: String,
    default: 'button'
  }
})
</script>
