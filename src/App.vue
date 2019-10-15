<template>
  <v-app class="App">
    <video class="background-video" ref="backgroundVideo" autoplay loop muted>
      <source src="@/assets/videos/background-video.mp4" />
    </video>

    <nav class="app-nav">
      <ul class="nav-links-list">
        <li>
          <router-link to="/">Home</router-link>
        </li>
        <li>
          <router-link to="/about">About</router-link>
        </li>
        <li>
          <router-link to="/projects">Projects</router-link>
        </li>
        <li>
          <router-link to="/contact">Contact</router-link>
        </li>
      </ul>

      <ul class="nav-icons-list">
        <li>
          <v-btn icon @click="leaveTo('https://www.instagram.com/compass_construction')">
            <v-icon>mdi-instagram</v-icon>
          </v-btn>
        </li>
        <li>
          <v-btn
            icon
            @click="leaveTo('https://www.linkedin.com/company/compass-commercial-construction')"
          >
            <v-icon>mdi-linkedin</v-icon>
          </v-btn>
        </li>
        <li>
          <v-btn icon @click="leaveTo('https://vimeo.com/compassconstruction')">
            <v-icon>mdi-vimeo</v-icon>
          </v-btn>
        </li>
      </ul>
    </nav>

    <img class="logo" ref="logo" src="@/assets/images/logo.jpg" v-if="logoShouldShow"/>
    <v-content v-if="backgroundVideoHasLoaded">
      <router-view />
    </v-content>
  </v-app>
</template>

<style lang="scss">
@import "./main.scss";

.App {
  position: relative;
  font-family: avgardm;
  overflow: hidden;

  .background-video {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translateX(-50%) translateY(-50%) scale(5);
    width: 50vw;
    opacity: 0;
    transition: opacity 2000ms linear;
  }

  .app-nav {
    position: absolute;
    top: 32px;
    left: 0;
    z-index: 1;
    display: flex;
    justify-content: space-between;
    padding: 0 8px 0 16px;
    width: 100%;
    height: 64px;

    background-color: rgba(0, 0, 0, 0.75);

    .nav-links-list {
      display: flex;
      align-items: center;

      li {
        &:not(last-of-type) {
          margin-right: 8px;
        }

        a {
          color: white;
        }
      }
    }

    .nav-icons-list {
      display: flex;
      align-items: center;
    }
  }

  .logo {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translateX(-50%) translateY(-50%);
    width: 50vw;
    transition: opacity 2000ms linear;
  }
}
</style>

<script>
export default {
  name: "App",
  data() {
    return {
      logoShouldShow: true,
      backgroundVideoHasLoaded: false
    };
  },
  mounted() {
    const _this = this;

    _this.$refs.backgroundVideo.oncanplaythrough = () => {
      window.setTimeout(() => {
        _this.$refs.logo.style.opacity = 0;
        _this.$refs.backgroundVideo.style.opacity = 1;

        window.setTimeout(() => {
          _this.backgroundVideoHasLoaded = true;
          _this.logoShouldShow = false;
        }, 2000);
      }, 2000);
    };
  },
  methods: {
    leaveTo(url) {
      window.open(url);
    }
  }
};
</script>
