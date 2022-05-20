<template>
 <div>
   <h1>Новости</h1>
   <button class="btn btn--add" @click="addNewsFormShow = true" v-if="!addNewsFormShow">
      Добавить новость
   </button>
   <AddNewsForm  v-else @onNewsAdd="handleAdd" :isShow="false" />
   <ul class="news-all">
     <li class="news" 
        v-for ="news in newsall" 
        :key="news.id"
      >
      <div class="news__btn">
          <button class="btn btn--edit"></button>
          <button class=" btn btn--exit"></button>
      </div>
      <h2 class="title"> {{news.title}} </h2>
      <p class="description"> {{news.description}}</p>
      </li>
   </ul>
 </div>
</template>
<script lang="ts" setup>
  import { reactive, ref } from "vue";
  import INews from "../interface/news.interface";
  import AddNewsForm from "../components/addNewsForm.vue"


  let addNewsFormShow = ref(false)
  let newsall = reactive<INews[]>([
      {
          id: "f8e8b4cc-a279-493f-b8c1-ae1e0de5758e",
          title: "Название новости",
          description: "Описание новости",
          ownerId: "8fcc0e4a-8595-4221-80dd-2e35f6315ebf"
      },
      {
          id: "f8e8b4cc-a279-493f-b8c1-ae1e0de5758e",
          title: "Название новости",
          description: "Описание новости",
          ownerId: "8fcc0e4a-8595-4221-80dd-2e35f6315ebf"
      }
  ]);
  const handleAdd = (news: INews) => {
    newsall.push(news)
    addNewsFormShow.value = false
  }
</script>

<style scoped>
.btn--add {
  position: absolute;
  top:  48px;
  right: 10px;
}
  h1 {
    text-align: center;
    margin-bottom: 30px;
  }
  .news-all {
    display: flex;
    justify-content: space-between;
    width: 100%;
    height: auto;
  }

  .news {
    width: 400px;
    height: auto;
    padding: 10px;
    margin: 50px; 

    background: #f0f0f0;
    box-shadow: 3px 3px 5px  #a3a3a3;
  }

  .news__btn {
    display: flex;
    justify-content: flex-end;
  }
  .btn--edit,
  .btn--exit {
    width: 20px;
    height: 20px;
  }

    .btn--edit {
      background: url('/public/img/icon/edit_white.svg') no-repeat center center / cover;
    }

    .btn--edit:hover {
      background: url('/public/img/icon/edit_black.svg') no-repeat center center / cover;
    }

    .btn--exit {
      background: url('/public/img/icon/exit_white.svg') no-repeat center center / cover;
    }

     .btn--exit:hover {
      background: url('/public/img/icon/exit_black.svg') no-repeat center center / cover;
    }

  .title {
    margin-bottom: 10px;
  }
  
  .description {
    font-weight: 300;
    line-height: 1.2;
  }
</style>
