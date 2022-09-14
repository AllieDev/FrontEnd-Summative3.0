<template>
  <div class="view">
    <div class="search-event__mobile">
      <div class="search-event__container">
        <h3>Find Events</h3>
        <select name="type-of-events" id="search-events">
          <option selected value="all-events">All Events</option>
          <option value="concerts">Concerts</option>
          <option value="exhibitions">Exhibitions</option>
          <option value="festivals">Festivals</option>
          <option value="sports">Sports</option>
          <option value="workshop">Workshop</option>
          <option value="conferences">Conferences</option>
        </select>
      </div>
    </div>

    <div class="event-list__container">
      <div class="event-list__event-cards">
        <h3 class="event-list__header">All Events</h3>
        <global-event-list
          @sendEventData="sendEventData"
          v-for="event in eData"
          :eData="event"
          :key="event._id"
        />
      </div>
    </div>
  </div>
</template>

<script>
import GlobalEventList from "../components/GlobalEventList.vue";
export default {
  components: { GlobalEventList },
  data() {
    return {};
  },
  props: ["eData"],
  methods: {
    sendEventData(data) {
      this.$emit("specificEventDetail", data);
    },
  },
  computed: {},
  watch: {},
  created() {
    this.$emit("visibleNav");
    this.$emit("visibleSearchInput");
  },
};
</script>

<style scoped>
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
.search-event__container {
  display: flex;
  align-items: center;
  justify-content: flex-end;
  max-width: 1200px;
  margin: auto;
  margin-top: 9rem;
  /* border: solid 1px #000; */
}

.search-event__container h3 {
  font-family: "Anton", sans-serif;
  text-transform: uppercase;
}

.search-event__container select {
  width: 25%;
  margin-left: 3rem;
  padding: 0.6rem 1rem;
  text-transform: uppercase;
  letter-spacing: 0.1rem;
}

.navbar__help-icon {
  visibility: hidden;
}

.event-list__container {
  display: flex;
  justify-content: center;
  align-items: center;
  max-width: 1200px;
  margin: auto;
  margin-bottom: 10rem;
  /* border: solid 1px greenyellow; */
}

.event-list__event-cards {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 10rem;
  margin-top: 10rem;
  max-width: 1100px;
  position: relative;
  /* border: solid 1px blue; */
}

.event-list__header {
  position: absolute;
  top: -50px;
  left: 0;
  text-transform: uppercase;
}

/* Landscape Tablet to Small Laptop 848px ~ 1403px */
@media only screen and (max-width: 1403px) {
  .search-event__container {
    margin: 9rem 15rem 8rem;
  }
  .search-event__container select {
    width: 30%;
  }
}
/* Landscape Mobile to Portrait Tablet 404px ~ 847px */
@media only screen and (max-width: 847px) {
  .search-event__mobile {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin: 5rem 5rem 0rem;
  }

  .navbar__help-icon {
    visibility: visible;
    padding: 0.8rem 1.25rem;
    border: solid 1px #000;
    border-radius: 30px;
    cursor: pointer;
  }
  .search-event__container {
    margin: 8rem 0rem 8rem;
  }
  .search-event__container select {
    width: 50%;
  }
  .event-list__event-cards {
    grid-template-columns: repeat(1, minmax(0, 1fr));
  }
}

/* Portrait Mobile 0px ~ 414px */
@media only screen and (max-width: 414px) {
  .search-event__mobile {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin: 5rem 2rem 0rem;
  }

  .search-event__container {
    justify-content: flex-start;
  }
  .search-event__container h3 {
    font-size: 1.6rem;
  }

  .search-event__container select {
    width: 50%;
    margin-left: 1rem;
    padding: 0.6rem 0.7rem;
  }

  .event-list__event-cards {
    max-width: 320px;
  }
  .event-list__header {
    font-size: 1.5rem;
  }
}
</style>
