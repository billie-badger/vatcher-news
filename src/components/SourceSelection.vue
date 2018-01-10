<template>
  <div class="sourceselection">
    <div class="outer-jumbo">
      <div class="jumbotron">
        <img class="logo" src="../assets/v-news-logo.png">
        <h2><span class="glyphicon glyphicon-list-alt"></span>&nbsp; Vatcher News</h2>
        <h4>Choose your Weapon</h4>
        <select class="form-control" v-on:change="sourceChanged">
          <option v-for="source in sources" v-bind:value="source.id">{{source.name}}</option>
        </select>
        <div v-if="source">
          <h5 class="description">{{source.description}}</h5>
          <a v-bind:href="source.url" class="btn btn-primary" target="_blank">Go To {{source.name}} Website</a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'sourceselection',
  data(){
    return {
      sources: [],
      source: ""
    }
  },
  methods: {
    sourceChanged: function(e) {
      for (var i = 0; i < this.sources.length; i++) {
        if (this.sources[i].id == e.target.value) {
          this.source = this.sources[i];
        }
      }
      this.$emit('sourceChanged', e.target.value);
    }
  },
  created: function(){
    this.$http.get('https://newsapi.org/v1/sources?language=en')
    .then(response => {
      this.sources = response.data.sources;
    });
  }
}
</script>

<style scoped>
  .jumbotron{
    margin: 0 auto;
    width: 80%;
    border-radius: 10px;
    box-shadow: 0px 5px 8px 0px grey;
  }
  .form-control{
    margin: 0 auto;
    width: 80%;

  }
  .outer-jumbo{
    text-align: center;
  }
  .description{
    width: 80%;
    margin: 0 auto;
    padding: 20px;
  }
  .btn-primary{
    /* colors #2AFFCC-green , #00276A-blue*/
    border: none;
    background: -webkit-linear-gradient(left, #2AFFCC , #00276A); /* For Safari 5.1 to 6.0 */
    background: -o-linear-gradient(right, #2AFFCC, #00276A); /* For Opera 11.1 to 12.0 */
    background: -moz-linear-gradient(right, #2AFFCC, #00276A); /* For Firefox 3.6 to 15 */
    background: linear-gradient(to right, #2AFFCC , #00276A); /* Standard syntax */
    box-shadow: 0px 5px 8px 0px grey;
  }
  .glyphicon-list-alt{
    background: -webkit-linear-gradient(left, #2AFFCC, #00276A);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
  }
  .btn{
    transition: all .3s ease-in-out;
  }
  .btn:hover{
    transform: scale(1.1);
  }

</style>
