<script setup>
import { ref, onMounted, computed, watch } from 'vue'
import NoteList from './NoteList.vue'
const todos = ref([])
const name = ref('')

const input_content = ref('')
const input_content_title = ref('')
const input_content_img = ref('')

const todos_asc = computed(() => todos.value.sort((a,b) =>{
  return a.createdAt - b.createdAt
}))

watch(name, (newVal) => {
  localStorage.setItem('name', newVal)
})

watch(todos, (newVal) => {
  localStorage.setItem('todos', JSON.stringify(newVal))
}, {
  deep: true
})

const addTodo = () => {
  if (input_content.value.trim() === '' || input_content_title.value.trim() === '' ||input_content_img.value.trim() === '' ) {
    return
  }

  todos.value.push({
    content: input_content.value,
    content_title: input_content_title.value,
    content_img: input_content_img.value,
    done: false,
    editable: false,
    createdAt: new Date().getTime()
  })
}

const removeTodo = (todo) => {
  todos.value = todos.value.filter((t) => t !== todo)
}

onMounted(() => {
  name.value = localStorage.getItem('name') || ''
  todos.value = JSON.parse(localStorage.getItem('todos')) || []
})
</script>

<template>
  <main class="app">
    <section class="greeting">
      <h2 class="title">
        Заметки
      </h2>
    </section>

    <section class="create-todo">
      <h1>Создать заметку</h1>
      <br>
      <form id="new-todo-form" @submit.prevent="addTodo">
        Тема
        <input
            type="text"
            name="content"
            id="content"
            v-model="input_content" />
        Основной текст
        <input
            type="text"
            name="content_title"
            id="content_title"
            v-model="input_content_title" />
        Добавить картинку
        <input
            type="text"
            name="content_img"
            id="content_img"
            placeholder="Вставте URL картинки"
            v-model="input_content_img" />
        <input type="submit" value="Добавить заметку" />
      </form>
      <br>
      <br>
      <h1>Список заметок</h1>
    </section>


    <NoteList
        v-for="todo in todos_asc"
        :content_="todo.content"
        :content_title_="todo.content_title"
        :content_img_="todo.content_img"
        :removeTodo_ ="removeTodo"
        :todo_ ="todo"
    ></NoteList>
  </main>
</template>>
