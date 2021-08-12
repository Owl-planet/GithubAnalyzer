<template>
  <div id="app">
    <app-header @CP="selectedComponent = $event"></app-header>
    <keep-alive>
          <component @CP="selectedComponent = $event" :is="selectedComponent"></component>
    </keep-alive>
    <app-footer></app-footer>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue';
import About from "./components/About.vue";
import Footer from "./components/Footer.vue";
import Header from "./components/Header.vue";
import Section from "./components/Section.vue";
import ag from "./components/ag.vue";

export default {
  name: 'App',
  data : function(){
      return {
          selectedComponent : "app-section"
      }
  },
  components: {
    HelloWorld,
    appFooter : Footer,
    appHeader : Header,
    appSection: Section,
    appAbout: About,
    appAg: ag
  }
}
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Nunito:wght@300&display=swap");
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  background-color: #24252a;
}
</style>
