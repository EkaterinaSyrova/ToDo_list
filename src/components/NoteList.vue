<script setup>
defineProps(['content_','content_title_','content_img_','removeTodo_','todo_'])
</script>

<template>
  <section  v-if="content_title_"  class="todo-list">
    <div class="list" id="todo-list">

      <div class="todo-item" >
        <div class="todo-content">
          <input :value="content_" type="text"/>
        </div>
        <div class="todo-content">
          <input :value="content_title_" type="text"  />
        </div>
        <div class="todo-content_img">
          <img :src="content_img_"/>
        </div>

        <div class="actions">
          <button class="delete" @click="removeTodo_(todo_)">Удалить</button>
        </div>
      </div>
    </div>
  </section>
</template>
