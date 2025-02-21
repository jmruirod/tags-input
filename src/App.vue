<script setup lang="ts">
import InputTag from './components/TagInput.vue'
// import InputTagTailwind from './components/InputTagTailwind.vue'
const handleOnTagsChange = (tags: string[]) => {
  console.log(tags)
}
</script>

<template>
  <div class="h-screen bg-emerald-100 flex justify-center items-center py-0 px-10">
    <InputTag @onTagsUpdated="handleOnTagsChange" />
  </div>
</template>

<style scoped></style>
