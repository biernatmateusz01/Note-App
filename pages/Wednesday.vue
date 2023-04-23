<template>
  <div class="flex flex-col">
    <div class="flex flex-col">
      <div class="flex justify-between p-8">
        <button
          @click="deleteAll"
          class="shadow-md bg-white text-yellow-400 px-4 rounded py-2 hover:text-white hover:bg-yellow-300"
        >
          Delete all notes
        </button>
        <div class="flex gap-2">
          <span>Notes:</span>
          <span>{{ notes.length }} / 50</span>
        </div>
      </div>
    </div>
    <TheNotesWrapper>
      <TheNote
        v-for="note in notes"
        :key="note.id"
        :note="note"
        @delete-item="deleteItem(note)"
        @edit-item="editItem(note)"
        @mark-done="markAsDone(note)"
      />
      <Transition>
        <BaseModal @close-modal="closeModal" v-if="isOpen">
          <form @submit.prevent="addNewNote">
            <div
              class="bg-white p-6 rounded shadow-md flex flex-col text-lg md:min-w-[400px]"
            >
              <span class="mb-2"
                >Add new note for
                <span class="text-blue-400 font-semibold">Wednesday</span></span
              >
              <div class="flex flex-col gap-2">
                <BaseInput :id="1" v-model="vTitle">Tytuł</BaseInput>

                <BaseTextarea :id="1" v-model="vNote"
                  >Zawartość notatki</BaseTextarea
                >
              </div>
              <div class="flex gap-2 mt-3 justify-end">
                <button
                type="button"

                  @click="isOpen = !isOpen"
                  class="bg-yellow-400 py-2 px-4 rounded text-white shadow-sm text-xs"
                >
                  back
                </button>
                <button
                  type="submit"
                  class="bg-yellow-400 py-2 px-4 rounded text-white shadow-sm text-xs"
                >
                  add
                </button>
              </div>
            </div>
          </form>
        </BaseModal>
      </Transition>

      <div  class="fixed bottom-3 right-3">
        <BaseButton v-if="!isOpen" @add-note="addNote" />
      </div>
    </TheNotesWrapper>
  </div>
</template>

<script setup>
// import { computed } from "vue";

const vNote = ref("");
const isOpen = ref(false);
const vTitle = ref("");
const notes = ref([]);
const isOpenEdit = ref(false);
const number = ref(1);
const isLoader = ref(false);
const count = ref(0);

const deleteAll = () => {
  notes.value = [];
  localStorage.setItem("wednesdayNotes", JSON.stringify(notes.value));
};

const data = computed(() => {
  const data = new Date();

  const day = data.getDate();
  const month = data.getMonth();
  const year = data.getFullYear();

  const fullDate = `${day}-0${month}-${year}`;
  return fullDate;
});

const deleteItem = (note) => {
  const indexOfObject = notes.value.findIndex((object) => {
    return object.id === note.id;
  });

  notes.value.splice(indexOfObject, 1);
  localStorage.setItem("wednesdayNotes", JSON.stringify(notes.value));
};

const closeModal = () => {
  isOpen.value = false;
};

const addNote = () => {
  isOpen.value = true;
};

const addNewNote = () => {
  notes.value.push({
    id: count.value++,
    text: vNote,
    title: vTitle,
    creationDate: data,
    done: false,
  });

  localStorage.setItem("wednesdayNotes", JSON.stringify(notes.value));
  getNotesFromStorage();
  (vNote.value = ""), (vTitle.value = ""), (isOpen.value = false);
};

const getNotesFromStorage = () => {
  const booksFromStorage = localStorage.getItem("wednesdayNotes");
  notes.value = JSON.parse(booksFromStorage);
};

const markAsDone = (note) => {
  note.done = true;
  localStorage.setItem("wednesdayNotes", JSON.stringify(notes.value));
};

onMounted(() => {
  getNotesFromStorage();
});
</script>
