<template>
  <div class="header">
    <div class="header-content">
      <div class="logo"><b>Per</b>sub</div>
      <nav>
        <div class="home passive"><span class="lnr lnr-home"></span></div>
        <div class="events active">
          <span class="lnr lnr-calendar-full"></span>
        </div>
        <div class="profile">
          <img src="../assets/images/profile.jpg" alt="profile" />
          <div class="status"></div>
          <div class="name">Beka Kvartskhava</div>
        </div>
      </nav>
    </div>
  </div>
</template>

<script>
export default {
  name: "Header",
};
</script>

<style lang="scss" scoped>
@import "../assets/sass/vars";
@import "../assets/sass/mixins";

.header {
  position: fixed;
  top: 0;
  z-index: 100;
  height: 10rem;
  width: 100%;
  @include flex-centered-totally;
  background: white;
  box-shadow: 0 5px 10px -6px rgba(black, 0.1);
}

.header-content {
  width: 155rem;
  @include flex-space-between;
  // border: 1px solid crimson;
}

.logo {
  font-size: 4rem;
  color: $gray;
}

nav {
  display: flex;
  font-size: 1.8rem;
  font-weight: 500;
  & .home,
  & .events {
    margin-top: 3.7rem;
    padding: 0 9rem 2.7rem 9rem;
    transition: $transition-time ease-out;
    &:hover {
      cursor: pointer;
      color: $gray;
    }
  }
  & .events {
    margin-right: 35rem;
  }
  & .lnr-home,
  & .lnr-calendar-full {
    font-size: 3rem;
  }
  & .profile {
    width: 23rem;
    display: flex;
    align-items: center;
    position: relative;
    &:hover {
      cursor: pointer;
    }
    // border: 1px solid green;
    & img {
      width: 4rem;
      height: 4rem;
      border-radius: 50%;
      object-fit: cover;
      border: 2px solid white;
      box-shadow: 0 5px 10px -1px rgba(black, 0.2);
    }
    & .status {
      position: absolute;
      width: 1rem;
      height: 1rem;
      top: 5.7rem;
      left: 3rem;
      border-radius: 50%;
      background: #74c299;
      border: 2px solid white;
    }
    & .name {
      margin-left: 2rem;
      color: $gray;
      transition: $transition-time ease-out;
      &:hover {
        cursor: pointer;
        color: #a1a1a1;
      }
    }
  }
}

.active {
  border-bottom: 3px solid $gray;
  color: $gray;
}

.passive {
  color: #a1a1a1;
}

// MEDIA
@media (max-width: 1600px) {
  .header-content {
    width: 135rem;
  }
  nav {
    & .events {
      margin-right: 15rem;
    }
  }
}

@media (max-width: 1400px) {
  .header-content {
    width: 115.3rem;
  }
  nav {
    & .home,
    & .events {
      margin-right: 3rem;
      padding: {
        left: 0;
        right: 0;
      }
    }
  }
}

@media (max-width: 1200px) {
  .header-content {
    width: 92.3rem;
  }
}

@media (max-width: 1000px) {
  // .header {
  //   left: -1.1rem;
  // }
  .header-content {
    width: 76rem;
  }
}

@media (max-width: 850px) {
  .header-content {
    width: 32rem;
  }
  nav {
    & .home,
    & .events {
      margin-right: 2rem;
    }
    & .profile {
      width: auto;
    }
    .name {
      display: none;
    }
  }
}
</style>