<template>
  <div id="app">
    <img src="./assets/logo.png">
    <h1 v-text="msg"></h1>
    <input v-model="newItem" v-on:keyup.enter="addNew">
    <ul>
      <li v-for="list in lists" v-bind:class="{finished:!list.isFinished}" v-on:click="toggleList(list)">
        {{list.label}}
      </li>
    </ul>
    <HelloWorld/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld'

export default {
  name: 'App',
  data (){
    return {
      msg: 'this is my first vue',
      lists: [],
      newItem:""
    }
  },
  methods:{
    toggleList:function(list){
      list.isFinished=!list.isFinished
    },
    addNew:function(){
      console.log(this.newItem),
        this.lists.push({
          label:this.newItem,
          isFinished:false,
        })
      this.newItem=""
    }
  },
  components: {
    HelloWorld
  }
}
</script>

<style>
  .finished{
    text-decoration:underline;
  }
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
