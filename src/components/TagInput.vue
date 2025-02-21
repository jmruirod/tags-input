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
  <div class="inputTag" @click="handleClick">
    <div class="tag" v-for="(tag, index) in tags" :key="index">
      {{ tag }} <button @click="removeTag(index)">X</button>
    </div>
    <input ref="inputRef" type="text" v-model="currentValue" @keyup="handleKeyUp" />
  </div>
</template>

<style scoped>
.inputTag {
  height: fit-content;
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  gap: 5px;
  padding: 5px;
  border: 2px solid #ccc;
  border-radius: 4px;
  background-color: white;
  box-shadow: 1px 1px 1px #999;
  cursor: text;
}

.inputTag .tag {
  display: flex;
  align-items: center;
  gap: 5px;
  padding: 5px;
  border: 1px solid #ccc;
  border-radius: 3px;
}

.inputTag input {
  border: none;
  outline: none;
  height: 40px;
}

.inputTag button {
  border: none;
  background: none;
  cursor: pointer;
}

.inputTag button:hover {
  color: darkred;
}
</style>
