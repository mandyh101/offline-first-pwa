<template>
<div class="flex w-screen h-screen text-gray-700">
  <aside class="flex flex-col w-64 border-r border-gray-300 bg-gray-100">
    <!-- sidebar -->
<!-- <TestComponent /> -->
<h1>side bar</h1>
  </aside>
  <main class="flex flex-col flex-grow">
<h1>main stuff</h1>
<editor-content :editor="editor" />
  </main>
</div>

</template>

<script setup>
import { useEditor, EditorContent } from '@tiptap/vue-3'
import StarterKit from '@tiptap/starter-kit'

const editor = useEditor({
  content: '<p>I’m running Tiptap with Vue.js. 🎉</p>',
  extensions: [
    StarterKit,
  ],
})

</script>

