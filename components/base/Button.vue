<template>
  <button
    @click="$emit('add-note', $event)"
    class="bg-black text-white h-24 w-24 rounded-full animate-bounce"
  >
    <span class="text-3xl">+</span>
  </button>
</template>