<script setup lang="ts">
    import { ref } from 'vue'
    interface todo {
    name: string
    //deadLine: string
    end: boolean
    }

    const todos = ref<todo[]>([
    { name: 'A Tour of Go ',end: false}
    ])
    
    const newTodoName = ref('')

    const addTodo = () => {
        if (newTodoName.value != ''){
            todos.value.push({ name: newTodoName.value, end: false })
        }
    }
    const endTodo = (index: number) => {
        todos.value[index].end = true
    }
    const notEndTodo = (index: number) => {
        todos.value[index].end = false
    }
    const eraceTodo = (index: number) => {
        todos.value.splice(index ,1)
    }
</script>

<template>
  <div>
    <div>ToDoリスト</div>
    <ul>
        <li>
            <div>未完了</div>
            <ul>
                <div v-for="(todo, index) in todos" :key="todo.name">
                    <li v-if="todo.end == false">
                    <div>{{ todo.name }}</div>
                    <button @click="endTodo(index)">完了</button>
                    </li>
                </div>
            </ul>
        </li>
        <li>
            <div>完了</div>
            <ul>
                <div v-for="(todo, index) in todos" :key="todo.name">
                    <li v-if="todo.end">
                    <div>{{ todo.name }}</div>
                    <button @click="notEndTodo(index)">未完了</button>
                    <button @click="eraceTodo(index)">削除</button>
                    </li>
                </div>
            </ul>
        </li>
    </ul>
    <div>
        <label>
            タスク名
            <input v-model="newTodoName" type="text" />
        </label>
        <!-- <label>
            価格
            <input v-model="newtodoPrice" type="number" />
        </label> -->
        <button @click="addTodo">追加</button>
    </div>
  </div>
</template>

<style></style>