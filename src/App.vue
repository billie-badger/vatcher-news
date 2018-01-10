<template>
  <div id="app">
    <!--<img class="logo" src="./assets/v-news-logo.png">-->
    <SourceSelection v-on:sourceChanged='sourceChanged'></SourceSelection>
    <NewsList v-bind:source='source'></NewsList>
  </div>
</template>

<script>
import SourceSelection from './components/SourceSelection'
import NewsList from './components/NewsList'

export default {
  name: 'app',
  components: {
    SourceSelection,
    NewsList
  },
  data () {
    return  {
      source: ''
    }
  },
  methods: {
    sourceChanged: function(source){
      this.source = source;
    }
  }
}
</script>

<style>
#app {
  padding: 20px;
  background: #ededed;
}
.logo{
  margin:0 auto;
}
</style>
