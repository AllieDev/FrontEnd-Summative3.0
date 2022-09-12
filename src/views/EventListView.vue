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
  computed: {},
  watch: {},
  created() {
    this.$emit("visibleNav");
    this.$emit("visibleSearchInput");
  },
};
</script>

<style scoped>
/* ---------------------------------------------------------------- */
.view {
  height: calc(100vh - 100px);
  overflow: hidden scroll;
  /* background-color: rgb(173, 230, 200); */
}
@media screen and (max-width: 800px) {
  .view {
    height: calc(100vh - 70px);
  }
}
/* ---------------------------------------------------------------- */
</style>
