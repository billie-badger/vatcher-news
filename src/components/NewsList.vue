<template>
  <div class="newsList">
    <div class="container">
      <ul class="media-list">
        <li class="media" v-for="article in articles">
          <div class="media-left">
            <a v-bind:href="article.url" target="_blank">
              <img class="media-object pull-left" v-bind:src="article.urlToImage">
            </a>
          <div class="media-body">
            <h4 class="media-heading">
              <a v-bind:href="article.url" target="_blank">{{article.title}}</a>
            </h4>
            <h5><i>by {{article.author}}</i></h5>
            <p>{{article.description}}</p>
          </div>
          </div>
        </li>
      </ul>

    </div>
  </div>
</template>

<script>
export default {
  name: 'newslist',
  props: ['source'],
  data(){
    return {
      articles: [],

    }
  },
  methods:{
    updateSource: function(source){
      this.$http.get('https://newsapi.org/v1/articles?source=' + source + '&apiKey=cfc5b74f7bf44109b734b21714267bf3').then(response => {
        this.articles = response.data.articles;
      })
    }
  },
  created: function(){
    this.updateSource(this.source);
  },
  watch: {
    source: function(val){
      this.updateSource(val);
    }
  }
}
</script>

<style scoped>
  .media-object{
    width:180px;
    padding: 10px;
  }
  .media {
    border-bottom: 1px solid lightgrey;
    padding-top: 30px;
  }
</style>

<!--API cfc5b74f7bf44109b734b21714267bf3  -->
