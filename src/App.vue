<script setup lang="ts">
import InputTag from './components/TagInput.vue'
// import InputTagTailwind from './components/InputTagTailwind.vue'
const handleOnTagsChange = (tags: string[]) => {
  console.log(tags)
}

const mainStyles = [
  'h-screen',
  'bg-emerald-100',
  'flex',
  'flex-col',
  'justify-center',
  'items-center',
  'py-0',
  'px-10',
]
</script>

<template>
  <div :class="mainStyles">
    <h1 class="text-2xl font-bold">Tag Input</h1>
    <InputTag @onTagsUpdated="handleOnTagsChange" />
  </div>
</template>

<style scoped></style>
