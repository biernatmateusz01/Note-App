<template>
  <div class="p-8">
    <TheNotesWrapper>
      <TheNote
        v-for="note in deletedNotes"
        :key="note.id"
        :note="note"
        restore
        @mark-done="markAsDone(note)"
        @remove-item="restoreFromTrash(note)"
      />
    </TheNotesWrapper>
  </div>
</template>

<script setup>
const restoreFromTrash = (item) => {
  console.log(JSON.parse(localStorage.tuesdayNotes));
  const data = JSON.parse(localStorage.tuesdayNotes);
  console.log('before', data)
  data.push(item);
  console.log('after', data)

};

const deletedNotes = [
  {
    id: 1,
    text: "lorem ipsum dolor",
    title: "Lorem",
    creationDate: "26-03-2023",
    done: false,
    day: "monday",
  },
  {
    id: 1,
    text: "lorem ipsum dolor",
    title: "Lorem",
    creationDate: "26-03-2023",
    done: false,
    day: "sunday",
  },
  {
    id: 1,
    text: "lorem ipsum dolor",
    title: "Lorem",
    creationDate: "26-03-2023",
    done: false,
  },

  {
    id: 1,
    text: "lorem ipsum dolor",
    title: "Lorem",
    creationDate: "26-03-2023",
    done: false,
  },
  {
    id: 1,
    text: "lorem ipsum dolor",
    title: "Lorem",
    creationDate: "26-03-2023",
    done: false,
  },
  {
    id: 1,
    text: "lorem ipsum dolor",
    title: "Lorem",
    creationDate: "26-03-2023",
    done: false,
  },
  {
    id: 1,
    text: "lorem ipsum dolor",
    title: "Lorem",
    creationDate: "26-03-2023",
    done: false,
  },
  {
    id: 1,
    text: "lorem ipsum dolor",
    title: "Lorem",
    creationDate: "26-03-2023",
    done: false,
  },
  {
    id: 1,
    text: "lorem ipsum dolor",
    title: "Lorem",
    creationDate: "26-03-2023",
    done: false,
  },
  {
    id: 1,
    text: "lorem ipsum dolor",
    title: "Lorem",
    creationDate: "26-03-2023",
    done: false,
  },
  {
    id: 1,
    text: "lorem ipsum dolor",
    title: "Lorem",
    creationDate: "26-03-2023",
    done: false,
  },
];
</script>
