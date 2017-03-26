<template>
  <div class="articles">
    <md-toolbar>
      <h2 class="md-title" style="flex: 1">Статьи</h2>
    </md-toolbar>
    <md-card md-with-hover v-for="article in articles">
      <md-card-header>
        <div class="md-title">{{ article.title }}</div>
      </md-card-header>
      <md-card-content>
        {{ article.body }}
      </md-card-content>
      <md-card-actions>
        <md-button>Перейти</md-button>
      </md-card-actions>
    </md-card>
  </div>
</template>

<script>
export default {
  name: 'articles',
  data() {
    return {
      endpoint: 'https://jsonplaceholder.typicode.com/posts',
      articles: [],
    };
  },
  methods: {
    getAllPOst() {
      this.$http.get(this.endpoint).then(function (response) {
        this.articles = response.data;
        console.log(this.articles);
      }, function (error) {
        // ошибка
      })
    },
  },
  created() {
    this.getAllPOst();
  },
};
</script>

