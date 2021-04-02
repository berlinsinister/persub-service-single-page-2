<template>
  <div class="payment-container">
    <div class="background" :style="{ background: background }"></div>
    <div class="amount-and-date">
      <div class="amount">$ {{ amount }}</div>
      <div class="date">{{ date }}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Payments",
  props: {
    background: String,
    amount: Number,
    date: {
      type: String,
      default: "Last Month",
    },
  },
};
</script>

<style lang="scss" scoped>
$width: 155rem;

.payment-container {
  display: grid;
  grid-template-columns: auto auto;
  grid-auto-rows: auto;
  grid-gap: 4rem;
  justify-content: start;
  width: floor($width / 4);
  height: 9rem;
  // border: 1px solid red;
  & .background {
    width: 9rem;
    height: 9rem;
    border-radius: 1rem;
  }
  & .amount-and-date {
    display: grid;
    align-content: center;
    grid-gap: 0.5rem;
    & .amount {
      font-size: 3rem;
      font-weight: 500;
    }
    & .date {
      color: gray;
    }
  }
}

// MEDIA
@mixin payment-container-media($width) {
  .payment-container {
    width: floor($width / 4);
  }
}

@media (max-width: 1600px) {
  @include payment-container-media($width: 135rem);
}

@media (max-width: 1400px) {
  @include payment-container-media($width: 115.3rem);
}

@media (max-width: 850px) {
  $width: 32rem;
  .payment-container {
    grid-gap: 1rem;
    width: 15rem;
    height: 5rem;
    // border: 1px solid red;
    & .background {
      width: 5rem;
      height: 5rem;
    }
    & .amount-and-date {
      grid-gap: 0.2rem;
      & .amount {
        font-size: 1.8rem;
      }
      & .date {
        font-size: 1.3rem;
      }
    }
  }
}
</style>