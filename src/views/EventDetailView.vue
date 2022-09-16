<template>
  <div v-if="seData !== null" class="view">
    <!--MODEL STARTS ---------------------------------------------------------------- -->
    <div
      @click.self="toggleModal"
      v-if="isEditMode"
      class="edit-model-background"
    >
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
            <button @click="emitCreateEventData" href="#">PUBLISH</button>
          </form>
        </div>
        <div class="event__conatinerTwo">
          <img :src="editModelImageDynamicSrc" class="event__photo" alt="" />
          <label for="myfile">Select a Photo</label>
          <input
            @input="(event) => (imageFile = event.target.files[0])"
            type="file"
            @change="displayImage"
            id="myfile"
            name="myfile"
          />
          <!-- ---------------------------------------------------------------- -->
          <div class="desktop">
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
        </div>
      </div>
    </div>
    <!--MODEL ENDS ---------------------------------------------------------------- -->
    <div class="detail__heading">
      <div @click="goBack()" class="router-link">
        <global-arrow-icon-vue class="back__button" />
      </div>

      <div class="detail__boxx">
        <h3 class="time__date">
          {{ seData.eventData.date + " -- " + seData.eventData.time }}
        </h3>
        <h1 class="event__title">{{ seData.eventData.title }}</h1>
        <h4 class="event__location">{{ seData.eventData.location }}</h4>
      </div>
    </div>

    <!-- AVATAR AND BUTTONS -->

    <!-- MAIN CONTAINER -->

    <main class="main__eventDetails">
      <div class="main__detail">
        <div class="user__avatar">
          <div class="avatar__container">
            <div class="avatar__cricle-heading-container">
              <div class="avatar__circle">
                <global-user-icon-vue :uData="seData.specificData.hostInfo" />
              </div>
              <div class="avatar__headings">
                <h5 class="hosted__by">HOSTED BY</h5>
                <h3 class="host__name">
                  {{
                    seData.specificData.hostInfo.firstName +
                    " " +
                    seData.specificData.hostInfo.lastName
                  }}
                </h3>
              </div>
            </div>
            <div class="attend--edit__container">
              <button
                class="attend__event"
                type="button"
                @click="sendAttendEventRequest"
              >
                ATTEND
              </button>
              <button
                @click="toggleModal"
                v-if="seData.eventData.hostId == uData._id"
                class="edit__event"
                type="button"
              >
                EDIT
              </button>
            </div>
          </div>
        </div>

        <div class="detail__image">
          <img
            v-if="seData.eventData.imageFile"
            class="details__image"
            :src="`data:image/jpeg;base64,${seData.eventData.imageFile.data}`"
            alt=""
          />
          <img
            v-else
            src="https://images.unsplash.com/photo-1540575467063-178a50c2df87?crop=entropy&cs=tinysrgb&fm=jpg&ixid=Mnw3MjAxN3wwfDF8c2VhcmNofDN8fGV2ZW50fGVufDB8MHx8fDE2NjI0Mjg0MTA&ixlib=rb-1.2.1&q=80&q=85&fmt=jpg&crop=entropy&cs=tinysrgb&w=450"
            class="details__image"
          />
          <div class="event__detail">
            <h3 class="box__heading">DETAILS</h3>
            <p class="detail__text">
              {{ seData.eventData.detail }}
            </p>
            <button class="map__marker" type="button">
              <i class="fa fa-map-marker" aria-hidden="true"></i>
            </button>
          </div>
        </div>

        <!-- COMMENT SECTION -->

        <div class="write__comment">
          <div class="avatar__circle">
            <global-user-icon-vue :uData="uData" />
          </div>
          <div class="write__box">
            <input
              v-model="commentInput"
              class="post__box"
              placeholder="WRITE YOUR COMMENT HERE"
              type="text"
            />
            <button @click="sendCommentPostRequest" class="post" type="button">
              POST
            </button>
          </div>
        </div>

        <div
          v-for="comment in seData.specificData.commentsInfo"
          class="view__comment"
        >
          <div class="avatar__circle">
            <global-user-icon-vue :uData="comment.commentator" />
          </div>
          <p class="posted__comment">
            {{ comment.comment }}
          </p>
        </div>
      </div>

      <!-- ATTENDING -->

      <div class="event__attendees">
        <div class="attendees__count">
          <h3 class="attendees__heading">ATTENDING</h3>
          <h3 class="attendees__number">
            ({{ seData.specificData.attendeesInfo.length }})
          </h3>
        </div>

        <div class="test__media">
          <div
            v-for="attendee in seData.specificData.attendeesInfo"
            class="attendees__avatar"
          >
            <div class="avatar__circle">
              <global-user-icon-vue :uData="attendee" />
            </div>
            <div class="attendees--name__status">
              <h4 class="attendee__name">
                {{ attendee.firstName + " " + attendee.lastName }}
              </h4>
              <h5 class="attendees__status">Member</h5>
            </div>
          </div>
        </div>
      </div>
    </main>
    <div class="logo__bottom">
      <h1>eventFULL</h1>
    </div>
  </div>
  <div v-else><h1>Please Login First</h1></div>
