<template>
  <div class="news-container">
    <h1 class="title">Mira las últimas noticias del COVID-19</h1>
    <div class="md-layout md-gutter">
      <div class="md-layout-item" v-for="(item, index) in news" :key="index">
        <NewsCard :article="item" />
      </div>
      <div class="show-more" v-if="pages.length !== 0" v-on:click="showMore">Mostrar más</div>
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
  data() {
    return {
      news: [],
      pages: [1, 2, 3, 4, 5]
    };
  },
  mounted: function() {
    fetch(`http://localhost:3000/newsApi/${this.pages[0]}`, { method: "get" })
      .then(res => res.json())
      .then(res => (this.news = res.articles));

    this.pages.reverse();
    this.pages.pop();
  },
  methods: {
    showMore: function() {
      fetch(
        `http://localhost:3000/newsApi/${this.pages[this.pages.length - 1]}`,
        {
          method: "get"
        }
      )
        .then(res => res.json())
        .then(res => res.articles.map(i => this.news.push(i)));

      this.pages.pop();
      console.log(this.pages);
    }
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
}
.show-more{
  display: flex;
  width: 100%;
  justify-content: center;
  padding: 32px;
  cursor: pointer;
  font-size: 16px;
}
</style>