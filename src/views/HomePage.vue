<script>
export default {
  data() {
    return {
      isHovered: false,
      sections: {
        1: {
          title: "Starlink Mission",
          text: "Recent Launch",
          buttonText: "Rewatch",
        },
        2: {
          title: "Starlink Mission",
          text: "Upcoming Launch",
          buttonText: "Watch",
        },
        3: {
          title: "Advancing Human Spaceflight",
          text: "",
          buttonText: "Learn More",
        },
        4: {
          title: "to Make Life Multiplanetary",
          text: "",
          buttonText: "Learn More",
        },
      },
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
    const lazyLoadSections = document.querySelectorAll(".section__inner");
    lazyLoadSections.forEach((section) => {
      observer.observe(section);
    });
  },
  methods: {
    animateButton() {
      this.isHovered = true;
    },
    resetButton() {
      this.isHovered = false;
    },
  },
};
</script>

<template>
  <div class="home">
    <div class="home__section">
      <div class="section__video-bg">
        <video autoplay muted loop>
          <source src="@/assets/video.mp4" type="video/mp4" />
        </video>
      </div>

      <div class="section__inner">
        <p class="section__text">UPCOMING LAUNCH</p>
        <h2 class="section__title">POLARIS DAWN</h2>
        <a
          href="#"
          class="section__button"
          @mouseover="animateButton"
          @mouseout="resetButton"
        >
          <div
            class="section__button-bg"
            :class="{ 'section__button-bg--hover': !isHovered }"
          ></div>
          <span>WATCH</span>
        </a>
      </div>

      <div class="scroll-indicator">
        <span></span>
      </div>
    </div>

    <div
      v-for="(section, i) in sections"
      :key="i"
      :class="`home__section home__section-bg--${i}`"
    >
      <div class="section__inner">
        <p class="section__text">{{ section.text }}</p>
        <h2 class="section__title">{{ section.title }}</h2>
        <a
          href="#"
          class="section__button"
          @mouseover="animateButton"
          @mouseout="resetButton"
        >
          <div
            class="section__button-bg"
            :class="{ 'section__button-bg--hover': !isHovered }"
          ></div>
          <span>{{ section.buttonText }}</span>
        </a>
      </div>

      <div class="scroll-indicator">
        <span></span>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.home__section {
  position: relative;
  background-size: cover;
  background-position: center;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh;
  text-transform: uppercase;
}

.section__video-bg {
  padding-top: 56.25%; /* 16:9 aspect ratio */
  width: 100%;

  video {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    object-fit: cover;
  }
}
.home__section-bg--1 {
  background-image: url("/images/img1-mobile.jpg");

  @media (min-width: 768px) {
    background-image: url("/images/img1.jpg");
    background-size: auto 100%;
  }
}
.home__section-bg--2 {
  background-image: url("/images/img2-mobile.jpg");

  @media (min-width: 768px) {
    background-image: url("/images/img2.jpg");
    background-size: auto 100%;
  }
}
.home__section-bg--3 {
  background-image: url("/images/img3-mobile.jpg");

  @media (min-width: 768px) {
    background-image: url("/images/img3.jpg");
    background-size: auto 100%;
  }
}
.home__section-bg--4 {
  background-image: url("/images/img4-mobile.jpg");

  @media (min-width: 768px) {
    background-image: url("/images/img4.jpg");
    background-size: auto 100%;
  }
}

.section__inner {
  display: flex;
  flex-direction: column;
  position: absolute;
  bottom: $padding-lg * 2;
  left: $padding-md;
  right: 0;
  color: $primary-color;
  max-width: 1400px;
  margin: 0 auto;
  opacity: 0;
  transform: translateY(120px);
  transition: opacity 1s ease, transform 1s ease, gap 1s ease;
  gap: 40px;

  &.visible {
    opacity: 1;
    transform: translateY(0);
    gap: 0;
  }

  @media all and (min-width: 600px) {
    padding: $padding-md;
    bottom: $padding-lg * 3;
  }

  @media all and (min-width: 960px) {
    &.visible {
      gap: $padding-xs;
    }
  }
}

.section__title {
  font-size: 2.2rem;
  text-shadow: 0 0 3px rgba($secondary-color, 0.6);
  max-width: 100%;

  @media all and (min-width: 600px) {
    font-size: 3rem;
    max-width: 300px;
  }

  @media all and (min-width: 960px) {
    max-width: 450px;
  }

  @media all and (min-width: 1200px) {
    max-width: 600px;
  }
}

.section__text {
  @media all and (min-width: 960px) {
    font-size: 1.25rem;
  }
}

.section__button {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-top: $padding-sm;
  border: 2px solid $primary-color;
  width: 160px;
  padding: $padding-sm;
  color: $primary-color;
  text-decoration: none;
  font-size: 0.9rem;
  font-weight: 700;
  position: relative;
  overflow: hidden;
  transition: color 0.3s ease;

  &:hover {
    color: $secondary-color;
    transition: color 0.3s ease;
  }

  .section__button-bg {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: $primary-color;
    transform: translateY(100%);
    transition: transform 0.3s ease-out;
  }

  &:hover .section__button-bg {
    transform: translateY(0);
    transition: transform 0.3s ease-out;
  }

  /* Add this */
  @keyframes slideUp {
    0% {
      transform: translateY(0);
    }
    100% {
      transform: translateY(-100%);
    }
  }

  &:not(:hover) .section__button-bg {
    animation: slideUp 0.3s ease-out;
  }

  span {
    position: relative;
  }
}

.scroll-indicator {
  margin-top: auto;
  margin-bottom: $padding-lg * 1.5;
  animation: bounce 3s ease infinite;

  span {
    display: block;
    border-right: 2px solid $primary-color;
    border-bottom: 2px solid $primary-color;
    width: 20px;
    height: 20px;
    transform: rotate(45deg);
  }

  @keyframes bounce {
    0% {
      opacity: 0;
    }
    40% {
      transform: translateY(0);
      opacity: 1;
    }
    80% {
      transform: translateY(8px);
      opacity: 0;
    }
    100% {
      opacity: 0;
    }
  }
}
</style>
