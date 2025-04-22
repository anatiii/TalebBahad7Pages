<template>
  <div id="welcome_page">
    <div id="first_page">
    <p id="welcome_title">ברוכים הבאים לתל"ב</p>
    <img src="../assets/startButton.svg" alt="startButton" id="start_button" @click="startPage"/>
    <img src="../assets/readingLady.svg" alt="readingLady" id="reading_lady"/>
  </div>
  <div id="sec_page">
    <h2 id="titles">טיפה הסבר</h2>
    <p id="explain">תל"ב = תקן לאיכות בהדרכה <br/><br/> התל"ב מחולק לשמונה נושאים עיקריים: <br/><br/> אחריות המפקדות, מערכת האיכות, סגלי ההדרכה, <br> פיתוח הדרכה, ניהול קורס, ניהול חניכים, הערכת הדרכה וניהול המידע ההדרכתי.</p>
    <img src="../assets/nextButton.svg" alt="nextButton" id="next_button" @click="startPage"/>
    <img src="../assets/readingBoy.svg" alt="readingBoy" id="reading_boy"/>
    <div id="instrucions">
      <p id="ins_one" class="follow_ups">במסך הבית תמצאו שמונה כפתורים אשר יובילו אתכם לחומר <br/> שאתם צריכים</p>
      <p id="ins_two" class="follow_ups">לאחר בחירת פרק תופיע רשימת הנהלים, לחצו על כותרת הנוהל אשר תרצו ללמוד</p>
      <p id="ins_three" class="follow_ups">בכל שלב תוכלו לחזור למסך הבית על ידי לחיצה על הספר<br/>שבתחתית העמוד </p>
    </div>
  </div>
  </div>
</template>


<script>
export default {
  name: "welcome-page",
  data() {
    return {
      nextPage: 0,
      titleImg: 1,
    };
  },
  methods: {
    startPage(){
      this.nextPage = this.nextPage + 1;
      if (this.nextPage == 1){
        document.getElementById("first_page").style.display = "none";
        document.getElementById("sec_page").style.display = "block";
      } else if (this.nextPage == 2){
        document.getElementById("titles").innerText = "הוראות";
        document.getElementById("instrucions").style.display = "block";
        document.getElementById("explain").style.display = "none";
      }else if (this.nextPage == 3){
        this.$emit("curr-page", 2);
      }
    }
  }
}
</script>

<style scoped>
#welcome_page{
  position: absolute;
  height: 100%;
  width: 100%;
  display: block;
}

#first_page{
  position: absolute;
  height: 100%;
  width: 100%;
}

#start_button{
  position: absolute;
  top: 45%;
  right: 25%;
  height: 20%;
  width: 50%;
}

#welcome_title{
  position: absolute;
  height: 18%;
  width: 70%;
  left: 15%;
  top: 18%;
  font-weight: 700;
  font-size: 5vh;
  color: white;
  font-family: myFirstFont;
}

#reading_lady{
  position: absolute;
  bottom: 0%;
  height: 26%;
  width: 60%;
  right: 0%;
}

#reading_boy{
  position: absolute;
  bottom: 7%;
  height: 22%;
  width: 40%;
  left: 0%;
}

#sec_page{
  display: none;
}

#next_button{
  position: absolute;
  height: 8%;
  width: 15%;
  bottom: 19%;
  left: 44%;
}

#titles{
  position: absolute;
  height: 10%;
  width: 60%;
  left: 20%;
  top: 3%;
  font-weight: 700;
  font-size: 5vh;
  color: white;
  font-family: myFirstFont;
}

#explain{
  position: absolute;
  direction: rtl;
  height: 50%;
  width: 85%;
  font-weight: 700;
  font-size: 3vh;
  color: rgb(0, 0, 0);
  top: 13%;
  left: 8%;
  font-family: myFirstFont;
}

#instrucions{
  position: absolute;
  height: 50%;
  width: 90%;
  top: 18%;
  left: 5%;
  display: none;
  font-weight: 500;
  font-size: 2.1;
}

.follow_ups{
  position: absolute;
  height: 22%;
  width: 95%;
  color: white;
  left: 1%;
  border-radius: 25px;
  font-weight: 500;
  font-size: 2.3vh;
  color: white;
  text-align: center;
  font-family: assistentReg;
}


#ins_one{
  border: 5px solid rgba(227, 22, 22, 0.751);
  top: 0%;
}

#ins_two{
  border: 5px solid rgb(64, 244, 109);
  top: 35%;
}

#ins_three{
  border: 5px solid  rgb(255, 242, 101);
  top: 70%;
}
</style>

