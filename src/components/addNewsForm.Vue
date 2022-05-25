<template>
  <form @submit.prevent="handleAdd() handleUp()">
    <input class="title" placeholder="Введите тему новости" v-model="title" />
    <textarea class="description" placeholder="Введите описание новости" v-model="description"></textarea>
    <button class="btn">Сохранить</button>
  </form>
</template>

<script lang="ts" setup>

import { onMounted, ref } from "@vue/runtime-dom";
import INews from "../interface/news.interface";
import { v4 as uuidv4 } from 'uuid';

  const props = defineProps({
    newsData: {
      type: Object
    }
  })

const title = ref("")
const description = ref("")



onMounted(() => {
  console.log(props)
}) 

const emit = defineEmits<{
  (e: 'onNewsAdd' , news: INews): void;
  (e: 'onNewsUp' , newsData): void;
}>();

const handleAdd = () => {
  emit('onNewsAdd', {
    id: uuidv4(),
    title: title.value,
    description: description.value
  
  })
}

  const handleUp = () => {
  emit('onNewsUp', {
    title: "",
    description: ""
  })
}
</script>