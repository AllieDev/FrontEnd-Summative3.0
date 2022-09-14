<template>
  <div>
    <nav v-if="isNavVisible" class="nav">
      <div class="nav__container">
        <div class="nav__logo-and-search-input-container">
          <router-link to="/" class="nav__logo">eventFULL</router-link>
          <div
            v-if="isSearchInputAvailable"
            class="nav__search-input-container"
          >
            <input class="nav__search-input" type="text" />
            <button class="nav__search-btn" type="button">
              <global-search-icon-vue />
            </button>
          </div>
        </div>
        <div class="nav__user-icon-create-btn-and-help-btn-container">
          <router-link to="/profile" class="nav__user-icon-container">
            <global-user-icon-vue :uData="userData" />
          </router-link>
          <p @click="toggleDropDownMenue" class="nav__links-dropdown">⌄</p>
          <router-link to="/create-event" class="nav__create-event-btn"
            >CREATE EVENT</router-link
          >
          <global-menu-icon-vue
            @click="toggleDropDownMenue"
            class="nav__mobile-menu-icon"
          />
          <global-help-icon-vue
            @click="toggleHelpCardVisiblity"
            class="nav__help-btn"
          />
          <!-- Help Card Starts -->
          <div v-if="isHelpCardVisible" class="help-card">
            <div class="help-card__pages" id="help-card__page-1">
              <p>
                page-1, dolor sit amet consectetur adipisicing elit. Maiores
                esse neque, veritatis hic aspernatur tempora, minus cum natus
                debitis ab pariatur aut beatae sapiente sunt, cumque eveniet
                iste doloribus voluptates?
              </p>

              <div class="help-card__navigation-btn-container">
                <a class="help-card__navigation-btn" href="#help-card__page-2">
                  <global-arrow-icon-vue class="up-arrow" />
                </a>
              </div>
            </div>
            <div class="help-card__pages" id="help-card__page-2">
              <p>
                page-2. Maiores esse neque, veritatis hic aspernatur tempora,
                minus cum natus debitis ab pariatur aut beatae sapiente sunt,
                cumque eveniet iste doloribus voluptates?
              </p>
              <div class="help-card__navigation-btn-container">
                <a class="help-card__navigation-btn" href="#help-card__page-1">
                  <global-arrow-icon-vue class="down-arrow" />
                </a>
              </div>
            </div>
          </div>
          <!-- Help Card Ends -->
        </div>
        <!-- Dropdown Menu Starts -->
        <div v-if="isDropDownVisible" class="drop-down__container">
          <router-link to="/" class="drop-down__links">Events</router-link>
          <router-link to="/create-event" class="drop-down__links"
            >Create</router-link
          >
          <router-link to="/profile" class="drop-down__links"
            >Profile</router-link
          >
          <div class="drop-down__login-logout-container">
            <router-link
              class="drop-down__login-btn drop-down__log-btns"
              to="/log-in"
            >
              LOG IN
            </router-link>
            <button class="drop-down__logout-btn drop-down__log-btns">
              LOG OUT
            </button>
          </div>
        </div>
        <!-- Dropdown Menu Ends -->
      </div>
      <div v-if="isSearchInputAvailable" class="nav__mobile-search-input">
        <div
          class="nav__search-input-container nav__mobile-search-input-container"
        >
          <input class="nav__search-input" type="text" />
          <button class="nav__search-btn" type="button">
            <global-search-icon-vue />
          </button>
        </div>
      </div>
    </nav>
    <div @click="closeAllDropDowns" class="router-view-container">
      <router-view
        :seData="specificEventDetail"
        :uData="userData"
        :eData="eventData"
        @unvisibleSearchInput="hideSearchInput"
        @visibleSearchInput="showSearchInput"
        @unvisibleNav="makeNavUnvisible"
        @visibleNav="makeNavVisible"
        @specificEventDetail="getSpecificEventDetail"
      />
    </div>
    <!-- For Development Only -->
    <div class="dev__quick-page-access">
      <router-link class="router-link" to="/log-in">Sign-Up Login</router-link>
      <router-link class="router-link" to="/">Event List</router-link>
      <router-link class="router-link" to="/event-detail"
        >Event Detail</router-link
      >
      <router-link class="router-link" to="/create-event"
        >Create Event</router-link
      >
      <router-link class="router-link" to="/profile">User Profile</router-link>
    </div>
    <!-- For Development Only -->
  </div>
