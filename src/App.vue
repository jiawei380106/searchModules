<template>
  <div id="show-modules">
    <profile-page></profile-page>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld'
import {db} from "@/firebase.js"
//import {seRef} from '@/firebase.js'
import searchModules from './components/searchModules'
import ProfilePage from './components/ProfilePage'

export default {
  name: 'App',
  components: {
    'hello-world': HelloWorld,
    'search-modules': searchModules,
    'profile-page': ProfilePage
  },
  firebase: {
    modules: db
  },
  data () {
    return {
      search: ""
    }
  },
  computed: {
    filteredModules: function() {
      return this.modules.filter((module) => {
        return module[".key"].match(this.search.toUpperCase());
      })
    },
    
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

#show-modules {
  max-width: 800px;
  margin:0 auto;
}

.single-module {
  padding: 20px;
  margin: 20px 0;
  box-sizing: border-box;
  background: #eee;
}
</style>
