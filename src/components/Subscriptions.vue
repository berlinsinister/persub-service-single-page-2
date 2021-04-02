<template>
  <div
    class="subscription-container"
    :class="
      id === 'first-child'
        ? 'rounded-top-borders'
        : id === 'last-child'
        ? 'rounded-bottom-borders'
        : ''
    "
    :style="
      windowWidth <= 850 ? { borderBottom: `4px solid ${background}` } : ''
    "
  >
    <div class="background">
      <div class="bg-circle" :style="{ background: background }"></div>
    </div>
    <div class="name" @click="popupHandler">{{ name }}</div>
    <div class="category">{{ category }}</div>
    <div class="date">{{ calcDate }}</div>
    <div class="frequency">{{ frequency }}</div>
    <div class="amount">{{ amount }}$</div>
  </div>
</template>

<script>
export default {
  name: "Subscriptions",
  props: {
    background: String,
    name: {
      type: String,
      default: "Terminal Co-Working",
    },
    category: {
      type: String,
      default: "Lifestyle",
    },
    frequency: {
      type: String,
      default: "Yearly",
    },
    amount: {
      type: Number,
      default: 14.45,
    },
    id: String,
  },
  data() {
    return {
      day: new Date().getDate(),
      month: new Date().getMonth(),
      hours: new Date().getHours(),
      minutes: new Date().getMinutes(),
      months: [
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December",
      ],
      windowWidth: window.innerWidth,
    };
  },
  mounted() {
    this.$nextTick(() => {
      window.addEventListener("resize", this.onResize);
    });
  },
  beforeUnmount() {
    window.removeEventListener("resize", this.onResize);
  },
  methods: {
    onResize() {
      this.windowWidth = window.innerWidth;
    },
    popupHandler() {
      let details = {
        background: this.background,
        name: this.name,
        frequency: this.frequency,
        amount: this.amount,
      };
      this.$emit("popup", details);
    },
  },
  computed: {
    calcDate() {
      let ampm = this.hours > 12 ? "pm" : "am";
      let minutes = this.minutes <= 9 ? "0" + this.minutes : this.minutes;
      return `${this.months[this.month]} ${this.day}, ${
        this.hours
      }:${minutes} ${ampm}`;
    },
  },
};
</script>

<style lang="scss" scoped>
@import "../assets/sass/vars";
@import "../assets/sass/mixins";

$width: 155rem;

.subscription-container {
  display: grid;
  grid-template-columns: repeat(6, auto);
  grid-auto-rows: auto;
  width: $width;
  height: 10rem;
  background: white;
  // border: 1px solid blueviolet;
  & > div {
    display: grid;
    align-content: center;
    width: floor(($width - 10rem) / 5);
    color: gray;
    font-size: 1.5rem;
    font-weight: 500;
  }
  & .background {
    width: 10rem;
    justify-content: center;
    & .bg-circle {
      width: 6rem;
      height: 6rem;
      border-radius: 50%;
    }
  }
  & .name {
    color: black;
    transition: $transition-time ease-out;
    &:hover {
      cursor: pointer;
      color: gray;
      transform: translate(3px);
    }
  }
  & .amount {
    color: black;
    font-size: 1.6rem;
  }
}

$radius: 1.5rem;
.rounded-top-borders {
  border-top-left-radius: $radius;
  border-top-right-radius: $radius;
}

.rounded-bottom-borders {
  border-bottom-left-radius: $radius;
  border-bottom-right-radius: $radius;
}

// MEDIA
@mixin subscription-container-media($width) {
  .subscription-container {
    width: $width;
    & > div {
      width: floor(($width - 10rem) / 5);
    }
  }
}

@media (max-width: 1600px) {
  @include subscription-container-media($width: 135rem);
}

@media (max-width: 1400px) {
  @include subscription-container-media($width: 115.3rem);
}

@media (max-width: 1200px) {
  @include subscription-container-media($width: 92.3rem);
}

@media (max-width: 1000px) {
  @include subscription-container-media($width: 76rem);
}

@media (max-width: 850px) {
  $width: 32rem;
  .subscription-container {
    grid-template-columns: repeat(2, auto);
    grid-template-rows: repeat(2, auto);
    width: $width;
    height: 8rem;
    & > div {
      justify-content: center;
      width: $width / 2;
      font-size: 1.3rem;
    }
    & .background,
    & .category {
      display: none;
    }
  }
}
</style>