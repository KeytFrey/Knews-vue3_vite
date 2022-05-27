<script lang="ts" setup>

import { ref } from "@vue/runtime-dom";
import INews from "../interface/news.interface";
import { v4 as uuidv4 } from 'uuid';

interface Props {
  newsData?: {
    id: string;
    title: string;
    description: string;
  }
}

const emit = defineEmits<{
  (e: 'onChange' , news: INews): void;
}>();

const {newsData} = defineProps<Props>();

const title = ref(newsData ? newsData.title : "");
const description = ref(newsData ? newsData.description : "");

const handleChange = () => {
  emit('onChange', {
    id: newsData ? newsData.id : uuidv4(),
    title: title.value,
    description: description.value
  })
}
</script>

<template>
  <form @submit.prevent="handleChange">
    <input class="title" placeholder="Введите тему новости" v-model="title" />
    <textarea class="description" placeholder="Введите описание новости" v-model="description"></textarea>
    <button class="btn">Сохранить</button>
  </form>
</template>
