<template>
  <div class="flex flex-col">
    <TheNotesWrapper>
      <BaseInput
        :id="1"
        type="text"
        v-model="input"
        placeholder="Search fruits..."
      />
      <TheNote v-for="note in filteredList()" :key="note" :note="note" />
      <div class="item error" v-if="input && !filteredList().length">
        <p>No results found!</p>
      </div>
    </TheNotesWrapper>
  </div>
</template>

<script setup>
import { ref } from "vue";
let input = ref("");
const notes = ref([]);
function filteredList() {
  return notes.value.filter(
    (note) => 
    console.log(note.filter(el => el.name))
    // note.value.title.toLowerCase().includes(input.value.toLowerCase())
  );
}

onMounted(() => {
  if (localStorage.hasOwnProperty("wednesdayNotes")) {
      const wednesday = localStorage.wednesdayNotes
    notes.value.push(JSON.parse(wednesday));
  }

  console.log(notes.value);
});
</script>
