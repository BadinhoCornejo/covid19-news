<template>
  <div class="news-container">
    <h1 class="title">Mira las últimas noticias del COVID-19</h1>
    <div class="md-layout" v-if="news !== []">
      <div class="md-layout-item" v-for="(item, index) in news" :key="index">
        <NewsCard :article="item" />
      </div>
    </div>
  </div>
</template>

<script>
import NewsCard from "./NewsCard.vue";

export default {
  name: "NewsContainer",
  components: {
    NewsCard
  },
  props: {
    news: Array
  }
};
</script>

<style>
.news-container {
  margin: 100px;
}
h1.title {
  text-align: center;
  padding-top: 15px;
  padding-bottom: 15px;
  font-size: 24px;
  line-height: 1.5;
}
.show-more {
  display: flex;
  width: 100%;
  justify-content: center;
  padding: 32px;
  cursor: pointer;
  font-size: 16px;
}
@media (max-width: 700px) {
  .news-container {
    margin: auto;
    padding: 8px;
    padding-left: 12px;
    padding-top: 16px;
  }
}
</style>