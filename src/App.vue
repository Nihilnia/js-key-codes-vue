<template>
  <home-page></home-page>
  <div class="particle"></div>
</template>

<script>
import HomePage from "./components/pages/HomePage.vue";

export default {
  components: {
    HomePage,
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap");

* {
  transition: all 0.3s ease;
}

body {
  margin: 0;
  font-family: "Poppins", serif;
  background-image: url("./assets/bg_3.jpg");
  font-size: 20px;
  color: #fff;
  display: grid;
  place-items: center;
  height: 100vh;
}

.particle {
  position: absolute;
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background-color: rgba(255, 255, 255, 0.8);
  animation: moveParticle 4s infinite;
}

@keyframes moveParticle {
  0% {
    transform: translate(0, 0);
    opacity: 1;
  }
  50% {
    opacity: 0.5;
  }
  100% {
    transform: translate(calc(100vw * 0.5), calc(100vh * 0.5));
    opacity: 0;
  }
}

.particle:nth-child(1) {
  animation-delay: 0s;
  left: 10%;
  top: 10%;
}
.particle:nth-child(2) {
  animation-delay: 1s;
  left: 20%;
  top: 20%;
}
.particle:nth-child(3) {
  animation-delay: 2s;
  left: 30%;
  top: 30%;
}
.particle:nth-child(4) {
  animation-delay: 3s;
  left: 40%;
  top: 40%;
}
.particle:nth-child(5) {
  animation-delay: 0.5s;
  left: 50%;
  top: 50%;
}
.particle:nth-child(6) {
  animation-delay: 1.5s;
  left: 60%;
  top: 60%;
}
.particle:nth-child(7) {
  animation-delay: 2.5s;
  left: 70%;
  top: 70%;
}
.particle:nth-child(8) {
  animation-delay: 3.5s;
  left: 80%;
  top: 80%;
}
</style>
