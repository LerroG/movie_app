<template>
  <div></div>
</template>

<script>
import { mapGetters } from "vuex";

export default {
  name: "NotificationToast",
  computed: {
    ...mapGetters(["messagePool"]),
  },
  watch: { messagePool: "showNotify" },
  methods: {
    showNotify({ variant, msg, title }) {
      this.$bvToast.toast(msg, {
        title,
        variant,
        solid: true,
      });
    },
  },
};
</script>

<style></style>
