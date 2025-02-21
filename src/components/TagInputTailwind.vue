<script setup lang="ts">
import { ref } from 'vue'

const currentValue = ref('')
const tags = ref<string[]>([])
const emit = defineEmits(['onTagsUpdated'])
const inputRef = ref<HTMLInputElement>()

const handleClick = () => {
  inputRef.value?.focus()
}

const handleKeyUp = (event: KeyboardEvent) => {
  if (event.key === 'Enter' && currentValue.value != '') {
    if (!tags.value.includes(currentValue.value)) {
      tags.value.push(currentValue.value)
      currentValue.value = ''
      emit('onTagsUpdated', tags.value)
    }
  }

  if (event.key === 'Backspace' && currentValue.value === '') {
    tags.value.pop()
    emit('onTagsUpdated', tags.value)
  }
}

const removeTag = (index: number) => {
  tags.value.splice(index, 1)
  emit('onTagsUpdated', tags.value)
}
</script>

<template>
  <div
    class="flex flex-wrap gap-1 p-1 bg-white border-2 border-gray-300 rounded shadow"
    @click="handleClick"
  >
    <div
      class="flex p-1 border border-gray-300 rounded items-center gap-1"
      v-for="(tag, index) in tags"
      :key="index"
    >
      {{ tag }}
      <button class="cursor-pointer hover:text-red-700 transition-all" @click="removeTag(index)">
        X
      </button>
    </div>
    <input
      class="border-none outline-none h-10"
      type="text"
      v-model="currentValue"
      @keyup="handleKeyUp"
    />
  </div>
</template>

<style scoped></style>
