<script setup>
import NoteList from './components/NoteList.vue'
import AddNoteForm from './components/AddNoteForm.vue'
</script>

<template>
  <header>
    <div class="wrapper">
      <NoteList />
    </div>
  </header>

  <main>
    <div class="wrapper">
      <AddNoteForm />
    </div>
  </main>
</template>
