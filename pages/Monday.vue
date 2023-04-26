<template>
  <div class="flex flex-col">
    <div class="flex flex-col">
      <div class="flex justify-between p-8">
        <div v-show="notes.length > 0">
          <button
            @click="isDeleteModal = !isDeleteModal"
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
        options
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
                <span class="text-blue-400 font-semibold">Monday</span></span
              >
              <div class="flex flex-col gap-2">
                <BaseInput :id="1" v-model="vTitle">Title</BaseInput>

                <BaseTextarea :id="1" v-model="vNote">Notes value</BaseTextarea>
              </div>
              <div class="mt-3 gap-2 flex justify-end">
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
                <BaseInput :id="2" v-model="vEditTitle">Title</BaseInput>

                <BaseTextarea :id="2" v-model="vEditNote"
                  >Notes value</BaseTextarea
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
      <Transition>
        <BaseModal @close-modal="closeModal" v-if="isDeleteModal">
          <div
            class="bg-white p-6 rounded shadow-md flex flex-col text-lg md:min-w-[400px]"
          >
            <p>Are you sure you want to delete all the notes ?</p>
            <div class="mt-4 flex items-center justify-center">
              <svg
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                viewBox="0 0 24 24"
                stroke-width="1.5"
                stroke="currentColor"
                class="w-24 h-24 text-red-600"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  d="M12 9v3.75m-9.303 3.376c-.866 1.5.217 3.374 1.948 3.374h14.71c1.73 0 2.813-1.874 1.948-3.374L13.949 3.378c-.866-1.5-3.032-1.5-3.898 0L2.697 16.126zM12 15.75h.007v.008H12v-.008z"
                />
              </svg>
            </div>
            <div class="mt-3 flex gap-1 items-center justify-center">
              <button
                @click="isDeleteModal = !isDeleteModal"
                class="bg-yellow-400 py-2 px-4 rounded text-white shadow-sm text-xs"
              >
                no
              </button>
              <button
                @click="deleteAll"
                class="bg-yellow-400 py-2 px-4 rounded text-white shadow-sm text-xs"
              >
                yes
              </button>
            </div>
          </div>
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
const isDeleteModal = ref(false);
useHead({
  title: "mondayNotes",
});

const deleteAll = () => {
  notes.value = [];
  localStorage.setItem("mondayNotes", JSON.stringify(notes.value));
  isDeleteModal.value = false;
};

const data = computed(() => {
  const data = new Date();

  const day = data.getDate();
  const month = data.getMonth();
  const year = data.getFullYear();

  const fullDate = `${day}-0${month + 1}-${year}`;
  return fullDate;
});

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
  localStorage.setItem("mondayNotes", JSON.stringify(notes.value));
  isEdit.value = false;
};

const deleteItem = (note) => {
  const indexOfObject = notes.value.findIndex((object) => {
    return object.id === note.id;
  });
  notes.value.splice(indexOfObject, 1);
  localStorage.setItem("mondayNotes", JSON.stringify(notes.value));
};

const closeModal = () => {
  isOpen.value = false;
  isEdit.value = false;
  isDeleteModal.value = false;
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
    day: 'monday'
  });

  localStorage.setItem("mondayNotes", JSON.stringify(notes.value));
  getNotesFromStorage();
  (vNote.value = ""), (vTitle.value = ""), (isOpen.value = false);
};

const getNotesFromStorage = () => {
  const booksFromStorage = localStorage.getItem("mondayNotes");
  notes.value = JSON.parse(booksFromStorage);
};

const markAsDone = (note) => {
  note.done = true;
  localStorage.setItem("mondayNotes", JSON.stringify(notes.value));
};

onMounted(() => {
  if (localStorage.hasOwnProperty("mondayNotes")) {
  } else {
    localStorage.setItem("mondayNotes", JSON.stringify(notes.value));
  }
  getNotesFromStorage();
});
</script>
