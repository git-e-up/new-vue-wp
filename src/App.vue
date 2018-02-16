<template>
  <div id="app">
    <img src="./assets/logo.png">
    <ul class="main-nav">
      <li class="main-nav__item" ref="mainnavitem" v-for="(item, index) in items" :key="index" v-html="item.message" :data-postIndex="index+2" v-on:click="bounce">
      </li>
    </ul>
    <div class="ssl-warning" v-bind:class="{ active: isActive }">
      <p>Sorry, I didn't want to pay godaddy $75 for SSL so you'll need to allow your browser from unauthenticated sources</p>
    </div>
    <div class="col-xs-12 text-center info">
      <transition name="slide-fade">
        <h1 class="init-header" v-if="show">{{ introMessage }}</h1>
      </transition>
    </div>
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'


export default {
  name: 'app',
  components: {
    HelloWorld
  },
  data: function() {
    return{
      items: [],
      isActive: false,
      show: true,
      introMessage:  'Hiyo'
    }
  },
  mounted: function(){
    this.$http.get('http://matthewlissner.com/wp-json/wp/v2/hot_sauces?filter[orderby]=date&order=asc').then(response => {
      let x = this;
      response.body.forEach(function(val){
        x.items.push({message: val.title.rendered})
      })
    }, () => {
      console.log('sorry about that');
      this.isActive = true;
      // error callback
    });
  },
  methods: {
    begin: function () {
      setTimeout(() => {
        let elements = document.getElementsByClassName('main-nav__item');
        elements[0].classList.add('main-nav__item--bouncing');
        console.log(elements[0].innerHTML);
        this.introMessage = this.items[0].message;
      }, 1000);
    },
    bounce: function (event) {
      this.$refs.mainnavitem.forEach(function(val){
        val.classList.remove('main-nav__item--bouncing');
      })
      event.target.classList.add('main-nav__item--bouncing');
      this.introMessage = event.target.innerHTML;
    }
  },
  updated(){
     this.begin()
  },

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
</style>
