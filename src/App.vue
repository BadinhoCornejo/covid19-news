<template>
  <div id="app">
    <Header @filterNews="filterNews" />
    <NewsContainer v-if="searchValue === ''" :news="sortNews()" />
    <NewsContainer v-else-if="newsBackUp.length" :news="newsBackUp" />
    <div class="not-found" v-if="searchValue !== '' && !newsBackUp.length">
      <div class="not-found-content">
        <img
          class="not-found-image"
          src="./assets/svg/support-notes-monochrome-400px.png"
          alt="suport"
        />
        No encontramos resultados para "{{searchValue}}"
      </div>
    </div>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import NewsContainer from "./components/NewsContainer.vue";

function getRandom(floors, length) {
  const randomIndex = Math.floor(Math.random() * length + 1);

  if (!floors.includes(randomIndex) || floors === []) {
    return randomIndex;
  } else {
    getRandom(floors, length);
  }
}

export default {
  name: "App",
  components: {
    Header,
    NewsContainer
  },
  data() {
    return {
      searchValue: "",
      articles: [],
      newsBackUp: []
    };
  },
  methods: {
    filterNews(value) {
      this.searchValue = value;

      this.newsBackUp = this.articles.filter(
        article =>
          article.title
            .toLowerCase()
            .includes(this.searchValue.toLowerCase()) ||
          article.source.name
            .toLowerCase()
            .includes(this.searchValue.toLowerCase())
      );
    },
    sortNews() {
      const newsLength = this.articles.length;
      const sortedNews = [];
      var floors = [];

      //Ordenando aleatoriamente
      for (let i = 0; i < newsLength; i++) {
        const randomIndex = getRandom(floors, newsLength);

        floors.push(randomIndex);

        sortedNews.push(this.articles[randomIndex]);
      }

      //Ordenando por fecha
      sortedNews.sort(
        (after, before) =>
          new Date(before.publishedAt) - new Date(after.publishedAt)
      );

      return sortedNews;
    }
  },
  mounted: function() {
    const fetchData = (uri, page) => {
      if (page > 5) {
        return 0;
      }

      fetch(`${uri}/${page}`, { method: "get" })
        .then(res => res.json())
        .then(res => {
          res.articles.map(article => this.articles.push(article));
          fetchData(uri, page + 1);
        })
        .catch(err => {
          console.log(err);
        });
    };

    fetchData("https://peaceful-eyrie-08219.herokuapp.com/newsApi", 1);
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.not-found {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.not-found-content {
  width: 400px;
  margin-top: 3rem;
}
.not-found-image {
  margin-bottom: 16px;
}
</style>
