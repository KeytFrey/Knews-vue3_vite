<template>
  <form  @submit.prevent="log(), handleAdd()">
    <input placeholder="Введите тему новости" v-model="title" />
    <textarea placeholder="Введите описание новости" v-model="description"></textarea>
    <button class="btn">Сохранить</button>
  </form>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  data() {
    return {
      show: false,
      title: "",
      description: "",
    }
  },
  methods: {
    handleAdd() {
      this.show = false
      this.title = ""
      this.description = ""
    },
    log() {
      console.log(this.description)
    }
  },
})
</script>

