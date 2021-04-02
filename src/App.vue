<template>
  <Header />
  <main>
    <div class="payments">
      <div v-for="(detail, index) in paymentDetails" :key="index">
        <Payments
          :background="detail.background"
          :amount="detail.amount"
          :date="detail.date"
        />
      </div>
    </div>
    <div class="subscriptions">
      <div class="title">Subscriptions</div>
      <div class="subscription-head">
        <div class="background-head"></div>
        <div>Name</div>
        <div>Category</div>
        <div>Date</div>
        <div>Frequency</div>
        <div>Amount</div>
      </div>
      <div class="subscription-body">
        <div v-for="(detail, index) in subscriptionDetails" :key="index">
          <Subscriptions
            :background="detail.background"
            :name="detail.name"
            :category="detail.category"
            :frequency="detail.frequency"
            :amount="detail.amount"
            :id="
              index === subscriptionDetails.length - 1
                ? 'last-child'
                : index === 0
                ? 'first-child'
                : ''
            "
            @popup="popupHandler"
          />
        </div>
      </div>
    </div>
    <div v-show="popup" class="popup" :style="{ height: scrollHeight + 'px' }">
      <div class="popup-body">
        <Popup :details="popupDetails" />
        <div class="close" @click="popup = false">&times;</div>
      </div>
    </div>
  </main>
</template>

<script>
import Header from "./components/Header.vue";
import Payments from "./components/Payments.vue";
import Subscriptions from "./components/Subscriptions.vue";
import Popup from "./components/Popup.vue";

export default {
  name: "App",
  components: { Header, Payments, Subscriptions, Popup },
  data() {
    return {
      popup: false,
      scrollHeight: "", // document.documentElement.scrollHeight,
      popupDetails: {
        background: "",
        name: "",
        frequency: "",
        amount: "",
      },
      paymentDetails: [
        {
          background: "linear-gradient(135deg, #b8e5c5, #f8e0ad)",
          amount: 124.43,
        },
        {
          background: "linear-gradient(135deg, #f19eaf, #f8e0ad)",
          amount: 94,
        },
        {
          background: "linear-gradient(135deg, #abe4ef, #f8e0ad)",
          amount: 324.43,
        },
        {
          background: "linear-gradient(135deg, #b5c0f2, #f8e0ad)",
          amount: 24.87,
        },
      ],
      subscriptionDetails: [
        {
          background: "#58c8fa",
        },
        {
          background: "#ed70ac",
          frequency: "Monthly",
          amount: 6.45,
        },
        {
          background: "#7467f6",
          frequency: "Monthly",
        },
        {
          background: "#f7c761",
          frequency: "Monthly",
        },
        {
          background: "#eb345c",
        },
        {
          background: "#2c506f",
        },
      ],
    };
  },
  mounted() {
    this.scrollHeight = document.documentElement.scrollHeight;
    this.$nextTick(() => {
      window.addEventListener("resize", this.onResize);
    });
  },
  beforeUnmount() {
    window.removeEventListener("resize", this.onResize);
  },
  methods: {
    popupHandler(details) {
      this.popup = true;
      this.popupDetails = Object.assign({}, details);
    },
    onResize() {
      this.scrollHeight = document.documentElement.scrollHeight;
    },
  },
};
</script>

<style lang="scss">
@import "./assets/sass/vars";
@import "./assets/sass/mixins";

$width: 155rem;

:root {
  font-size: $font-size;
}

html,
body {
  @include reset;
}

body {
  font: {
    family: $font-family;
    size: 1.4rem;
    weight: 400;
  }
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background: #f8f8f8;
}

main {
  display: grid;
  grid-template-columns: auto;
  grid-auto-rows: auto;
  justify-content: center;
  grid-gap: 7rem;
  margin: 15rem 0 7rem 0;
  & > div {
    // border: 1px solid royalblue;
  }
}

.payments {
  display: grid;
  grid-template-columns: repeat(4, auto);
  grid-auto-rows: auto;
  justify-content: space-between;
}

.grid-settings {
  display: grid;
  grid-template-columns: auto;
  grid-auto-rows: auto;
  grid-gap: 2px;
}

.subscriptions {
  @extend .grid-settings;
  & .title {
    font-size: 2.5rem;
    font-weight: 500;
    padding-bottom: 4rem;
  }
  & .subscription-head {
    display: grid;
    grid-template-columns: repeat(6, auto);
    grid-auto-rows: auto;
    width: $width;
    height: 5rem;
    & > div {
      display: grid;
      align-content: center;
      width: floor(($width - 10rem) / 5); // 29rem;
      color: black;
      font-size: 1.5rem;
      font-weight: 500;
    }
    & .background-head {
      width: 10rem;
    }
  }
  & .subscription-body {
    @extend .grid-settings;
    @include around-shadow;
  }
}

.popup {
  position: absolute;
  overflow-y: scroll;
  overflow-x: hidden;

  // position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  // height: 100vh;
  background: rgba($color: white, $alpha: 0.8);
  & .popup-body {
    /** center of the screen */
    position: absolute;
    left: 50%;
    transform: translate(-50%, 0);
    /** */
    margin-top: 20rem;
    display: flex;
    align-items: flex-start;
    & .close {
      margin-left: 2rem;
      font-size: 4rem;
      transition: $transition-time ease-out;
      &:hover {
        cursor: pointer;
        transform: rotate(90deg);
      }
    }
  }
}

.opacity {
  opacity: 0.9;
}

// MEDIA
@mixin subscription-head-media($width) {
  .subscriptions {
    & .subscription-head {
      width: $width;
      & > div {
        width: floor(($width - 10rem) / 5);
      }
    }
  }
}

@media (max-width: 1600px) {
  @include subscription-head-media($width: 135rem);
}

@media (max-width: 1400px) {
  @include subscription-head-media($width: 115.3rem);
}

@media (max-width: 1200px) {
  .payments {
    display: grid;
    grid-template-columns: repeat(2, auto);
    grid-auto-rows: auto;
    justify-content: center;
    grid-gap: 2rem;
  }
  @include subscription-head-media($width: 92.3rem);
}

@media (max-width: 1000px) {
  @include subscription-head-media($width: 76rem);
}

@media (max-width: 850px) {
  main {
    grid-gap: 3rem;
  }
  .payments {
    justify-content: space-between;
  }
  .subscriptions {
    & .title {
      padding-bottom: 2rem;
    }
    & .subscription-head {
      display: none;
    }
  }
}
</style>