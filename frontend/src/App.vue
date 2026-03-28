<template>
  <main class="container">
    <h1>Vue 小 Demo</h1>
    <section class="card">
      <h2>计数器</h2>
      <p class="count">{{ count }}</p>
      <button class="btn" @click="count++">+1</button>
      <button class="btn secondary" @click="reset">重置</button>
    </section>

    <section class="card">
      <h2>待办列表</h2>
      <form class="row" @submit.prevent="addTodo">
        <input v-model="input" placeholder="添加待办…" />
        <button class="btn" type="submit">添加</button>
      </form>
      <ul class="todos">
        <li v-for="(t, i) in todos" :key="i">
          <label>
            <input type="checkbox" v-model="t.done" />
            <span :class="{ done: t.done }">{{ t.text }}</span>
          </label>
        </li>
      </ul>
    </section>
  </main>
 </template>

<script setup>
import { ref } from 'vue'

const count = ref(0)
const input = ref('')
const todos = ref([{ text: '学习 Vue', done: false }])

function reset() {
  count.value = 0
}

function addTodo() {
  const text = input.value.trim()
  if (text) {
    todos.value.push({ text, done: false })
    input.value = ''
  }
}
</script>

<style scoped>
.container {
  max-width: 720px;
  margin: 40px auto;
  padding: 24px;
  font-family: system-ui, -apple-system, Segoe UI, Roboto, Noto Sans, Arial, sans-serif;
  line-height: 1.6;
}
.card {
  background: #fff;
  border: 1px solid #e9e9e9;
  border-radius: 12px;
  padding: 16px 16px 8px;
  box-shadow: 0 1px 2px rgba(0,0,0,.04);
  margin: 16px 0;
}
.row {
  display: flex;
  gap: 8px;
}
input {
  flex: 1;
  padding: 8px 10px;
  border: 1px solid #ddd;
  border-radius: 8px;
}
.count {
  font-size: 28px;
  margin: 8px 0 12px;
}
.btn {
  padding: 8px 12px;
  border: 1px solid #409eff;
  background: #409eff;
  color: #fff;
  border-radius: 8px;
  cursor: pointer;
}
.btn.secondary {
  border-color: #ddd;
  background: #fff;
  color: #333;
}
.todos {
  list-style: none;
  padding: 0;
}
.todos li {
  padding: 6px 0;
}
.done {
  text-decoration: line-through;
  color: #999;
}
body {
  background: #f7f9fb;
}
</style>
