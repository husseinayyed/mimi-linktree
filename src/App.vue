<script setup>
import gsap from 'gsap';
import SplitText from 'gsap/SplitText';
import { onMounted } from 'vue';
import { desContext } from './context/arabic';
import links from './context/links';
onMounted(()=>{
  document.fonts.ready.then(()=>{
    gsap.registerPlugin(SplitText)
    const title = new SplitText("h1.title",{
      type:"chars"
    })
    
    const tl = gsap.timeline()
    tl.from(".icon .container .bar",{
      duration:1,
      ease:"power2.inOut",
      stagger:0.5,
      opacity:0,
      height:0
    })
    tl.from(".icon .container .after-element",{
      duration:1,
      ease:"power2.inOut",
      opacity:0,
    },"+=0.1")
    tl.from(title.chars,{
      opacity:0,
      duration:0.4,
      stagger:0.1,
      rotate:20,
      y:20,
      ease:"power1.out"
    },"-=0.4")
    tl.from("p.describe",{
      opacity:0,
      duration:0.6,
      x:5,
      y:-5,
      ease:"power1.in"
    },"-=0.6")
    tl.from(".social-media img",{
      opacity:0,
      duration:0.4,
      stagger:0.2,
      y:10,
      x:10,
      ease:"power1.out"
    },"+=0.2")

  })
})
function goLink(link) {
  location.href = link
}
</script>

<template>
  <main>
  <div class="icon">
    <div class="container">
      <div class="bar"></div>
      <div class="bar"></div>
      <div class="bar"></div>
      <div class="bar"></div>
      <div class="after-element">S</div>
    </div>
  </div>
    <h1 class="quicksand-bold title">MimiStore</h1>
    <div v-for="text in desContext">
      <p class="amiri-regular describe rtl">{{ text }}</p>
    </div>
    <div class="social-media">
      <div class="image-wrapper" :key="link.id" v-for="link in links">
        <img :src="link.src" @click="goLink(link.link)" :alt="link.app">
      </div>
    </div>
  </main>
  
</template>

<style scoped>
main {
  width: 100%;
  position: absolute;
  top: 45%;
  left: 50%;
  transform: translate(-50%,-50%);
  display: flex;
  justify-content: center;
  align-items: center;
  flex-flow: column wrap;
}
.describe {
  font-size: 1.28em;
  display: block;
  margin: 0;
}
.icon {
  overflow: hidden;
  width: 80px;
  height: 80px;
  background-color: transparent;
}
.icon .container {
  width: 100%;
  height: 100%;
  display: flex;
  position: relative;
  justify-content: space-between;
  flex-flow: row nowrap;
}
.icon .after-element {
  position: absolute;
  top: -14%;
  left: 26%;
  opacity: 1;
  font-size: 6rem;
  color: #00CFFF;
}
.icon .container .bar {
  width: 8px;
  height: 80px;
  background-color: purple;
  border-radius: 4px;
}
.icon .container .bar:nth-child(2) {
  transform: skewX(25deg);
  margin-right: 20px;
}
.icon .container .bar:nth-child(3) {
  transform: skewX(-25deg);
}
.social-media {
  display: flex;
  gap: 10px;
}
img {
  width:40px;
  height:40px;
  border-radius: 50%;
  cursor: pointer;
}
</style>
