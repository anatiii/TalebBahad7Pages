<template>
    <div id="home_page">
        <h2 id="home_titles">מסך בית </h2>
      <div id="button_container">
        <p class="episode" id="0"  @click="switchScreen" >אחריות המפקדות<br/>פרק 1</p>
        <p class="episode" id="1"   @click="switchScreen" >מערכת האיכות <br/> פרק 2</p>
        <p class="episode" id="2"   @click="switchScreen" > סגלי ההדרכה <br/> פרק 3</p>
        <p class="episode" id="3"   @click="switchScreen" >פיתוח הדרכה <br/> פרק 4</p>
        <p class="episode" id="4"  @click="switchScreen" >ניהול קורס  <br/>פרק 5א</p>
        <p class="episode" id="5"  @click="switchScreen" >ניהול חניכים <br/> פרק 5ב</p>
        <p class="episode" id="6"   @click="switchScreen" >הערכת הדרכה <br/> פרק 6</p>
        <p class="episode" id="7 "   @click="switchScreen" >ניהול המידע ההדרכתי <br/>פרק  7</p>
      </div>
      <div id="reminder_card">
        <div id="close_card" @click="tableReminder">x</div>
      </div>
      <img src="../assets/envelope.svg" alt="envelope" id="reminder" @click="tableReminder">
    </div>
  </template>


<script>

export default{
  name: "taleb-pages",
  data() {
    return {
    }
},
  methods: {
    switchScreen(event) {
      this.$emit("picked-subject", event.target.id);
      this.$emit("curr-page", 3);
    },
    
    tableReminder(name){
      if(name.target.id === "reminder"){
        document.getElementById("reminder_card").style.cssText="display: block;"
      }
      else if(name.target.id === "close_card"){
        document.getElementById("reminder_card").style.cssText="display: none;"
      }
    }
  },

}

</script>


<style scoped>
#home_page{
  position: absolute;
  height: 100%;
  width: 100%;
  display: block;
}

#home_titles{
  position: absolute;
  height: 10%;
  width: 60%;
  left: 21%;
  font-weight: 700;
  font-size: 5vh;
  color: white;
  font-family: myFirstFont;
}

#button_container{
  position: absolute;
  height: 60%;
  width: 85%;
  top: 15%;
  left: 8%;
  display: flex;
  flex-wrap: wrap;
  flex-flow: column wrap;
  align-items: center;
}

#reminder{
  position: absolute;
  height: 10%;
  width: 15%;
  bottom: 6%;
  left: 3%;
}

.episode{
  position: relative;
  height: 16%;
  width: 42%;
  color: white;
  font-weight: 500;
  font-size: 2.1vh;
  background-color:#4fb0fac8;
  border-radius: 10%;
  cursor: pointer;
  font-family: assistentReg;
}

#reminder_card{
  position: absolute;
  height: 55%;
  width: 75%;
  background-color: bisque;
  top: 14%;
  left: 13%;
  animation: cardAnimation 2s ease-in;
  display: none;
}

#close_card{
  position: absolute;
  height: 8%;
  width: 10%;
  right: 0%;
  font-size: 2.2vh;
  font-weight: 500;
}

@keyframes cardAnimation {
  0%{
    transform: rotate(0deg);
    height: 15%;
    width: 25%;
  }
  100%{
    transform: rotate(360deg);
    height: 55%;
    width: 75%;
  }
}

</style>