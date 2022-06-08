<script lang="ts" setup>
  import { reactive, ref } from "vue";
  import INews from "../interface/news.interface";
  import AddNewsForm from "../components/addNewsForm.vue"

  let addNewsFormShow = ref(false)
  const newsData = ref<INews>()

  let newsall = reactive<INews[]>([])

  const loadNews = async () => {
    await fetch('http://localhost:8080/api/rest/news', {method: 'GET'}).then( async (res) => {
      newsall.splice(0, newsall.length, ...await res.json())
    })
  }

  await loadNews()

  const handleAdd = async (news: INews) => {
    addNewsFormShow.value = false
    if(news.id) {
      console.log(news)
      const requestOptions = {
        method: 'PUT',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({
            title: news.title,
            description: news.description,
            ownerId: news.ownerId
      })
      }
      await fetch(`http://localhost:8080/api/rest/news/${news.id}`, requestOptions).then(newsall => newsall.json())
    } else {
      const requestOptions = {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({
            title: news.title,
            description: news.description,
            ownerId: news.ownerId
        })
      }
      await fetch(`http://localhost:8080/api/rest/news`, requestOptions).then(newsall => newsall.json())
    }
    await loadNews()
    // const index = newsall.findIndex((item) => {
    //   return  item.id === news.id;
    // })
    // if(index == -1) {
    //   newsall.push(news)
    // } else {
    //   newsall.splice(index, 1, news);
    // }
  }

  const handleEdit = async (news: INews) => {
    addNewsFormShow.value = true
    newsData.value = news
  }

  const handleDel = async (id: string) => {
    await fetch(`http://localhost:8080/api/rest/news/${id}`, { method: 'DELETE' }).then(() => {})
    await loadNews()
    // const index = newsall.findIndex((news) => {
    //   return news.id === id;
    // });
    // if (index == -1) {
    //   return null;
    // } else {
    //   newsall.splice(index, 1);
    // }
  }

</script>

<template>
  <h1>Новости</h1>
  <button class="btn btn--add" @click="addNewsFormShow = true" v-if="!addNewsFormShow">
    Добавить новость
  </button>
  <AddNewsForm
    v-else
    @onChange="handleAdd"
    :newsData="newsData"
  />
  <ul class="news-all">
    <li class="news"
      v-for ="news in newsall" 
      :key="news.id"
    >
    <div class="news__btn">
      <button class="btn btn--edit" @click="handleEdit(news)"></button>
      <button class=" btn btn--exit" @click="handleDel(news.id)"></button>
    </div>
    <h2 class="title"> {{news.title}} </h2>
    <p class="description"> {{news.description}}</p>
    </li>
  </ul>
</template>

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
    flex-wrap: wrap;
    width: 100%;
    height: auto;
  }

  .news {
    width: 200px;
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
      background: url('/img/icon/edit_white.svg') no-repeat center center / cover;
    }

    .btn--edit:hover {
      background: url('/img/icon/edit_black.svg') no-repeat center center / cover;
    }

    .btn--exit {
      background: url('/img/icon/exit_white.svg') no-repeat center center / cover;
    }

     .btn--exit:hover {
      background: url('/img/icon/exit_black.svg') no-repeat center center / cover;
    }

  .title {
    margin-bottom: 10px;
  }
  
  .description {
    font-weight: 300;
    line-height: 1.2;
  }
</style>
