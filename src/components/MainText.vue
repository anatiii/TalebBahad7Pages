<template>
  <div id="main_text">
    <div id="back_button" @click="backButton"></div>
    <div id="next_page_button" @click="nextButton"></div>
    <div id="next_chapter" @click="nextChapter">לעבור לפרק הבא</div>
    <div id="last_chapter" @click="lastChapter">לפרק הקודם</div>
    <div id="first_chapter">זה הפרק הראשון</div>
    <div id="final_chapter">זה הפרק האחרון</div>
    <h3 id="inner_title">{{ this.nameTitle }}</h3>
    <div id="study">
      <div id="real_study_text" v-html="currentText"></div>
    </div>
  </div>
</template>

<script>
import contentData from "../assets/content.json";

export default {
  name: "main-text",
  props: ["subjectsName", "subNumber", "innerPart", "nameTitle"],
  data() {
    return {
      array: contentData,
      choosen: this.subNumber,
      i: this.innerPart,
      j: 0,
      graphicsArray: [[]],
    };
  },
  computed: {
    currentText() {
      return this.array[this.choosen]?.[this.i]?.[this.j] || "";
    },
  },
  methods: {
    startPage() {
      this.$emit("curr-page", 2);
    },

    backButton() {
      document.getElementById("next_page_button").style.display = "block";
      document.getElementById("first_chapter").style.display = "none";
      document.getElementById("next_chapter").style.display = "none";
      document.getElementById("final_chapter").style.display = "none";
      if (this.j > 0) {
        this.j = this.j - 1;
      } else if (this.j <= 0) {
        this.lastChapter();
      }
    },

    nextButton() {
      document.getElementById("back_button").style.display = "block";
      document.getElementById("first_chapter").style.display = "none";
      document.getElementById("last_chapter").style.display = "none";


      if (this.array[this.choosen][this.i][this.j + 1] === undefined) {
        if (this.array[this.choosen][this.i + 1] === undefined) {
          document.getElementById("final_chapter").style.display = "block";
          document.getElementById("next_page_button").style.display = "none";
        } else {
          document.getElementById("next_chapter").style.display = "block";
          document.getElementById("next_page_button").style.display = "none";
        }
      } else {
        document.getElementById("next_page_button").style.display = "block";
        this.j = this.j + 1;
      }
    },

    nextChapter() {
      console.log(this.i);

        this.$emit("make-progress", this.i);
        this.i = this.i + 1;
        this.j = 0;
        document.getElementById("next_page_button").style.display = "block";
        document.getElementById("next_chapter").style.display = "none";
    },

    lastChapter() {
      console.log("hi");

      if (this.i === 0) {
        console.log("hello");
        document.getElementById("back_button").style.display = "none";
        document.getElementById("first_chapter").style.display = "block";
      } else {
        this.$emit("made-progress", this.i);
        this.i--;
        this.j = 0;
        document.getElementById("last_chapter").style.display = "none";
        document.getElementById("back_button").style.display = "block";
      }
    },
  },
};
</script>

<style scoped>
#main_text {
  background-image: url("../assets/textBackground.svg");
  background-size: cover;
  background-repeat: no-repeat;
  visibility: visible;
}

#study {
  position: absolute;
  width: 100%;
  height: 90%;
  cursor: pointer;
  bottom: 10%;
  direction: rtl;
  color: white;
}

#real_study_text {
  position: absolute;
  direction: rtl;
  width: 95%;
  height: 85%;
  line-height: 2;
  top: 10%;
  right: 2%;
  font-size: 3.8vw;
  font-family: assistentReg;
}

#back_button {
  position: absolute;
  background-image: url("../assets/nextPageButton.svg");
  background-size: contain;
  background-repeat: no-repeat;
  width: 15%;
  height: 7%;
  bottom: 2%;
  right: 2%;
}

#next_page_button {
  position: absolute;
  background-image: url("../assets/nextPageButton.svg");
  background-size: contain;
  background-repeat: no-repeat;
  width: 15%;
  height: 7%;
  bottom: 2%;
  left: 2%;
  transform: rotate(180deg);
}

#next_chapter {
  position: absolute;
  width: 30%;
  height: 10%;
  bottom: 0%;
  left: 2%;
  cursor: pointer;
  display: none;
  color: white;
}

#last_chapter {
  position: absolute;
  width: 30%;
  height: 10%;
  bottom: 0%;
  right: 2%;
  cursor: pointer;
  display: none;
  color: white;
}

#first_chapter {
  position: absolute;
  width: 30%;
  height: 10%;
  bottom: 0%;
  right: 2%;
  cursor: pointer;
  display: none;
  color: white;
}

#final_chapter {
  position: absolute;
  width: 30%;
  height: 10%;
  bottom: 0%;
  left: 2%;
  cursor: pointer;
  display: none;
  color: white;
}

#inner_title {
  position: absolute;
  height: 10%;
  width: 100%;
  color: white;
  font-weight: 700;
  font-size: 4vw;
  direction: rtl;
  right: 0%;
  top: -2%;
  font-family: myFirstFont;
}
</style>