</template>

<script>
import GlobalUserIconVue from "./components/GlobalUserIcon.vue";
import GlobalSearchIconVue from "./components/icons/GlobalSearchIcon.vue";
import GlobalHelpIconVue from "./components/icons/GlobalHelpIcon.vue";
import GlobalArrowIconVue from "./components/icons/GlobalArrowIcon.vue";
import GlobalMenuIconVue from "./components/icons/GlobalMenuIcon.vue";

export default {
  components: {
    GlobalUserIconVue,
    GlobalSearchIconVue,
    GlobalHelpIconVue,
    GlobalArrowIconVue,
    GlobalMenuIconVue,
  },
  data() {
    return {
      isDropDownVisible: false,
      isSearchInputAvailable: true,
      isHelpCardVisible: false,
      isNavVisible: true,
      userData: {
        _id: "63197b52f62ff345ce130c62",
        iconColor: "lightgray",
        firstName: "Guest",
        lastName: "",
        email: "no-gmail@gmail.com",
        memberSince: "Now",
        about: "This is a little about me...",
      },
      eventData: [{}, {}],
      specificEventDetail: {},
    };
  },
  methods: {
    makeNavVisible() {
      this.isNavVisible = true;
    },
    makeNavUnvisible() {
      this.isNavVisible = false;
    },
    toggleHelpCardVisiblity() {
      this.isHelpCardVisible = !this.isHelpCardVisible;
      this.isDropDownVisible = false;
    },
    toggleDropDownMenue() {
      this.isDropDownVisible = !this.isDropDownVisible;
      this.isHelpCardVisible = false;
    },
    closeAllDropDowns() {
      this.isHelpCardVisible = false;
      this.isDropDownVisible = false;
    },
    hideSearchInput() {
      this.isSearchInputAvailable = false;
    },
    showSearchInput() {
      this.isSearchInputAvailable = true;
    },
    async getListOfAllEventsRequest() {
      const response = await fetch("http://localhost:3000/events");
      const data = await response.json();
      this.eventData = data;
    },
    async getSpecificEventDetail(data) {
      const response = await fetch(`http://localhost:3000/events/${data._id}`);

      const specificData = await response.json();
      const evenData = data;

      this.specificEventDetail = {
        eventData: evenData,
        specificData: specificData,
      };

      console.log(this.specificEventDetail);
      router.push("/event-detail");
    },
    // ----------------------------------------------------------------
  },
  created() {
    this.getListOfAllEventsRequest();
  },
};
</script>

<style scoped>
.router-view-container {
  height: calc(100vh - 100px);
  /* border: 3px solid rgb(255, 0, 0); */
}
.nav {
  height: 100px;
  box-shadow: 0px 5px 15px 5px rgba(0, 0, 0, 0.156);

  display: flex;
  justify-content: center;
  align-items: center;
}
.nav__container {
  position: relative;

  padding: 0 20px;
  height: 100%;
  max-width: 1200px;
  width: 100%;

  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 30px;

  /* border: 1px solid black; */
}
.nav__logo-and-search-input-container {
  max-width: 500px;
  width: 100%;

  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 20px;
}
.nav__logo {
  text-decoration: none;
  font-weight: 600;
  font-size: xx-large;

  color: rgb(244, 60, 60);
}
.nav__search-input-container {
  height: 30px;
  max-width: 300px;
  width: 100%;

  display: flex;
  border: 1px solid black;
  border-radius: 5px;
}

.nav__search-input {
  font-size: medium;
  padding-left: 10px;
  height: 100%;
  width: calc(100% - 20px);

  border: none;
  border-radius: 5px 0 0 5px;
  outline: none;
}

