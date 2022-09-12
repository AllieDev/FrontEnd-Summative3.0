<template>
  <div class="view"></div>
</template>

<script>
export default {
  components: {},
  data() {
    return {};
  },
  props: [],
  methods: {},
  created() {
    this.$emit("unvisibleNav");
  },
};
</script>

<style scoped>
/* ---------------------------------------------------------------- */
.view {
  height: 100vh;
  /* background-color: rgb(196, 173, 230); */

  display: flex;
  justify-content: center;
  align-items: center;
}
/* ---------------------------------------------------------------- */
</style>
