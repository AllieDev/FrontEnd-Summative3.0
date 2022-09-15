<template>
  <div class="view">
    <div class="profile">
      <div class="profile__user-info">
        <div class="profile__username-and-icon-container">
          <div class="profile__user-icon">
            <global-user-icon-vue :uData="uData" />
          </div>
          <div class="profile__username-and-membersince-container">
            <p class="profile__username">
              {{ uData.firstName + " " + uData.lastName }}
            </p>
            <p class="profile__membersince">
              Member Since {{ uData.memberSince }}
            </p>
          </div>
        </div>
        <p class="profile__about">{{ uData.about }}</p>
        <button class="profile_edit-btn">EDIT PROFILE</button>
      </div>
      <div class="profile__user-created-events">
        <div class="profile__subtitle">CREATED EVENTS</div>
        <div class="profile__events-container">
          <global-event-list-vue :eData="eData" />
        </div>
      </div>
      <div class="profile__user-to-attend-events">
        <div class="profile__subtitle">TO ATTEND</div>
        <div class="profile__events-container">
          <global-event-list-vue :eData="eData" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import GlobalUserIconVue from "../components/GlobalUserIcon.vue";
import GlobalEventListVue from "../components/GlobalEventList.vue";
export default {
  components: {
    GlobalUserIconVue,
    GlobalEventListVue,
  },
  data() {
    return {};
  },
  props: ["uData", "eData"],
  methods: {},
  computed: {},
  watch: {},
  created() {
    this.$emit("visibleNav");
    this.$emit("unvisibleSearchInput");
  },
};
</script>

<style scoped>
.view {
  height: calc(100vh - 100px);
  overflow: hidden scroll;
}
@media screen and (max-width: 800px) {
  .view {
    height: calc(100vh - 70px);
  }
}
.profile {
  padding: 20px;
  width: 100%;
  margin: auto;

  overflow: scroll;

  background-color: white;

  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 50px;
}
.profile__subtitle {
  font-family: "Anton", sans-serif;
  font-size: x-large;
  font-weight: 100;
  max-width: 1000px;
  width: 100%;
  margin: auto;
  margin-top: -20px;
}
.profile__events-container {
  min-height: 700px;
  max-width: 1200px;
  margin: auto;
  overflow: scroll hidden;

  display: flex;
  flex-direction: row;
  justify-content: center;
  gap: 20px;
}
.profile__events-container::-webkit-scrollbar {
  display: none;
}
.profile__user-info {
  min-height: 300px;
  width: 100%;
  max-width: 1000px;
  margin: auto;

  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: flex-start;
  gap: 20px;
}
.profile__username-and-icon-container {
  display: flex;
  justify-content: flex-start;
  align-items: center;
  gap: 20px;
}
.profile__user-icon {
  height: 100px;
  width: 100px;
}

.profile__username {
  font-family: "Anton", sans-serif;
  font-size: x-large;
  width: fit-content;
  margin-right: 10px;
}
.profile__membersince {
  font-family: "Abel", sans-serif;
  font-size: medium;
  color: rgb(164, 164, 164);
}
.profile__about {
  font-family: "Abel", sans-serif;
  font-size: medium;
  width: 100%;
  outline: none;
  padding: 0 20px;
}
.profile_edit-btn {
  font-family: "Anton", sans-serif;
  font-weight: 100;
  height: 35px;
  width: 130px;
  background-color: rgb(210, 37, 37);
  color: white;
  border: none;
  border-radius: 20px;
}
.profile__user-created-events {
  width: 100%;
}
.profile__user-to-attend-events {
  width: 100%;
}

@media screen and (max-width: 568px) {
  .profile__user-icon {
    height: 60px;
    width: 60px;
  }
  .profile__username {
    font-size: large;
  }
  .profile__membersince {
    font-size: small;
  }
  .profile__about {
    font-size: small;
  }
}
</style>
