<template>
  <div id="app">
    <img src="./assets/pumaIcon.svg" alt="pumaicon" id="puma_icon"/>
    <img src="./assets/Bahad_7_tag_from_2023.svg.png" alt="bahad7icon" id="bahad_7_icon"/>
    <welcome-page
      v-if="showPage === 1"
      @curr-page="switchScreen"
    ></welcome-page>
    <home-page
      v-if="showPage === 2"
      @curr-page="switchScreen"
      @picked-subject="subjectSwitch"
    ></home-page>
    <sub-num  v-if="showPage === 3" @curr-page="switchScreen" :subNumber="pickedNumber"></sub-num>
  </div>
</template>

<script>
import WelcomePage from "./components/WelcomePage.vue";
import HomePage from "./components/HomePage.vue";
import SubNum from './components/SubNum.vue';

export default {
  name: "taleb-pages",
  data() {
    return {
      showPage: 1,
      pickedNumber: 0,
    };
  },
  components: {
    WelcomePage,
    HomePage,
    SubNum,
  },
  methods: {
    switchScreen(pageNum) {
      this.showPage = pageNum;
    },

    subjectSwitch(subName) {
      this.pickedNumber = `${subName}`;
      console.log(this.pickedNumber);
  
      }
    },
  }
</script>

<style>
* {
  height: 92vh;
  width: 100vw;
  overflow: hidden;
  position: fixed;
}

@font-face {
    font-family: myFirstFont;
    src: url('./assets/font/SecularOne-Regular.ttf');
}

@font-face {
    font-family: assistentReg;
    src: url('./assets/font/assistant/Assistant-Regular.ttf');
}


#app{
  margin: 0;
  padding: 0;
  top: 0;
  background-image: url("./assets/cleanBackground.jpg");
  background-size: cover;
  background-repeat: no-repeat;
}

body {
    margin: 0;
    padding: 0;
}

#puma_icon{
  position: absolute;
  height: 9%;
  width: 17%;
  left: 2%;
  top: 0.5%;
}

#bahad_7_icon{
  position: absolute;
  height: 8%;
  width: 13%;
  right: 2%;
  top: 1%;
}


</style>
