<template>
  <div
    class="text-white px-4 py-8 xl:p-8 h-full rounded-r-sm bg-black shadow-md"
  >
    <div class="flex flex-col justify-between h-full rounded-r-lg">
      <div class="flex flex-col">
        <NuxtLink to="/">
          <div class="w-full flex flex-col md:flex-row gap-3">
            <img
              class="h-12 w-12 rounded-full"
              src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTfsTQFb0kp8I5e3JYPbVszsdPRsHBp3MM0snd7GltdQQ&s"
              alt=""
            />
            <span class="text-white font-semibold block my-auto"
              >Marek Koniarek</span
            >
          </div>
        </NuxtLink>

        <div class="flex flex-col gap-3 mt-8">
          <NuxtLink v-for="item in navigation" :key="item.id" :to="item.href"
            ><span class="hover:underline text-xs xl:text-sm">{{
              item.name
            }}</span></NuxtLink
          >
        </div>
      </div>
      <!-- <button @click="logout">Logout</button> -->
    </div>
  </div>
</template>

<script setup>
const route = useRoute();

const navigation = [
  {
    id: 1,
    name: "Monday",
    href: "/monday",
  },
  {
    id: 2,
    name: "Tuesday",
    href: "/tuesday",
  },
  {
    id: 3,
    name: "Wednesday",
    href: "/wednesday",
  },
  {
    id: 4,
    name: "Thursday",
    href: "/thursday",
  },
  {
    id: 5,
    name: "Friday",
    href: "/friday",
  },
  {
    id: 6,
    name: "Saturday",
    href: "/saturday",
  },
  {
    id: 7,
    name: "Sunday",
    href: "/sunday",
  },
  // {
  //   id: 8,
  //   name: "Done",
  //   href: "/done",
  // },
  // {
  //   id: 9,
  //   name: "Trash",
  //   href: "/trash",
  // },
  //   {
  //   id: 10,
  //   name: "All",
  //   href: "/all",
  // },
];
</script>
<style scoped>
.router-link-active {
  @apply bg-yellow-400 font-bold text-black pl-2 xl:pl-6 py-1 xl:py-2;
}
</style>
