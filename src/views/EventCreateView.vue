<template>
  <div class="event">
    <div class="event__container">
      <h3 class="event__header">Create Event</h3>
      <form class="event__form" action="./events">
        <div>
          <label class="event__label" for="title">Title</label>
          <input
            v-model="eventTitle"
            type="text"
            id="title"
            name="title"
            required
          />
        </div>
        <div>
          <label class="event__label" for="location">Location</label>
          <input
            v-model="eventLocation"
            type="text"
            id="location"
            name="location"
            required
          />
        </div>
        <div>
          <label class="event__label" for="date">Date</label>
          <input
            v-model="eventDate"
            type="date"
            id="date"
            name="date"
            required
          />
        </div>
        <div>
          <label class="event__label" for="time">Time</label><br />
          <input
            v-model="eventTime"
            type="time"
            id="time"
            name="time"
            required
          />
        </div>
        <div class="mobile">
          <label class="event__label" for="description">Description</label
          ><br />
          <textarea
            class="event__description"
            v-model="eventDescription"
            rows="4"
            cols="50"
            required
          ></textarea>
        </div>
        <button href="#">PUBLISH</button>
      </form>
    </div>
    <div class="event__conatinerTwo">
      <img src="#" class="event__photo" alt="" />
      <label for="myfile">Select a Photo</label>
      <input type="file" id="myfile" name="myfile" />
      <!-- ---------------------------------------------------------------- -->
      <div class="desktop">
        <label class="event__label" for="description">Description</label><br />
        <textarea
          class="event__description"
          v-model="eventDescription"
          rows="4"
          cols="50"
          required
        ></textarea>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      eventTitle: null,
      eventLocation: null,
      eventDate: null,
      eventTime: null,
      eventDescription: null,
      imageFile: "",
      imageFileUrl: "",
    };
  },
  props: [],
  methods: {},
  watch() {},
  created() {
    this.$emit("unvisibleNav");
  },
};
</script>
<style scoped>
.view {
  min-height: 100vh;
  height: max-content;

  display: flex;
  justify-content: center;
  align-items: center;
}
.event {
  display: grid;
  grid-template-columns: 1fr 3fr;
  grid-template-rows: 1fr;
  grid-template-areas: "event__container event__containerTwo";

  text-transform: uppercase;
  background-color: white;
  box-shadow: 6px 10px 8px #00000022;
  width: 1200px;
  min-height: max-content;

  /* flex-wrap: wrap; */

  /* border: 5px solid rgb(255, 85, 0); */
}

.event__container {
  grid-area: event__container;
  padding: 20px;
  display: flex;
  flex-direction: column;
  max-width: 400px;
  width: 100%;
  height: 100%;

  /* border: 5px solid rgb(235, 0, 0); */
}

.event__conatinerTwo {
  padding: 20px;
  grid-area: event__containerTwo;
  display: flex;
  flex-direction: column;
  justify-content: center;
  width: 100%;
  height: 100%;

  /* border: 5px solid black; */
}

.event__header {
  /* border: 1px solid black; */
  margin-bottom: 1rem;
  font-size: 2rem;
  font-weight: 700;
}

.event__form {
  display: flex;
  flex-direction: column;
  /* margin: 2rem 14rem; */
}

.event__form input,
textarea {
  width: 100%;
  padding: 0 1.5rem;
  font-size: 2.5rem;
  outline: none;
  border: solid 2px #000;
  margin: 0.5rem 0 2.5rem 0;
}

/* .event__description {
  height: 15rem;
} */

.mobile {
  display: none;
}

.event__label {
  font-size: 1.5rem;
  letter-spacing: 0.1rem;
}

.event__form a {
  align-self: flex-end;
  padding: 0.2rem;
  border-bottom: solid 2px transparent;
  transition: 0.2s linear;
  cursor: pointer;
}

.event__form a:hover {
  border-bottom-color: white;
}

.event__form button {
  align-self: flex-end;
  background-color: #e35353;
  color: white;
  margin-top: 1em;
  padding: 0.5rem 2.5rem;
  font-size: 1.7rem;
  outline: none;
  cursor: pointer;
  font-weight: 700;
  border-radius: 30px;
  text-transform: uppercase;
  border: none;
}

.event__photo {
  min-width: 100%;
  min-height: 200px;
  max-height: 400px;
  margin-bottom: 2.5em;
  object-fit: cover;
}
input[type="file"] {
  color: rgba(0, 0, 0, 0);
}
@media (max-width: 852px) {
  .event__header {
    text-align: center;
  }
  .event__form {
    margin: 1rem 3rem;
  }
}

@media (max-width: 550px) {
  .event__form input {
    width: 5em;
    height: auto;
  }
  .event__header {
    font-size: 2rem;
  }
}

@media screen and (max-width: 800px) {
  .event {
    display: grid;
    grid-template-columns: 1fr;
    grid-template-rows: 1fr 2fr;
    grid-template-areas:
      "event__containerTwo"
      "event__container ";
    height: 2000px;
  }
  .event__container {
    min-width: 100%;
    min-height: 100%;
  }
  .desktop {
    display: none;
  }
  .mobile {
    display: flex;
    flex-direction: column;
  }
}
</style>
