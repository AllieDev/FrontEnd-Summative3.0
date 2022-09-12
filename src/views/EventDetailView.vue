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
    this.$emit("visibleNav");
    this.$emit("unvisibleSearchInput");
  },
};
</script>

<style scoped>
/* ---------------------------------------------------------------- */
.view {
  height: calc(100vh - 100px);
  overflow: hidden scroll;
}
@media screen and (max-width: 800px) {
  .view {
    height: calc(100vh - 70px);
  }
}
/* ---------------------------------------------------------------- */
</style>
