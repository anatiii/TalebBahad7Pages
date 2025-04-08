<template>
  <div id="sub_num">
    <main-text
      v-if="showPlaces === 1"
      id="main_text"
      :subNumber="i"
      :innerPart="innerSub"
      :nameTitle="nameTitle"
      @make-progress="nextChapter"
      @made-progress="lastChapter"
    ></main-text>
    <div id="text_container" v-if="showPlaces === 0">
      <div
        id="sub_text_list"
        v-for="(j, index) in optionArray[i]"
        :key="index"
        @click="updateSelected(index)"
        class="list-group-item"
      >
        {{ optionArray[i][index] }}
      </div>
    </div>
        <div id="home_click"  @click="startPage"></div>
  </div>
</template>

<script>
import MainText from "./MainText.vue";

export default {
  name: "sub-num",
  props: [ "subNumber"],
  data() {
    return {
      optionArray: [
        ['יחסי הגומלין בין המפקדה הממונה לבסיס ההדרכה (בה"ד) 1.1', 'יחסי הגומלין בין הבה"ד ליחידות הקולטות (שטח)1.2', 'יחסי הגומלין בין מסגרות ההדרכה למטה הבה"ד1.3', 'גיבוש תוכנית עבודה שנתית1.4', 'גיבוש תוכנית עבודה שנתית לפיתוח הדרכה1.5', 'תכנון שנתי לקליטת סגלי הדרכה ברמת המסגרת הענף1.6', 'תהליך כניסה לתפקיד וחפיפת בעלי תפקיד1.7', 'פורום הדרכה בהדי1.8', 'תפיסת ההדרכה1.9'],
        ['הגדרת בעלי התפקידים לניהול מערך התלב2.1', 'ועדת היגוי ייעודית לנושא התלב2.2', 'פורום נאמני תלב2.3', 'מבדקי תלב פנימיים וחיצוניים2.4', 'טיפול בפנייה בנושא הדרכתי2.5', 'טיפול באירוע הדרכתי חריג2.6', 'נוהל תלב2.7', 'תיק נהלי תלב2.8', 'בקרת תיעוד2.9'],
        ['הגדרת תפקידי סגל הדרכה3.1', 'איתור סגלי הדרכה ומיונם3.2', 'שיבוץ סגלי הדרכה3.3', 'קליטה הכשרה והסמכה של סגלי הדרכה3.4', 'מסלול קידום סגלי הדרכה3.5', 'פיתוח סגלי הדרכה ושמירה על כשירותם3.6', 'חניכת סגלי הדרכה3.7', 'תהליך הערכה של איש סגל הדרכה3.8', 'הרחקת איש סגל3.9', 'בחירת אנשי סגל מצטיינים 3.10', 'מעקב אחר התיק האישי של סגלי הדרכה וניהולו3.11'],
        ['אבחון פערים ומיפוי צרכים הדרכתיים4.1', 'ועדת צרכים לפיתוח הדרכה4.2', 'פיתוח הכשרות ומסלולים4.3', 'הסמכת בעלי תפקידים4.4', 'אישור תיק יסוד4.5', 'תיקוף קורס4.6', 'פיתוח מבחנים ותיקופם4.7', 'פיתוח אמצעי הדרכה ועזרי אימון והטמעתם4.8'],
        ['הערכות לפתיחת קורס5.1א', 'הכנת סגל5.2א', 'העברת מבחנים ותיקופם5.3א', 'סיכומים עיתיים במהלך הקורס5.4א', 'סיכום קורס5.5א'],
        ['תהליך קליטת חניך לקורס5.1ב', 'חניכה במהלך קורס5.2ב', 'מעקב אחר חניך וניהול תיק אישי5.3ב', 'טיפול בפניות חניכים5.4ב', 'טיפול בחניך מתקשה 5.5 ב', 'הרחקת חניך 5.6ב', 'בחירת חניך מצטיין וחניך למופת 5.7ב', 'העברת בוגר קורס ליחידה קולטת - העברת מקל 5.8 ב', 'מניעת חופשה 5.9 ב', 'טיפול בפניות הורים 5.10 ב', 'טיפול בחניכים במהלך שעות מנוחה רפואית 5.11 ב'],
        ['תפיסת הערכה בבהד -6.1', '6.2 הערכת מחזור קורס', 'תהליכי הערכה,כלי הערכה ומדדים- 6.3', 'תהליכים וכלים 6.4'],
        ['תפיסת ניהול המידע ההדרכתי- 7.1', 'מבנה עץ המידע ההדרכתי - 7.2', 'בעלי תפקידים במערכת ניהול המידע ההדרכתי - 7.3']

      ],
      img: `/src/assets/symbols/subjects/${this.subNumber}.svg`,
      i: this.subNumber,
      showPlaces: 0,
      innerSub: "",
      nameTitle: "",
      saver: "",
    };
  },

  components: {
    MainText,
  },

  methods: {
    startPage(event) {
      if (this.showPlaces === 1) {
        this.showPlaces = 0;
      } else {
        if (event.target.id === "home_click") {
          this.$emit("curr-page", 2);
        }
      }
    },

    updateSelected(selectedPart) {
      console.log(this.optionArray[this.i][selectedPart]);
      this.nameTitle = this.optionArray[this.i][selectedPart];
      this.saver = selectedPart;
      this.innerSub = selectedPart;
      this.showPlaces = 1;
      document.getElementById("text_container").style.visibility = "hidden";
    },

    nextChapter(count) {
      this.nameTitle = this.optionArray[this.i][count + 1];
    },
    lastChapter(count) {
      this.nameTitle = this.optionArray[this.i][count - 1];
    },
  },
};
</script>

<style>
#sub_num {
  
  display: block;
}

#main_text {
  position: absolute;
    width: 85%;
    height: 70%;
    top: 13%;
    left: 8.3%;
}

#text_container {
  position: absolute;
  width: 90%;
  height: 75%;
  top: 11%;
  left: 6%;
  background-image: url("../assets/textBackground.svg");
  background-size: cover;
  background-repeat: no-repeat;
  visibility: visible;
  text-align: center;
}

#sub_text_list {
  height: 8%;
  width: 100%;
  top: 2%;
  border-radius: 25px;
  text-align: center;
  position: relative;
  text-decoration: underline;
}

.list-group-item {
  direction: rtl;
  text-decoration: none;
  font-weight: 1000vw;
  font-size: 3.3vw;
  color: white;
  cursor: pointer;
}

#titles {
  position: absolute;
  height: 100%;
  width: 30%;
  right: 34%;
}

#home_click {
  position: absolute;
  background-image: url("../assets/symbols/HomeSymbol.svg");
  background-repeat: no-repeat;
  background-size: contain;
  width: 10%;
  height: 45%;
  left: 44%;
  bottom: 50%;
  cursor: pointer;
}

#bottom_part {
    position: absolute;
    width: 100dvw;
    height: 14dvh;
    top: 86dvh;   
}

#home_click {
    position: absolute;
    background-image: url("../assets/book.svg");
    background-repeat: no-repeat;
    background-size: contain;
    width: 40%;
    height: 10%;
    left: 31%;
    bottom: 0%;
    cursor: pointer;
}
</style>
