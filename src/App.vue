<script setup>
import TheHeader from './components/TheHeader.vue'
import TheFooter from './components/TheFooter.vue'
import HomePage from './views/HomePage.vue'
</script>

<template>
  <TheHeader />

  <main>
    <HomePage />
  </main>
  <TheFooter />
</template>

<!--
TO DO
 
logo z-index above side-nav
slideIn offset transition sidenav__link, lazyload?
better cubic-bezier on section__button (home)
vue smoothscroll
lazyload

home section__inner slide into view as lazyload
loading page black screen opacity transition
-->