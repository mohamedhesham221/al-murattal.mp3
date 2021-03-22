<template>
  <div>
    <button @click="toTop" id="top" :class="{ displayTopBtn: showBtn }">
      <i class="fas fa-angle-double-up"></i>
    </button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      showBtn: ""
    };
  },
  created() {
    window.addEventListener("scroll", this.handleScroll);
    // console.log("created");
  },
  destroyed() {
    window.removeEventListener("scroll", this.handleScroll);
  },
  methods: {
    toTop() {
      window.scrollTo({
        top: 0,
        behavior: "smooth"
      });
    },
    handleScroll() {
      if (window.scrollY > 200) {
        this.showBtn = true;
      } else {
        this.showBtn = false;
      }
    }
  }
};
</script>
