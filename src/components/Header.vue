<template>
  <header>
    <Logo />
    <div class="nav nav-pills">
      <div
        v-for="nav in navigations"
        :key="nav.name"
        class="nav-item">
        <Router-link
          :to="nav.href"
          active-class="active"
          :class="{ active: isMatch(nav.path) }"
          class="nav-link">
          {{ nav.name }}
        </Router-link>
      </div>
    </div>
    <div
      class="user"
      @click="toAbout">
      <img
        :src="image"
        :alt="name" />
    </div>
  </header>
</template>

<script>
import {mapState} from "vuex";
import Logo from "~/components/Logo";

export default {
  data() {
    return {
      navigations: [
        {
          name: "Search",
          href: "/",
        },
        {
          name: "Movie",
          href: "/movie",
          path: /^\/movie/,
        },
        {
          name: "About",
          href: "/about",
        },
      ],
    };
  },
  computed: {
    ...mapState( 'about', [
      'image',
      'name'
    ])
  },
  components: {
    Logo,
  },
  methods: {
    isMatch(path) {
      if (!path) return false;
      return path.test(this.$route.fullPath);
    },
    toAbout(){
      this.$router.push('/about')
    },
  },
};
</script>

<style lang="scss" scoped>
@import "~/scss/main";
header {
  position: relative;
  height: 70px;
  padding: 0 40px;
  display: flex;
  align-items: center;
  .logo {
    margin-right: 40px;
  }
  .user {
    width: 40px;
    height: 40px;
    padding: 6px;
    border-radius: 50%;
    box-sizing: border-box;
    background: white;
    cursor: pointer;
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    right: 40px;
    margin: 0;
    transition: 0.4s;
    &:hover {
      background: darken($gray-200, 10%);
      transition: 0.4s;
    }
    img {
      width: 100%;
    }
  }
  @include media-breakpoint-down(sm){
    .nav{
      display: none;
    }
  }
}
</style>