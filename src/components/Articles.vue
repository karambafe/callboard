<template>
  <div class="articles">
    <md-toolbar>
      <h2 class="md-title" style="flex: 1">Статьи</h2>
      <md-input-container>
        <label>Поиск</label>
        <md-input v-model="filterKey"></md-input>
      </md-input-container>
    </md-toolbar>
    <md-card md-with-hover v-for="article in filteredData" :key="article.id">
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
        filterKey:'',
      };
    },
    methods: {
      getAllPOst() {
        const options ={
          params: {
            _limit: 10,
          }
        };
        this.$http.get(this.endpoint, options).then(function (response) {
          this.articles = response.data;
          console.log(this.articles);
        }, function (error) {
          // ошибка
        })
      },
    },
    computed: {
      filteredData: function () {
        var filterKey = this.filterKey && this.filterKey.toLowerCase();
        var data = this.articles;
        if (filterKey) {
          data = data.filter(function (row) {
            return Object.keys(row).some(function (key) {
              return String(row[key]).toLowerCase().indexOf(filterKey) > -1
            })
          })
        }

        return data;
      }
    },
    created() {
      this.getAllPOst();
    },
  };
</script>

