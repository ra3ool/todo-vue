<template>
  <li :class="item.done ? 'completed' : ''">
    <div class="form-check">
      <label class="form-check-label">
        <input class="checkbox" type="checkbox" :checked="item.done" @change="doTodo(item.id, $event)" />
        <i class="input-helper"></i>
        <b>{{ item.text }}</b>
        <br />
        <small>{{ item.date }}</small>
      </label>
    </div>
    <div class="ml-auto">
      <Icon
        v-show="!item.done"
        icon="akar-icons:edit"
        width="25"
        height="25"
        style="cursor: pointer"
        @click="editTodo(item.id, item.text)"
      />
      <Icon
        icon="typcn:delete-outline"
        width="25"
        height="25"
        style="cursor: pointer"
        @click="deleteTodo(item.id, item.text)"
      />
    </div>
  </li>
</template>


<script>
import { Icon } from "@iconify/vue";

export default {
  components: {
    Icon,
  },
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
  emits: ["edit-todo", "delete-todo", "do-todo"],
  methods: {
    editTodo(id, oldText) {
      let newText = prompt('do edit in "' + oldText + '"');
      if(!newText) return;
      this.$emit("edit-todo", id, newText);
    },
    deleteTodo(id, text) {
      this.$emit("delete-todo", id, text);
    },
    doTodo(id, e) {
      this.$emit('do-todo', id, e.target.checked)
    }
  },
};
</script>
