<template>
  <div class="quran_list">
    <div class="list_head">
      <form @submit.prevent id="search_form">
        <span id="input_contain">
          <input
            type="text"
            id="search_input"
            v-model="search"
            placeholder="البحث بأسم السورة . . ."
          />
        </span>
      </form>
      <div class="surah_details" :class="{ displayDetails: show }">
        <p v-text="mainSurah" class="surah_name"></p>
        <img
          :src="imageSrc"
          :title="imageTitle"
          alt="reciter"
          id="reciter_img"
        />
        <p class="reciter_name">
          <q>{{ mainTitle }}</q>
        </p>
      </div>
      <audio
        controls
        autoplay
        :key="src"
        class="audio"
        :class="{ displayAudio: show }"
      >
        <source :src="src" type="audio/mp3" />
      </audio>
    </div>
    <ul class="surahs_list">
      <li class="surah_item" v-for="surah in filteredSurahs()" :key="surah.id">
        <span class="arabic_name">{{ surah.arabic_name }}</span> <br />
        <q class="english_name">
          <span>&nbsp;{{ surah.english_name }}&nbsp;</span>
        </q>
        <br />
        <div class="group_buttons">
          <div class="down_arrow" @click="surah.reciter = !surah.reciter">
            <span class="choose_reciters"> أختر مقرئ</span
            ><i class="fas fa-caret-down"></i>
          </div>
          <ul class="reciter_group" :class="{ displayReciters: surah.reciter }">
            <li
              class="reciter_item"
              @click="
                src = surah.abdelbasitUrl;
                show = true;
                mainTitle = titleBasit;
                mainSurah = surah.arabic_name;
                surah.reciter = !surah.reciter;
                imgTitleBasit();
              "
            >
              {{ titleBasit }}
            </li>
            <li
              class="reciter_item"
              @click="
                src = surah.elsudisUrl;
                show = true;
                mainTitle = titleSudis;
                mainSurah = surah.arabic_name;
                surah.reciter = !surah.reciter;
                imgTitleSudis();
              "
            >
              {{ titleSudis }}
            </li>
            <li
              class="reciter_item"
              @click="
                src = surah.elajimUrl;
                show = true;
                mainTitle = titleAjim;
                mainSurah = surah.arabic_name;
                surah.reciter = !surah.reciter;
                imgTitleAjim();
              "
            >
              {{ titleAjim }}
            </li>
          </ul>
        </div>
      </li>
    </ul>
    <br />
  </div>
</template>

<script>
import data from "../assets/json/DATA.json";
export default {
  name: "play-list",
  data() {
    return {
      search: "",
      surahs: [],
      src: "",
      show: false,
      titleAjim: "أحمد العجمي",
      titleBasit: "عبد الباسط عبد الصمد",
      titleSudis: "عبد الرحمن السديس",
      mainTitle: "",
      mainSurah: "",
      imageSrc: "",
      imageTitle: "",
      srcBasit: require("../assets/abdelbasit.png"),
      srcSudis: require("../assets/sudis.png"),
      srcAjim: require("../assets/ajim.png")
    };
  },
  created() {
    this.surahs = data;
    let surahs = this.surahs;
    surahs.forEach(item => {
      this.$set(item, "reciter", false);
    });
  },
  methods: {
    filteredSurahs() {
      if (this.search) {
        let findSurah = new RegExp(this.search, "i");
        return this.surahs.filter(surah => surah.arabic_name.match(findSurah));
      } else {
        this.surah = [];
      }
    },
    imgTitleBasit() {
      this.imageTitle = this.titleBasit;
      this.imageSrc = this.srcBasit;
    },
    imgTitleSudis() {
      this.imageTitle = this.titleSudis;
      this.imageSrc = this.srcSudis;
    },
    imgTitleAjim() {
      this.imageTitle = this.titleAjim;
      this.imageSrc = this.srcAjim;
    }
  }
};
</script>