</template>

<script>
import GlobalArrowIconVue from "../components/icons/GlobalArrowIcon.vue";
import GlobalUserIconVue from "../components/GlobalUserIcon.vue";
import router from "../router";
export default {
  components: {
    GlobalUserIconVue,
    GlobalArrowIconVue,
  },
  data() {
    return {
      isDisplayImage: true,
      eventTitle: null,
      eventLocation: null,
      eventDate: null,
      eventTime: null,
      eventDescription: null,
      imageFile: "",
      imageFileUrl: "",
      isEditMode: true,
      commentInput: "",
    };
  },
  props: ["uData", "seData"],
  methods: {
    displayImage() {
      this.isDisplayImage = false;
      const reader = new FileReader();
      reader.readAsDataURL(this.imageFile);
      reader.addEventListener("load", () => {
        this.imageFileUrl = reader.result.toString();
      });
    },
    toggleModal() {
      this.isEditMode = !this.isEditMode;

      this.eventTitle = this.$props.seData.eventData.title;
      this.eventLocation = this.$props.seData.eventData.location;
      this.eventDate = this.$props.seData.eventData.date;
      this.eventTime = this.$props.seData.eventData.time;
      this.eventDescription = this.$props.seData.eventData.detail;
      console.log();
    },
    goBack() {
      router.back();
    },
    async sendAttendEventRequest() {
      // console.log(this.seData.eventData._id);
      const response = await fetch(
        `http://localhost:3000/events/attend/${this.$props.seData.eventData._id}`,
        {
          method: "PATCH",
          headers: {
            "Content-Type": "application/json",
            Authorization: "Bearer " + localStorage.getItem("token"),
          },
        }
      );
      const data = await response.json();
      alert(data.message);
    },
    async sendCommentPostRequest() {
      console.log("sending comment post request");
      console.log(this.commentInput);
      const response = await fetch(
        `http://localhost:3000/events/${this.$props.seData.eventData._id}`,
        {
          method: "PATCH",
          headers: {
            "Content-Type": "application/json",
            Authorization: "Bearer " + localStorage.getItem("token"),
          },
          body: JSON.stringify({
            comment: this.commentInput,
          }),
        }
      );
      const data = await response.json();
      alert(data.message);
    },
  },
  computed: {
    editModelImageDynamicSrc() {
      if (this.isDisplayImage) {
        return `data:image/jpeg;base64,${this.$props.seData.eventData.imageFile.data}`;
      } else {
        return this.imageFileUrl;
      }
    },
  },
  created() {
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

.back__button {
  cursor: pointer;
  margin-bottom: 50px;
}
.router-link {
  width: fit-content;
}
.detail__heading {
  padding: 0 20px;
  max-width: 1200px;
  margin: auto;
}
@media screen and (max-width: 768px) {
  .detail__heading {
    padding: 0 10px;
  }
}

.time__date {
  font-family: abel, sans-serif;
}

@media screen and (max-width: 768px) {
  .time__date {
    font-size: 16px;
  }
}
.event__title {
  font-family: anton, sans-serif;
  letter-spacing: 2px;
}

@media screen and (max-width: 768px) {
  .event__title {
    font-size: 25px;
  }
}

.event__location {
  margin-top: 1%;
  font-family: anton, sans-serif;
  font-size: 14px;
  letter-spacing: 1.5px;
  color: #5c5c5c;
}

@media screen and (max-width: 768px) {
  .event__location {
    font-size: 13px;
  }
}
.user__avatar {
  margin-top: 4%;
  margin-bottom: 4%;
}

.avatar__circle {
  border-radius: 100%;
  width: 4rem;
  height: 4rem;
}

@media screen and (max-width: 768px) {
  .avatar__circle {
    width: 3rem;
    height: 3rem;
  }
}

.avatar__container {
  width: 100%;

  display: flex;
  align-items: center;
  justify-content: space-between;
}

@media screen and (max-width: 768px) {
  .avatar__container {
    flex-wrap: wrap;
    gap: 10px;
  }
}

.avatar__cricle-heading-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 180px;
}
@media screen and (max-width: 768px) {
  .avatar__cricle-heading-container {
    width: 150px;
  }
}

.hosted__by {
  font-family: abel, sans-serif;
}

.host__name {
  font-family: anton, sans-serif;
  letter-spacing: 2px;
}

@media screen and (max-width: 768px) {
  .host__name {
    font-size: 15px;
  }
}

.attend--edit__container {
  max-width: 270px;
  width: 100%;
  display: flex;
  justify-content: space-between;
}
@media screen and (max-width: 800px) {
  .attend--edit__container {
    max-width: 100px;
    flex-direction: column;
    gap: 5px;
    align-items: flex-end;
  }
}

.attend__event,
.edit__event {
  cursor: pointer;
  border: 0px solid #e35353;
  border-radius: 20px;
  background-color: #e35353;
  color: #f1f1f1;
  width: 8rem;
  height: 2.5rem;
  font-family: anton, sans-serif;
  font-size: 12px;
  letter-spacing: 2px;
}

@media screen and (max-width: 800px) {
  .attend__event,
  .edit__event {
    cursor: pointer;
    border: 0px solid #e35353;
    border-radius: 20px;
    background-color: #e35353;
    color: #f1f1f1;
    width: 5rem;
    height: 2rem;
    font-family: anton, sans-serif;
    font-size: x-small;
    letter-spacing: 2px;
  }
}

/* /////////////////////////////////////////////// */

.main__eventDetails {
  display: flex;
  justify-content: space-between;
  margin-top: 2%;
  padding: 0 20px;
  width: 100%;
  max-width: 1200px;
  margin: auto;
}

@media screen and (max-width: 768px) {
  .main__eventDetails {
    display: block;
    padding: 0 10px;
  }
}

.main__detail {
  max-width: 700px;
}

@media screen and (max-width: 768px) {
  .main__detail {
    margin-left: 0rem;
    width: 100%;
  }
}

.detail__image {
  margin-bottom: 50px;
  min-width: 100%;
  height: 550px;

  display: flex;
  flex-direction: column;
  align-items: center;
}

.details__image {
  width: 100%;
  height: 250px;
  object-fit: cover;
}

.event__detail {
  height: 400px;
  margin-top: -30px;
  width: 90%;
  padding: 30px;
  background-color: white;
  box-shadow: 6px 10px 18px #00000028;
}

.box__heading {
  font-family: anton, sans-serif;
  letter-spacing: 2px;
}

.detail__text {
  margin-top: 2%;
  font-family: abel, sans-serif;
}

.map__marker {
  cursor: pointer;
  background-color: white;
  border: 0px;
  margin-top: 5%;
  margin-left: 90%;
  font-size: 20px;
  color: rgb(58, 152, 215);
}

/* //////////////////////////////////////////////////////////// */

/* //////////////////////////////////////////////////////////// */

.write__comment {
  margin-top: 4%;
  display: flex;
  align-items: center;
  gap: 2rem;
}

@media screen and (max-width: 768px) {
  .write__comment {
    gap: 1rem;
  }
}

.write__box {
  width: 80%;
  border: 1.5px solid black;
  display: flex;
  justify-content: space-between;
}

@media screen and (max-width: 768px) {
  .write__box {
    width: 80%;
  }
}

.post__box {
  outline: none;
  margin-left: 1rem;
  width: 90%;
  height: 2.5rem;
  border: 0px;
  font-family: abel, sans-serif;
}

.post {
  cursor: pointer;
  margin-right: 1rem;
  border: 0px;
  background-color: white;
  font-family: anton, sans-serif;
  letter-spacing: 1px;
  color: black;
}

.view__comment {
  margin-top: 3%;
  margin-left: 0rem;
  display: flex;
  align-items: center;
  gap: 2rem;
}

@media screen and (max-width: 768px) {
  .view__comment {
    gap: 1rem;
  }
}

.posted__comment {
  width: 80%;
}

@media screen and (max-width: 768px) {
  .posted__comment {
    font-size: small;
  }
}

/* /////////////////////////////////////////////////// */

@media screen and (max-width: 768px) {
  .event__attendees {
    margin-top: 7rem;
  }
}

.attendees__count {
  display: flex;
  gap: 10px;
  margin-bottom: 3rem;
  font-family: anton, sans-serif;
  font-size: 14px;
  letter-spacing: 2px;
}

@media screen and (max-width: 768px) {
  .attendees__count {
    font-size: 12px;
  }
}

.attendees__avatar {
  font-family: anton, sans-serif;
  font-size: 14px;
  letter-spacing: 1.5px;
  margin: 0 20px;

  display: flex;
  align-items: center;
  justify-content: center;
  gap: 2rem;

  color: #333333;
}
.attendees__status {
  font-family: abel, sans-serif;
}

@media screen and (max-width: 768px) {
  .attendees__avatar {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 1rem;

    font-size: 12px;

    /* flex-direction: row; */
    /* margin-left: -83%; */
  }
}
.test__media {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

@media screen and (max-width: 768px) {
  .test__media {
    padding: 10px;
    width: 100%;
    display: flex;
    overflow: scroll hidden;
    flex-direction: row;
    gap: 0.5rem;
  }
}
/* /////////////////////////////////////////////////// */

.logo__bottom {
  margin-top: 10rem;

  font-family: anton, sans-serif;
  letter-spacing: 2px;
  font-size: 12px;
  /* background-color: aquamarine; */
  display: flex;
  justify-content: center;
  padding: 50px;
}

@media screen and (max-width: 768px) {
  .logo__bottom {
    font-size: 8px;
    margin-top: 8rem;
  }
}
/* -------------------------------------------------------------------------- */
/* -------------------------------------------------------------------------- */
.edit-model-background {
  overflow: hidden scroll;
  position: fixed;
  top: 0;
  right: 0;

  height: 100vh;
  width: 100vw;
  background-color: rgba(0, 0, 0, 0.713);

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
}

.event__container {
  grid-area: event__container;
  padding: 20px;
  display: flex;
  flex-direction: column;
  max-width: 400px;
  width: 100%;
  height: 100%;
}

.event__conatinerTwo {
  padding: 20px;
  grid-area: event__containerTwo;
  display: flex;
  flex-direction: column;
  justify-content: center;
  width: 100%;
  height: 100%;
}

.event__header {
  margin-bottom: 1rem;
  font-size: 2rem;
  font-weight: 700;
}

.event__form {
  display: flex;
  flex-direction: column;
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
