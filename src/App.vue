<template>
  <div id="app">
    <h1>{{msg}}</h1>

    <book-mark></book-mark>

  </div>
</template>

<script>
  import Bookmark from './components/bookmarks.vue'

  export default {
    name: 'app',
    components: {
      'book-mark': Bookmark
    },
    data() {
      return {
        msg: 'Bookmarks'
      }
    }
  }
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css?family=Roboto+Slab:400,700');
  #app{
    font-size: 18px;
    width: 700px;
    margin:0 auto;
    font-family: 'Roboto Slab', serif;
    color:#333;
    padding:20px;
    box-sizing: border-box;
  }
  h1{
    padding-bottom:2px;
    position: relative;
    font-size:24px;
    margin-bottom:20px;
    font-weight: bold;

    &:after{
      content:'';
      display:block;
      height:2px;
      background:#ffc107;
      position:absolute;
      bottom:0;
      left:0;
      width:2em;
    }
  }
</style>