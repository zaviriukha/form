<template>
  <label class="inline-flex items-center gap-2 cursor-pointer select-none">
    <input
        type="radio"
        :value="value"
        :checked="modelValue === value"
        @change="$emit('update:modelValue', value)"
        class="accent-blue-600 w-4 h-4"
    />
    <slot />
  </label>
</template>

<script setup>
defineProps({
  modelValue: [String, Number],
  value: {
    type: [String, Number],
    required: true
  }
})

defineEmits(['update:modelValue'])
</script>
