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
};
</script>

<template>
  <div class="header__sidenav">
    <ul class="header__sidenav-list is-mobile">
      <transition-group name="slide-up">
        <li
          v-for="(item, index) in list1"
          :key="index"
          class="header__sidenav-item"
        >
		<a class="header__sidenav-link" href="#">{{ item }}</a>
        </li>
      </transition-group>
    </ul>

    <ul class="header__sidenav-list">
		<transition-group name="slide-up">
        <li
          v-for="(item, index) in list2"
          :key="index"
          class="header__sidenav-item"
        >
		<a class="header__sidenav-link" href="#">{{ item }}</a>
        </li>
      </transition-group>
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
  }

  &-item {
    opacity: 1;
    transform: translateY(-10px);
    transition: opacity 0.5s, transform 0.5s;
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
