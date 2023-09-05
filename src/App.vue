<script setup>
  import { ref } from 'vue';

  let show = ref(false);
  let note = ref([]);
  let noteContent = ref("");
  let error = ref("");

  const openCloseModal = () => {
    noteContent.value = "";
    show.value = !show.value;
  }

  const addNote = () => {
    if(noteContent.value != " " && noteContent.value.length >= 6){
      note.value.push({
        id: Math.floor(Math.random() * 100000000),
        text: noteContent.value,
        date: new Date(),
        backgroundColor: getRandomColor( )
      });
      error.value = "";
      openCloseModal();
    }else{
      error.value = "Note too short, text must be up to 6 characters";
    }
  }

  const getRandomColor = () => {
    return "hsl(" + Math.random() * 360 + ", 100%, 75%)";
  }
  

</script>

<template>
  <main class="mx-[2rem] md:mx-[12rem]">
    <div class="flex justify-between mt-12 mb-2">
      <div class="text-4xl font-bold">Vue Note</div>
      <div class="">
        <button @click="openCloseModal" class="p-4 bg-black text-white rounded-full">add</button>
      </div>
    </div>
    <hr>
    <div class="grid grid-cols-4 gap-2">
      <div class="mt-4" v-for="each in note" :key="each.id">
        <div class="border p-2 rounded w-auto h-auto text-gray-700" :style="{backgroundColor: each.backgroundColor}">
          <h3 class="text-sm">{{ each.text }}</h3>
          <p class="text-sm">{{ each.date.toLocaleDateString("en-US") }}</p>
        </div>
      </div>
    </div>
    
  </main>
  <div v-if="show" class="fixed top-0 bottom-0 left-0 right-0 p-6 bg-black opacity-75 grid grid-cols-1 place-contents-center">
    <div class="bg-white shadow-md rounded-2xl m-32 w-auto">
      <div class="w-auto mx-8">
        <textarea v-model="noteContent" class="border border-gray-400 w-full mt-6 rounded-2xl p-4" cols="30" rows="10"></textarea>
        <div class="bg-red-500 text-white p-2" v-if="error != ''">
          {{ error }}
        </div>
        <button @click="addNote" class="p-4 bg-blue-500 rounded w-full text-white mt-4">Add note</button>
        <button @click="openCloseModal"  class="p-4 bg-red-500 rounded w-full text-white mt-4">Close</button>
      </div>
    </div>
  </div>
</template>

