<template>
  <div v-if="seData !== null" class="view">
    <button class="back__button"></button>

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
              <button class="attend__event" type="button">ATTEND</button>
              <button
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
            <global-user-icon-vue :uData="seData.specificData.hostInfo" />
          </div>
          <div class="write__box">
            <input
              v-model="commentInput"
              class="post__box"
              placeholder="WRITE YOUR COMMENT HERE"
              type="text"
            />
            <button class="post" type="button">POST</button>
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
      commentInput: "",
    };
  },
  props: ["uData", "seData"],
  methods: {
    goBack() {
      router.back();
    },
    created() {
      this.$emit("unvisibleSearchInput");
    },
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
</style>
