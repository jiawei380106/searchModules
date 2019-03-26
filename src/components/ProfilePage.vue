<template>
  <div id="show-modules">
    <h1>Profile Page</h1>
    <input type="text" v-model="search" placeholder="search modules">
    <div v-for="module in filteredModules" class="single-module">
      <h2>{{module["ModuleCode"]}} {{module["ModuleTitle"]}}</h2>
      <article>module description</article>
    </div>
  </div>
</template>

<script>
import HelloWorld from "./HelloWorld";
import { db } from "@/firebase.js";
//import {seRef} from '@/firebase.js'

export default {
  name: "searchModules",
  components: {
    HelloWorld
  },
  firebase: {
    modules: db.ref("se/data")
  },
  data() {
    return {
      search: ""
    };
  },
  computed: {
    filteredModules: function() {
      var datakeys = [];
      datakeys = Object.keys(this.modules);
      console.log(datakeys);
      var m = Object.keys(datakeys).length;
      console.log(m);

      return this.modules.filter(module => {
        return module["ModuleCode"].match(this.search.toUpperCase());
      });
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

#show-modules {
  max-width: 800px;
  margin: 0 auto;
}

.single-module {
  padding: 20px;
  margin: 20px 0;
  box-sizing: border-box;
  background: #eee;
}
</style>
