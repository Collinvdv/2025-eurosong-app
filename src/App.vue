<template>
  <div id="app">
    <!-- Navigation -->
    <NavigationComponent @setActivePage="setActivePage"/>

    <!-- Pages -->
     <PageArtists v-if="activePage == 'artists'"/>
     <PageHome v-if="activePage == 'home'"/>
     <PageRanking v-if="activePage == 'ranking'"/>
     <PageVoting v-if="activePage == 'voting'"/>
  </div>
</template>

<script>
  // Components
  import NavigationComponent from './components/NavigationComponent.vue';

  // Pages
  import PageArtists from './pages/PageArtists.vue';
  import PageHome from './pages/PageHome.vue';
  import PageRanking from './pages/PageRanking.vue';
  import PageVoting from './pages/PageVoting.vue';

  // Export
  export default {
    name: 'App',
    data() {
      return {
        activePage: "artists"
      }
    },
    components: {
      NavigationComponent,
      PageArtists,
      PageHome,
      PageRanking,
      PageVoting
    },
    methods: {
      setActivePage(page) {
        this.activePage = page;
      }
    }
  }
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
</style>
