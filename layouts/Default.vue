<template>
  <div class="flex min-h-screen min-w-screen">
    <div class="w-1/4 max-h-screen">
      <TheNavigation />
    </div>
    <div class="w-3/4 max-h-screen overflow-auto">
      <slot />
    </div>
  </div>
</template>

<script setup>
const getData = () => {
  console.log("dodaj");
};
</script>
