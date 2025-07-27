<template>
  <label class="inline-flex items-center gap-2 cursor-pointer select-none">
    <input
        type="checkbox"
        :checked="isChecked"
        @change="toggleValue"
        class="accent-blue-600 w-4 h-4"
    />
    <slot />
  </label>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  modelValue: [Array, Boolean],
  value: {
    type: [String, Number, Boolean],
    default: true
  }
})

const emit = defineEmits(['update:modelValue'])

const isArray = computed(() => Array.isArray(props.modelValue))

const isChecked = computed(() => {
  return isArray.value
      ? props.modelValue.includes(props.value)
      : props.modelValue
})

function toggleValue(event) {
  const checked = event.target.checked

  if (isArray.value) {
    const newValue = [...props.modelValue]
    const index = newValue.indexOf(props.value)

    if (checked && index === -1) newValue.push(props.value)
    else if (!checked && index !== -1) newValue.splice(index, 1)

    emit('update:modelValue', newValue)
  } else {
    emit('update:modelValue', checked)
  }
}
</script>
