<template>
  <div>
    <div class="flex flex-col">
      <div class="flex justify-end p-8">
        <div class="flex gap-2 flex-col">
          <span>Notes:</span>
          <span>{{ allNotes.length }} / {{maxNotes}}</span>
        </div>
      </div>
    </div>

    <TheNotesWrapper>
      <TheNote v-for="note in allNotes" :key="note.id" :note="note" />
    </TheNotesWrapper>
  </div>
</template>

<script setup>

const monday = JSON.parse(localStorage.mondayNotes);
const tuesday = JSON.parse(localStorage.tuesdayNotes);
const wednesday = JSON.parse(localStorage.wednesdayNotes);
const thursday = JSON.parse(localStorage.thursdayNotes);
const friday = JSON.parse(localStorage.fridayNotes);
const saturday = JSON.parse(localStorage.saturdayNotes);
const sunday = JSON.parse(localStorage.sundayNotes);

const maxNotes = 7*50;

const allNotes = monday
  .concat(tuesday)
  .concat(wednesday)
  .concat(thursday)
  .concat(friday)
  .concat(saturday)
  .concat(sunday);

console.log(allNotes);
</script>
