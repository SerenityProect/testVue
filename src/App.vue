<template>
  <div id="app" class="wrapper">
    <keep-alive>
      <app-header  :title="titleHeader"  id="header"></app-header>
    </keep-alive>
    <app-content></app-content>
  </div>
</template>

<script>
    import AppHeader from './components/Header';
    import AppContent from './components/Content';
    export default {
        name: 'app',
        components: {
            AppHeader,
            AppContent,
        },
        data () {
            return {
                titleHeader:'ShoppingList',
            }
        }
    }
</script>

<style>
  html,body{
    min-height: 100%;
  }
  body{
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: left;
    color: #000;
    height: 100%;
  }
</style>