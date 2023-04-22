<template>
  <div>
    <div>
      <label
        :for="`base-textarea-${id}`"
        class="block mb-1 text-sm font-medium text-gray-700 dark:text-gray-50"
      >
        <slot />
      </label>
      <textarea
        :id="`base-textarea-${id}`"
        :value="modelValue"
        class="block w-full px-3 py-2 text-sm placeholder-gray-400 border border-gray-300 rounded-md shadow-sm appearance-none focus:border-accent dark:bg-black-medium dark:text-white focus:outline-none"
        :class="bigger ? 'min-h-[124px]' : 'min-h-[6rem]'"
        @input="
          $emit('update:modelValue', ($event.target as HTMLInputElement).value)
        "
      ></textarea>
    </div>
  </div>
</template>
<script setup lang="ts">
defineEmits<{
  (e: "update:modelValue", value: string): void;
}>();

defineProps<{
  modelValue?: string;
  id: number | string;
  bigger?: boolean;
}>();
</script>
