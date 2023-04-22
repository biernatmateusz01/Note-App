<template>
  <div class="flex flex-col">
    <label :for="`base-input-${id}`" class="block mb-1 text-sm font-medium text-gray-700 dark:text-gray-50">
      <slot />
    </label>
    <div
      class="flex items-center px-3 overflow-hidden text-sm border border-gray-300 rounded-md focus-within:border-accent focus-within:ring-1 focus-within:ring-accent"
      :class="disabled ? 'bg-gray-100 text-gray-500' : 'bg-white'"
    >
      <input
        :id="`base-input-${id}`"
        :value="modelValue"
        :type="type"
        :placeholder="placeholder"
        class="block w-full placeholder-gray-400 focus:outline-none py-[7px] shadow-sm bg-transparent appearance-none"
        @input="$emit('update:modelValue', ($event.target as HTMLInputElement).value)"
      />
    </div>
    <p v-if="validation?.passed === false" class="mt-2 text-xs text-red-600">{{ validation?.message }}</p>
  </div>
</template>
<script setup lang="ts">
defineEmits<{
  (e: "update:modelValue", value: string): void;
}>();

defineProps<{
  modelValue?: string;
  modelModifiers?: object;
  id: number;
  type?: string;
  disabled?: boolean;
  placeholder?: string;
  validation?: Validation;
}>();
</script>
<style>
input:-webkit-autofill,
input:-webkit-autofill:hover,
input:-webkit-autofill:focus,
input:-webkit-autofill:active {
  transition: background-color 5000s ease-in-out 0s;
}
</style>