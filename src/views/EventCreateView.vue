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
  min-height: 100vh;
  height: max-content;

  display: flex;
  justify-content: center;
  align-items: center;
}
/* ---------------------------------------------------------------- */
</style>
