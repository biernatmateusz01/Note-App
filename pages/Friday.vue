<template>
  <div class="flex flex-col">
    <div class="flex flex-col">
      <div class="flex justify-between p-8">
        <div>
          <button
            @click="deleteAll"
            class="shadow-md bg-white text-yellow-400 px-4 rounded py-2 hover:text-white hover:bg-yellow-300"
          >
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
        </div>
        <div class="flex gap-2 flex-col">
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
                <span class="text-blue-400 font-semibold">Friday</span></span
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
      <Transition>
        <BaseModal @close-modal="closeModal" v-if="isEdit">
          <form @submit.prevent="editNote">
            <div
              class="bg-white p-6 rounded shadow-md flex flex-col text-lg md:min-w-[400px]"
            >
              <span class="mb-2">Edit note </span>
              <div class="flex flex-col gap-2">
                <BaseInput :id="2" v-model="vEditTitle">Tytuł</BaseInput>

                <BaseTextarea :id="2" v-model="vEditNote"
                  >Zawartość notatki</BaseTextarea
                >
              </div>
              <div class="flex gap-2 mt-3 justify-end">
                <button
                  type="button"
                  @click="isEdit = !isEdit"
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
      <div v-if="notes.length < 50" class="fixed bottom-3 right-3">
        <BaseButton v-if="!isOpen" @add-note="addNote" />
      </div>
    </TheNotesWrapper>
  </div>
</template>

<script setup>
const vNote = ref("");
const isOpen = ref(false);
const vTitle = ref("");
const notes = ref([]);
const isOpenEdit = ref(false);
const number = ref(1);
const isLoader = ref(false);
const count = ref(0);
const itemForEdit = ref(null);
const isEdit = ref(false);
const vEditTitle = ref("");
const vEditNote = ref("");

const deleteAll = () => {
  notes.value = [];
  localStorage.setItem("fridayNotes", JSON.stringify(notes.value));
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
  localStorage.setItem("fridayNotes", JSON.stringify(notes.value));
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

  localStorage.setItem("fridayNotes", JSON.stringify(notes.value));
  getNotesFromStorage();
  (vNote.value = ""), (vTitle.value = ""), (isOpen.value = false);
};

const getNotesFromStorage = () => {
  const booksFromStorage = localStorage.getItem("fridayNotes");
  notes.value = JSON.parse(booksFromStorage);
};

const markAsDone = (note) => {
  note.done = true;
  localStorage.setItem("fridayNotes", JSON.stringify(notes.value));
};

const editItem = (item) => {
  vEditNote.value = "";
  vEditTitle.value = "";
  isEdit.value = true;
  itemForEdit.value = item;
  vEditNote.value = itemForEdit.value.text;
  vEditTitle.value = itemForEdit.value.title;
};

const editNote = () => {
  itemForEdit.value.title = vEditTitle;
  itemForEdit.value.text = vEditNote;
  localStorage.setItem("fridayNotes", JSON.stringify(notes.value));
  isEdit.value = false;
};

onMounted(() => {
  if (localStorage.hasOwnProperty("fridayNotes")) {
  } else {
    localStorage.setItem("fridayNotes", JSON.stringify(notes.value));
  }
  getNotesFromStorage();
});
</script>
