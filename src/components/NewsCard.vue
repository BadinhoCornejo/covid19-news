<template>
  <div class="news-card">
    <md-card>
      <md-card-header>
        <md-avatar>
          <img class="avatar" :src="getLogo()" alt="Avatar" />
        </md-avatar>

        <div class="titles">
          <div class="md-title">{{ article.title }}</div>
          <div class="md-subhead">
            <div class="source">{{ article.source.name | formatSource }}</div>
            <span class="dot">°</span>
            <div class="date">{{article.publishedAt | formatDate}}</div>
          </div>
        </div>
      </md-card-header>

      <md-card-media>
        <img class="media" :src="article.urlToImage" alt="media" />
      </md-card-media>

      <md-card-content>{{ article.description }}</md-card-content>

      <md-card-actions>
        <md-button>
          <a :href="article.url" target="_blank">Ver noticia completa</a>
        </md-button>
      </md-card-actions>
    </md-card>
  </div>
</template>

<script>
import localization from "moment/locale/es";
import moment from "moment";

moment().locale("es", localization);

export default {
  props: {
    article: Object
  },
  filters: {
    formatSource: function(value) {
      return value.split(".")[0].toUpperCase();
    },
    formatDate: function(value) {
      return moment(value).format("LLL");
    }
  },
  methods: {
    getLogo: function() {
      let logo = this.article.source.name.split(".")[0].toLowerCase();
      return require(`../assets/logos/${logo}.png`);
    }
  }
};
</script>

<style>
.md-card {
  width: 380px;
  margin: 4px;
}

img.avatar {
  width: auto;
  height: auto;
}
.md-card-header {
  display: flex;
  width: auto !important;
}
.md-avatar {
  margin: 0px;
}
.titles {
  display: flex;
  flex-direction: column;
}
.md-title {
  font-weight: bold !important;
  text-align: initial !important;
  display: inline-flex;
  font-size: 16px !important;
  line-height: 1.5 !important;
}
.md-subhead {
  text-align: initial;
  font-size: 11px !important;
  display: inline-flex;
}
.md-card-content {
  text-align: initial;
}
a {
  color: #000000 !important;
  text-decoration: none !important;
}
.dot {
  padding-left: 4px;
  padding-right: 4px;
}
</style>