.nav__search-btn {
  height: 100%;
  width: 50px;

  display: flex;
  justify-content: center;
  align-items: center;

  border: none;
  background-color: white;
  border-left: 1px solid black;
  border-radius: 0 5px 5px 0;
}
.nav__user-icon-create-btn-and-help-btn-container {
  max-width: 300px;
  width: 100%;

  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 10px;
}

.nav__user-icon-container {
  text-decoration: none;
  height: 50px;
  width: 50px;
}
.nav__create-event-btn {
  text-decoration: none;
  font-size: medium;
  padding: 8px 20px;

  background-color: rgb(244, 60, 60);
  color: white;

  border: none;
  border-radius: 20px;
}
.nav__mobile-menu-icon {
  display: none;
}
.nav__links-dropdown {
  font-size: x-large;
}
.nav__mobile-search-input {
  display: none;
}

.help-card::-webkit-scrollbar {
  display: none;
}

.help-card {
  z-index: 2;
  position: absolute;
  top: 101px;
  right: 2px;
  max-width: 300px;
  height: 400px;

  background-color: white;
  box-shadow: 5px 10px 10px 0 rgba(23, 23, 23, 0.25);

  overflow: hidden scroll;
  scroll-snap-type: y mandatory;
}
.help-card__pages {
  box-sizing: border-box;
  padding: 30px;
  width: 100%;
  height: 100%;

  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;

  scroll-snap-align: center;
}
.help-card__navigation-btn-container {
  display: flex;
  justify-content: center;
  align-items: center;
}
.help-card__navigation-btn {
  font-size: 15px;
  text-decoration: none;
  width: 3.5rem;
  height: 3.5rem;

  display: flex;
  align-items: center;
  justify-content: center;
}
.down-arrow {
  rotate: 90deg;
}
.up-arrow {
  rotate: 270deg;
}
.dev__quick-page-access {
  padding-bottom: 20px;
  z-index: 1;
  position: fixed;
  bottom: 0;
  left: 0;

  display: flex;
  gap: 20px;
  background-color: rgb(0, 136, 255);
}
.drop-down__container {
  z-index: 1;
  position: absolute;
  top: 101px;
  right: 150px;

  padding: 10px;
  height: 200px;
  width: 200px;

  background-color: rgb(255, 255, 255);
  box-shadow: 5px 10px 10px 0 rgba(23, 23, 23, 0.25);

  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  align-items: center;
}
.drop-down__links {
  text-decoration: none;
  font-family: "Abel", sans-serif;
  color: black;
}
.drop-down__login-logout-container {
  width: 100%;
}
.drop-down__log-btns {
  text-decoration: none;
  font-size: small;
  padding: 10px 0;
  width: 100%;

  color: white;
  background-color: red;
  border: none;

  display: flex;
  justify-content: center;
  align-items: center;
}
.router-link {
  font-size: medium;
  text-decoration: none;
  background-color: rgb(0, 136, 255);
  color: white;
}
.router-link:hover {
  margin-top: -20px;
}

@media screen and (max-width: 800px) {
  .nav {
    height: 70px;
  }
  .nav__search-input-container {
    display: none;
  }
  .nav__user-icon-create-btn-and-help-btn-container {
    max-width: 100px;
  }
  .nav__links-dropdown {
    display: none;
  }
  .nav__create-event-btn {
    display: none;
  }
  .nav__help-btn {
    display: none;
  }
  .nav__mobile-search-input {
    z-index: 1;
    position: fixed;
    top: 70px;
    left: 0;

    padding-bottom: 10px;
    width: 100vw;
    height: 40px;
    background-color: white;

    display: flex;
    justify-content: center;
    align-items: center;
    box-shadow: 0px 5px 15px 0px rgba(149, 149, 149, 0.156);
  }
  .nav__mobile-search-input-container {
    max-width: 97vw;

    display: flex;
  }
  .nav__mobile-menu-icon {
    display: flex;
  }
  .drop-down__container {
    z-index: 2;
    position: fixed;
    top: 70px;
    right: 0;
    height: 100vh;
    width: 100vw;
    /* border: 10px solid black; */
  }
}
</style>
