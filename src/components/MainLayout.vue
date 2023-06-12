<template>
<div class="flex w-screen h-screen text-gray-700">
  <aside class="flex flex-col w-64 border-r border-gray-300 bg-gray-100">
    <!-- sidebar -->
<!-- <TestComponent /> -->
<h1>side bar</h1>
  </aside>
  <main class="flex flex-col flex-grow overflow-auto">
<!-- TODO change focus colour?? -->
  <editor-content :editor="editor" class="prose prose-zinc my-4 mx-auto text-left" />

  </main>
</div>

</template>

<script setup>
import { useEditor, EditorContent } from '@tiptap/vue-3'
import StarterKit from '@tiptap/starter-kit'
import { onBeforeMount, ref } from 'vue';

const storedNotes = ref({})

const editor = useEditor({
  content: '<p>I’m running Tiptap with Vue.js. 🎉</p>',
  extensions: [
    StarterKit,
  ],
})

const getNotesFromDb = () => {
  return new Promise((resolve, reject) => {
const notesDb = window.indexedDB.open("notes")

notesDb.onerror = e => {
  console.log(notesDb.onerror, e)
  reject('Error accessing the database')
};

notesDb.onsuccess = e => {
console.log(notesDb.onsuccess, e)
  resolve(storedNotes.value = e.target.value)
}

notesDb.onupgradeneeded = e => { //triggers when version of your db needs to be updated
console.log(notesDb.onupgradeneeded, e)
  e.target.result.createObjectStore("notes", {}) //create a data object , first arh is name of table and second is the object properties you need
}

  })
}

onBeforeMount(() => {
  getNotesFromDb()
})

</script>

