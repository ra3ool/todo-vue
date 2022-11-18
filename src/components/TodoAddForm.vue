<template>
    <div class="add-items d-flex">
        <input type="text" class="form-control todo-list-input" placeholder="What do you need to do today?" v-model="newTodo" @keyup.enter="addTodo" />
        <button class="add btn btn-primary font-weight-bold todo-list-add-btn" @click="addTodo">
            Add
        </button>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                newTodo : ''
            }
        },
        emits: ['todo-text'],
        methods : {
            addTodo() {
                if(!this.newTodo) return alert('type something!')
                this.$emit('todo-text', this.newTodo)
                this.newTodo = ''
            }
        }
    }
</script>