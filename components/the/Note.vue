<template>
  <div
    class="relative p-4 shadow-md bg-white rounded-md border-l-8 border-gray-300 overflow-hidden hover:bg-gray-100"
  >
    <div
      v-if="note.done === true"
      class="absolute top-0 left-0 bg-black bg-opacity-40 h-full w-full flex items-center justify-center"
    >
      <img
        src="https://cdn2.iconfinder.com/data/icons/greenline/512/check-512.png"
        class="h-16 w-16"
        alt=""
      />
    </div>
    <div class="w-full flex justify-between mb-2 overflow-auto">
      <div class="flex flex-col">
        <span class="text-xs">Added:</span>
        <span
          v-if="note.hasOwnProperty('creationDate')"
          class="text-yellow-400 text-sm font-semibold"
          >{{ note.creationDate }}</span
        >
      </div>
      <div v-if="options" class="flex gap-1">
        <button @click="$emit('delete-item', $event)">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke-width="1.5"
            stroke="currentColor"
            class="w-6 h-6"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M14.74 9l-.346 9m-4.788 0L9.26 9m9.968-3.21c.342.052.682.107 1.022.166m-1.022-.165L18.16 19.673a2.25 2.25 0 01-2.244 2.077H8.084a2.25 2.25 0 01-2.244-2.077L4.772 5.79m14.456 0a48.108 48.108 0 00-3.478-.397m-12 .562c.34-.059.68-.114 1.022-.165m0 0a48.11 48.11 0 013.478-.397m7.5 0v-.916c0-1.18-.91-2.164-2.09-2.201a51.964 51.964 0 00-3.32 0c-1.18.037-2.09 1.022-2.09 2.201v.916m7.5 0a48.667 48.667 0 00-7.5 0"
            />
          </svg>
        </button>
        <button @click="$emit('edit-item', $event)">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke-width="1.5"
            stroke="currentColor"
            class="w-6 h-6"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M16.862 4.487l1.687-1.688a1.875 1.875 0 112.652 2.652L10.582 16.07a4.5 4.5 0 01-1.897 1.13L6 18l.8-2.685a4.5 4.5 0 011.13-1.897l8.932-8.931zm0 0L19.5 7.125M18 14v4.75A2.25 2.25 0 0115.75 21H5.25A2.25 2.25 0 013 18.75V8.25A2.25 2.25 0 015.25 6H10"
            />
          </svg>
        </button>
        <button @click="$emit('mark-done', $event)">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke-width="1.5"
            stroke="currentColor"
            class="w-6 h-6"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M9 12.75L11.25 15 15 9.75M21 12a9 9 0 11-18 0 9 9 0 0118 0z"
            />
          </svg>
        </button>
      </div>
      <div v-if="restore">
        <button @click="$emit('remove-item', $event)">restore</button>
      </div>
    </div>
    <div class="flex justify-between gap-4">
      <p class="text-lg font-semibold text-gray-700">{{ note.title }}</p>
    </div>
    <span class="mt-3 text-md">{{ note.text }} </span>
  </div>
</template>

<script setup>
defineProps({
  note: Object,
  options: Boolean,
  restore: Boolean,
});

const done = ref(false);

const asDone = () => {
  done.value = !done.value;
};
</script>
