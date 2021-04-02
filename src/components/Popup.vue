<template>
  <div class="popup-container">
    <div class="company-info">
      <div class="logo-name-and-subscription-type">
        <div class="logo" :style="{ background: details.background }"></div>
        <div class="name-and-subscription-type">
          <div class="name">{{ details.name }}</div>
          <div class="subscription-type">
            {{ details.frequency }} Subscription
          </div>
        </div>
      </div>
      <div class="unsubscription-options">
        <button class="unsubscribe-button">Unsubscribe</button>
        <div class="unsubscription-policy">Unsubscription Policy</div>
      </div>
    </div>
    <div class="transaction-info">
      <div class="transaction-history">
        <div class="title">Transaction History</div>
        <div class="header">
          <div>Date</div>
          <div>Amount</div>
        </div>
        <div class="body">
          <div class="container" v-for="index in 4" :key="index">
            <div class="gray">March, 9th 14:45</div>
            <div class="bold">14.45$</div>
          </div>
        </div>
      </div>
      <div class="delivery-history">
        <div class="title">Delivery History</div>
        <div class="header">
          <div>Date</div>
          <div>Delivered by</div>
        </div>
        <div class="body">
          <div class="container" v-for="index in 4" :key="index">
            <div class="gray">April, 9th 14:45</div>
            <div class="bold">Glovo</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Popup",
  props: {
    details: Object,
  },
};
</script>

<style lang="scss" scoped>
@import "../assets/sass/vars";
@import "../assets/sass/mixins";

$container-width: 112rem;
$container-height: 49rem;
$inner-width: 100rem;

.popup-container {
  display: grid;
  grid-template-columns: auto;
  grid-template-rows: auto auto;
  justify-content: center;
  align-content: center;
  width: $container-width;
  height: $container-height;
  background: white;
  border-radius: 1.5rem;
  @include around-shadow;
  & > div {
    // border: 1px solid green;
  }
  & .company-info {
    width: $inner-width;
    height: 11rem;
    & > div {
      //   border: 1px solid blue;
    }
    display: grid;
    grid-template-columns: auto auto;
    grid-template-rows: auto;
    justify-content: space-between;
    align-content: start;
    border-bottom: 1px solid gainsboro;
    & .logo-name-and-subscription-type {
      display: grid;
      grid-template-columns: auto auto;
      grid-template-rows: auto;
      grid-gap: 2rem;
      justify-content: start;
      & > div {
        // border: 1px solid red;
      }
      & .logo {
        $size: 7.5rem;
        width: $size;
        height: $size;
        border-radius: 50%;
      }
      & .name-and-subscription-type {
        display: grid;
        align-content: center;
        grid-gap: 0.5rem;
        & .name {
          font-weight: 500;
          font-size: 2rem;
        }
        & .subscription-type {
          color: gray;
        }
      }
    }
    & .unsubscription-options {
      display: grid;
      grid-gap: 0.5rem;
      & .unsubscribe-button {
        width: 35rem;
        height: 5rem;
        background: white;
        color: black;
        border: 1px solid black;
        border-radius: 2px;
        font-size: 1.5rem;
        font-weight: 600;
        transition: $transition-time ease-out;
        &:focus {
          outline: none;
        }
        &:hover {
          cursor: pointer;
          color: white;
          background: black;
        }
      }
      & .unsubscription-policy {
        color: gray;
        font-size: 1.2rem;
        text-align: center;
      }
    }
  }
  & .transaction-info {
    $width: $inner-width;
    // border: 1px solid salmon;
    width: $width;
    height: 26rem;
    display: grid;
    grid-template-columns: repeat(2, ($inner-width - 4rem) / 2);
    align-content: end;
    justify-content: space-between;
    // grid-gap: 4rem;
    & .transaction-history,
    & .delivery-history {
      display: grid;
      grid-template-rows: repeat(3, auto);
      grid-gap: 2rem;
      //   border: 1px solid green;
      font-size: 1.5rem;
      & .title {
        font-weight: 500;
        font-size: 2rem;
      }
      & .header {
        display: grid;
        grid-template-columns: auto auto;
        justify-content: space-between;
        font-weight: 500;
      }
      & .body {
        display: grid;
        grid-template-rows: repeat(4, auto);
        grid-gap: 2rem;
        & .container {
          display: grid;
          grid-template-columns: auto auto;
          justify-content: space-between;
        }
      }
    }
  }
}
.gray {
  color: gray;
}
.bold {
  font-weight: 500;
}

@media (max-width: 1200px) {
  $container-width: 32rem; // 112rem;
  $inner-width: 26rem; // 100rem; 6 rem difference

  .popup-container {
    width: $container-width;
    height: auto;
    grid-gap: 3rem;
    padding: 3rem 0;
    & .company-info {
      width: $inner-width;
      height: auto; // 11rem;
      grid-template-columns: auto;
      grid-template-rows: auto auto;
      justify-content: center; // space-between;
      align-content: start;
      grid-gap: 2rem;
      border-bottom: none;
      & .logo-name-and-subscription-type {
        & .logo {
          $size: 6rem;
          width: $size;
          height: $size;
        }
        & .name-and-subscription-type {
          & .name {
            font-size: 1.8rem;
          }
        }
      }
      & .unsubscription-options {
        & .unsubscribe-button {
          width: $inner-width;
          height: 4rem;
        }
      }
    }
    & .transaction-info {
      width: $inner-width;
      height: auto; // 26rem;
      grid-template-columns: $inner-width;
      grid-auto-rows: auto; // columns: repeat(2, ($inner-width - 4rem) / 2);
      align-content: start;
      justify-content: space-between;
      grid-gap: 2rem;
      & .transaction-history,
      & .delivery-history {
        grid-gap: 1rem;
        font-size: 1.4rem;
        & .title {
          font-size: 1.8rem;
        }
      }
    }
  }
}
</style>