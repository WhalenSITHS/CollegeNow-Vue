<template>
  <section class="first">
    <div class="first-bg">
      <h1 class="first-header first-word">GSAP</h1>
      <div class="reveal-color reveal-1"></div>
    </div>
    <div class="second-bg">
      <h1 class="first-header second-word">Is Pretty Cool</h1>
      <div class="reveal-color reveal-2"></div>
    </div>
  </section>
  <section class="second">
    <video
      src="../assets/video.mp4"
      class="bg-video"
      autoplay
      loop
      muted
    ></video>
    <video
      src="../assets/video.mp4"
      class="bg-video wendy-2"
      autoplay
      loop
      muted
    ></video>
    <h1 class="second-header wendy-1">GSAP With Video Is Neat</h1>
    <h1 class="second-header wendy-2">GSAP With Video Is Neat</h1>
  </section>
  <section class="third">
    <h1 class="third-header">GSAP TEXT ANIMATIONS</h1>
  </section>
  <section class="fourth">
    <div class="hero">
      <h1 class="hero__heading">Welcome to my website</h1>
    </div>

    <div class="hero hero--secondary" aria-hidden="true" data-hero>
      <p class="hero__heading">Welcome to my website</p>
    </div>
  </section>
</template>

<script setup>
import { onMounted } from "vue";
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";
gsap.registerPlugin(ScrollTrigger);
onMounted(() => {
  const firstSection = {
    firstWord: document.querySelector(".first-word"),
    secondWord: document.querySelector(".second-word"),
    words: document.querySelectorAll("first-header"),
    firstBG: document.querySelector(".first-bg"),
    secondBG: document.querySelector(".second-bg"),
  };
  const tl = gsap.timeline({ delay: 0.5 });

  /* tl.to(firstSection.firstBG, { scaleX: 1 }); */
  tl.to(".reveal-1", { width: "100%", duration: 0.2 });
  tl.to(".reveal-2", { width: "100%", duration: 0.2 });
  tl.to(".first-header", { opacity: 1, duration: 0.1 });
  tl.to(".reveal-1", { width: "0%", duration: 0.2 });
  tl.to(".reveal-2", { width: "0%", duration: 0.2 });

  const tl2 = gsap.timeline({ scrollTrigger: ".second", delay: 0.3 });
  tl2.to(".wendy-2", {
    opacity: 0,
    duration: 1,
  });

  const letters = document.querySelector(".third-header").textContent;
  const lettersArr = Array.from(letters);
  function createLetterSpans() {
    let node = document.querySelector(".third-header");
    node.innerHTML = "";
    lettersArr.forEach((letter) => {
      node.insertAdjacentHTML(
        "beforeend",
        `<span class="letter-span">${letter}</span>`
      );
    });
  }

  createLetterSpans();
  const tl3 = gsap.timeline({ scrollTrigger: ".third-header", delay: 0.2 });
  tl3.from(".letter-span", {
    opacity: 0,
    y: -20,
    stagger: 0.05,
  });

  const tl4 = gsap.timeline({ scrollTrigger: ".hero__heading", delay: 0.2 });
  tl4.to(".hero--secondary", {
    "--mask": "radial-gradient(circle at 50% 50%, black 100%, transparent 0)",
    duration: 1,
    ease: "bounce.out",
  });
});
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Lato:wght@400;700&display=swap");
html,
body,
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  font-size: 62.5%;
  font-family: "Lato";
}
.first {
  height: 100vh;
  background-color: white;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.first-header {
  text-transform: uppercase;
  color: black;
  margin: 1rem auto;
  width: 100%;
  opacity: 0;
  width: 100%;
  position: absolute;
  height: 100%;
  top: 0;
  left: 0;
}
.first-bg,
.second-bg {
  position: relative;
  width: 60rem;
  height: 20%;
  margin: 1rem auto;
}
.reveal-1 {
  width: 0;
  top: 0;
  left: 0;
  position: absolute;
  display: inline-block;
  height: 100%;
  background-color: blue;
}
.reveal-2 {
  width: 0;
  top: 0;
  left: 0;
  position: absolute;
  display: inline-block;
  height: 100%;
  background-color: green;
}
.second,
.third {
  height: 100vh;

  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  position: relative;
}
.bg-video {
  top: 0;
  left: 0;
  position: absolute;
  width: 100%;
  height: 100%;
  object-fit: cover;
}
.second-header {
  text-transform: uppercase;
  color: #fff;
  position: absolute;
  inset: 0;
  display: grid;
  place-items: center;
  background-color: #000;
  font-weight: 900;
  font-size: 20rem;
  mix-blend-mode: multiply;
}
.wendy-1,
.wendy-2 {
  text-transform: uppercase;
  color: #fff;
  position: absolute;
  inset: 0;
  display: grid;
  place-items: center;
  background-color: #000;
  font-weight: 900;
  font-size: 20rem;
}
.wendy-2 {
  mix-blend-mode: normal;
  z-index: 2;
  background-color: transparent;
}
.letter-span {
  display: inline-block;
  letter-spacing: 1rem;
}

.fourth {
  position: relative;
  height: 100vh;
  background-color: rgb(9, 14, 23);
  color: #ffffff;
}
.hero {
  min-height: 100vh;
  padding: clamp(1rem, 2vw, 5rem);
  display: flex;
  align-items: center;
}

.hero--secondary {
  --mask: radial-gradient(circle at 50% 50%, black 0%, transparent 0);
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(45deg, #40e0d0, #9932cc, #ff1493, orange);
  color: rgb(9, 14, 23);
  -webkit-mask-image: var(--mask);
  mask-image: var(--mask);
}

.hero__heading {
  font-size: clamp(2rem, 5vw, 8rem);
  text-transform: uppercase;
  margin: 0;
}
</style>
