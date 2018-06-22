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
    <p>tell me:{{herwords}}</p>
    <HelloWorld fathermsg="i love you" v-on:tell-me="listentoher"></HelloWorld>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld'
import Store from './store.js'
console.log(Store)

export default {
  name: 'App',
  data (){
    return {
      msg: 'this is my first vue',
      lists: Store.fetch(),
      newItem:"",
      herwords:''
    }
  },
  watch:{
    lists:{
      handler:function(lists){
        Store.save(lists)
      },
      deep:true //深层赋值
    }
  },
  methods:{
    toggleList:function(list){
      list.isFinished=!list.isFinished
    },
    addNew:function(){
        this.lists.push({
          label:this.newItem,
          isFinished:false,
        })
      this.newItem=""
      },
    listentoher:function(msga){
      this.herwords=msga
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
