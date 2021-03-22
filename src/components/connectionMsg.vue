<template>
  <div>
    <div
      class="connection"
      :class="[{ isTrue: showMsg }, { isFalse: !showMsg }]"
    >
      <p class="connection_msg" v-text="msg"></p>
    </div>
  </div>
</template>
<script>
export default {
  name: "connection",
  data() {
    return {
      showMsg: false,
      msg: ""
    };
  },
  created() {
    window.addEventListener("online", this.connectHandle);
    window.addEventListener("offline", this.connectHandle);
  },
  methods: {
    connectHandle() {
      if (navigator.onLine) {
        this.showMsg = !this.showMsg;
        this.msg = "online";
      } else {
        this.showMsg = !this.showMsg;
        this.msg = "your are offline, please go online";
      }
    }
  }
};
</script>
