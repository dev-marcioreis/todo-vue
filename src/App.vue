<script setup>

import { ref, onMounted, computed, watch } from 'vue'

const todos = ref([])
const name = ref('')
const input_content = ref('')
const input_category = ref(null)

const todos_asc = computed(() => todos.value.sort((a, b) => {
    return a.createdAt - b.createdAt
}))

const addTodo = () => {

}

watch(name, newVal => {
    localStorage.setItem('name', newVal)
})

onMounted(() => {
    name.value = localStorage.getItem('name') || ''
})

</script>

<template>
    <main class="app">
        <section class="greeting">
            <h2 class="title">E aí, <input type="text" placeholder="seu nome..." v-model="name" /></h2>
        </section>
        <section class="create-todo">
            <h3>Criar afazeres</h3>
            <form @submit.prevent="addTodo">
                <h4>Qual sua lista de tarefas?</h4>
                <input type="text" placeholder="Digite o nome..." v-model="input_content" />
                <h4>Escolha</h4>
                <div class="options">
                    <label>
                        <input type="radio" name="category" value="negócios" v-model="input_category" />
                        <span class="bubble business"></span>
                        <div>Negócios</div>
                    </label>
                    <label>
                        <input type="radio" name="category" value="pessoal" v-model="input_category" />
                        <span class="bubble personal"></span>
                        <div>Pessoal</div>
                    </label>
                </div>
            </form>
        </section>
    </main>
</template>

