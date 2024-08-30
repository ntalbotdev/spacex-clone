<script setup>
import LogoImage from "./LogoImage.vue";
import SideNav from "./SideNav.vue";
</script>

<script>
export default {
  data() {
    return {
      isSidebarOpen: false,
      headerHasBg: false,
      isHeaderSlidingUp: false,
      isHeaderHidden: false,
      prevScrollY: 0,
    };
  },
  mounted() {
    window.addEventListener("scroll", this.handleScroll);
  },
  beforeUnmount() {
    window.removeEventListener("scroll", this.handleScroll);
  },
  methods: {
    handleScroll() {
      const scrollY = window.scrollY;
      const viewportHeight = window.innerHeight;

      if (scrollY >= viewportHeight && scrollY < this.prevScrollY) {
        this.headerHasBg = true;
      } else {
        this.isHeaderSlidingUp = true;
        this.headerHasBg = false;
      }

      if (scrollY > 0 && scrollY > this.prevScrollY) {
        this.isHeaderHidden = true;
      } else if (scrollY < this.prevScrollY) {
        this.isHeaderHidden = false;
      }

      if (this.isSidebarOpen == true) {
        this.isSidebarOpen = false;
      }

      this.prevScrollY = scrollY;
    },
    toggleSidebar() {
      this.isSidebarOpen = !this.isSidebarOpen;
    },
  },
};
</script>

<template>
  <header class="header">
    <transition name="slide" appear>
      <div class="header__background" v-show="headerHasBg"></div>
    </transition>
    <div class="header__inner" :class="{ 'is-hidden': isHeaderHidden }">
      <a class="header__logo" href="https://www.spacex.com">
        <LogoImage class="header__logo-img" />
      </a>

      <nav class="header__nav is-desktop">
        <ul class="header__nav-list">
          <li class="header__nav-item">
            <a class="header__nav-link" href="#">Falcon 9</a>
          </li>
          <li class="header__nav-item">
            <a class="header__nav-link" href="#">Falcon Heavy</a>
          </li>
          <li class="header__nav-item">
            <a class="header__nav-link" href="#">Dragon</a>
          </li>
          <li class="header__nav-item">
            <a class="header__nav-link" href="#">Starship</a>
          </li>
          <li class="header__nav-item">
            <a class="header__nav-link" href="#">Human Spaceflight</a>
          </li>
          <li class="header__nav-item">
            <a class="header__nav-link" href="#">Rideshare</a>
          </li>
          <li class="header__nav-item">
            <a class="header__nav-link" href="#">Starlink</a>
          </li>
        </ul>
      </nav>

      <nav class="header__nav--right is-desktop">
        <ul class="header__nav-list">
          <li class="header__nav-item">
            <a class="header__nav-link" href="#">Shop</a>
          </li>
        </ul>
      </nav>

      <transition name="slideLeft">
        <SideNav
          :class="{ 'header__sidenav--open': isSidebarOpen }"
          v-show="isSidebarOpen"
        />
      </transition>
    </div>

    <div
      class="header__hamburger-icon"
      :class="{ 'is-hidden': isHeaderHidden }"
      @click="toggleSidebar"
    >
      <span :class="{ active: isSidebarOpen }"></span>
      <span :class="{ active: isSidebarOpen }"></span>
      <span :class="{ active: isSidebarOpen }"></span>
    </div>

    <div
      class="overlay"
      :class="{ 'overlay--show': isSidebarOpen }"
      v-show="isSidebarOpen"
      @click="toggleSidebar"
    ></div>
  </header>
</template>

<style lang="scss" scoped>
.slide-enter-active,
.slide-leave-active {
  transition: transform 1s cubic-bezier(0.08, 1, 0.44, 0.99);
}

.slide-enter-from,
.slide-leave-to {
  transform: translateY(-100%);
  transition-delay: 0.2s;
}

.slide-enter-to,
.slide-leave-from {
  transform: translateY(0);
}

.slideLeft-enter-active,
.slideLeft-leave-active {
  transition: transform 0.8s cubic-bezier(0.19, 0.51, 0.07, 0.97);
}

.slideLeft-enter-from {
  transform: translateX(100%) rotate(-5deg);
}

.slideLeft-leave-to {
  transform: translateX(100%);
}

.header {
  position: fixed;
  top: 0;
  left: 0;
  z-index: 1;
  display: flex;
  align-items: center;
  width: 100%;
  transition: all 0.3s ease;

  &__background {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: $secondary-color;
  }

  &__inner {
    display: flex;
    align-items: center;
    width: 100%;
    max-width: 1400px;
    margin: 0 auto;
    z-index: 99;
    padding: $padding-md;
    transition: all 0.3s cubic-bezier(0.19, 0.51, 0.07, 0.97);

    @media (min-width: 600px) {
      padding: $padding-md $padding-lg;
    }

    @media (min-width: 960px) {
      padding: $padding-lg;
    }
  }

  .is-hidden {
    opacity: 0;
    transition: all 0.3s cubic-bezier(0.19, 0.51, 0.07, 0.97);
  }

  &__logo {
    margin: 0 auto;
    z-index: 10000;

    &-img {
      width: 150px;
      margin-left: 30px;
    }

    @media (min-width: 960px) {
      &-img {
        width: 200px;
        margin-left: 0;
        margin-right: $padding-md;
      }
    }
  }
}

.header__hamburger-icon {
  display: flex;
  flex-direction: column;
  position: absolute;
  z-index: 101;
  right: $padding-md;
  transition: opacity 0.3s ease;

  @media all and (min-width: 600px) {
    right: $padding-lg;
  }

  &:hover {
    cursor: pointer;
  }

  span {
    width: 16px;
    height: 2px;
    background-color: $primary-color;
    margin: 1px 0;
    transition: all 0.2s ease-out;

    &.active {
      transition: all 0.2s ease-out;
    }

    &.active:nth-child(1) {
      transform: translateY(4px) rotate(45deg);
    }

    &.active:nth-child(2) {
      opacity: 0;
      transform: translateX(8px);
      width: 0;
    }

    &.active:nth-child(3) {
      transform: translateY(-4px) rotate(-45deg);
    }
  }
}

.header__nav {
  display: none;
  width: 100%;
  margin-right: 100px;

  @media (min-width: 960px) {
    display: block;
  }

  &-list {
    list-style: none;
    display: flex;
    flex-wrap: wrap;
    gap: $padding-md;
  }

  &-item {
    position: relative;

    &:after {
      content: "";
      display: none;
      display: block;
      width: 100%;
      height: 1px;
      position: absolute;
      bottom: -4px;
      left: 0;
      background-color: $primary-color;
      transform: scaleX(0);
      transform-origin: right;
      transition: transform 0.3s ease;
    }

    &:hover:after {
      transform: scaleX(1);
      transform-origin: left;
      transition: transform 0.3s ease;
    }
  }

  &-link {
    color: $primary-color;
    text-decoration: none;
    text-transform: uppercase;
    font-weight: 700;
    font-size: 0.9rem;
    white-space: nowrap;

    &:hover {
      // border-bottom anim left right like btn
    }
  }
}

.header__nav--right {
  margin-left: auto;
  margin-right: $padding-md;
  position: absolute;
  right: $padding-lg + $padding-md;
}

.overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba($secondary-color, 0.5);
  z-index: 1;
  opacity: 0;
  transition: all 0.3s ease;

  &--show {
    opacity: 1;
    transition: all 0.3s;
  }
}
</style>
