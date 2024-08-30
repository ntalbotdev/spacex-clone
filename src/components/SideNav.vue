<script>
export default {
  data() {
    return {
      list1: [
        "Falcon 9",
        "Falcon Heavy",
        "Dragon",
        "Starship",
        "Human Spaceflight",
        "Rideshare",
        "Starshield",
        "Sharlink",
      ],
      list2: ["Mission", "Launches", "Careers", "Updates", "Shop"],
    };
  },
  mounted() {
    const observer = new IntersectionObserver(
      (entries) => {
        entries.forEach((entry) => {
          if (entry.isIntersecting) {
            const section = entry.target;
            section.classList.add("visible");
            observer.unobserve(section);
          }
        });
      },
      {
        root: null,
        threshold: 0.5,
      }
    );
    const lazyLoadSections = document.querySelectorAll(".header__sidenav-item");
    lazyLoadSections.forEach((section) => {
      observer.observe(section);
    });
  },
};
</script>

<template>
  <div class="header__sidenav">
    <ul class="header__sidenav-list">
      <li
        v-for="(item, index) in list1"
        :key="index"
        class="header__sidenav-item is-mobile"
      >
        <a class="header__sidenav-link" href="#">{{ item }}</a>
      </li>
      <li
        v-for="(item, index) in list2"
        :key="index"
        class="header__sidenav-item"
      >
        <a class="header__sidenav-link" href="#">{{ item }}</a>
      </li>
    </ul>
  </div>
</template>

<style lang="scss" scoped>
.header__sidenav {
  position: fixed;
  top: -30px;
  bottom: 0;
  right: 0;
  z-index: 99;
  padding-top: $header-height + 30px;
  background: $secondary-color;

  &-list {
    width: 350px;
    list-style: none;
    padding: 0 $padding-md;
    padding-left: $padding-lg * 2;

    @media all and (min-width: 600px) {
      padding: 0 $padding-lg;
    }

    @media all and (min-width: 960px) {
      padding: $padding-md $padding-lg;
    }

    @for $i from 1 through 13 {
      & li:nth-of-type(#{$i}) {
        transition-delay: $i * 0.1s;
      }
    }

    @media (min-width: 960px) {
      @for $i from 1 through 7 {
        & li:nth-of-type(#{$i}) {
          transition: none;
          transition-delay: 0s;
        }
      }

      @for $i from 8 through 13 {
        & li:not(.is-mobile):nth-of-type(#{$i}) {
          transition-delay: ($i - 8) * 0.1s;
        }
      }
    }
  }

  &-item {
    transform: translateY(10px);
    opacity: 0;
    transition: opacity 1s ease, transform 1s ease, padding-bottom 1s ease;

    &.visible {
      opacity: 1;
      transform: translateY(0);
    }
  }

  &-link {
    display: block;
    text-transform: uppercase;
    color: $primary-color;
    font-family: $font-normal;
    text-decoration: none;
    padding: $padding-xs 0;
    border-bottom: 1px solid #252525;
    text-align: right;
    transition: color 0.3s ease;

    &:hover {
      color: rgba($primary-color, 0.5);
      transition: color 0.3s ease;
    }
  }
}
</style>
