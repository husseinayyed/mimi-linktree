<script setup>
import gsap from 'gsap';
import SplitText from 'gsap/SplitText';
import { onMounted } from 'vue';
import { desContext } from './context/arabic';
onMounted(()=>{
  document.fonts.ready.then(()=>{
    gsap.registerPlugin(SplitText)
    const title = new SplitText("h1.title",{
      type:"chars"
    })
    const des = new SplitText(".describe",{
      type:"words"
    })
    const tl = gsap.timeline()
    tl.from(title.chars,{
      opacity:0,
      duration:0.4,
      stagger:0.1,
      rotate:20,
      y:20,
      ease:"power1.out"
    })
    tl.from(des.words,{
      opacity:0,
      duration:0.4,
      stagger:0.2,
      y:20,
      ease:"power1.out"
    })

  })
})
</script>

<template>
  <main>
  <div class="icon">
    <div class="container">
      <div></div>
      <div></div>
      <div></div>
      <div></div>
    </div>
  </div>
    <h1 class="quicksand-bold title">MimiStore</h1>
    <div v-for="text in desContext">
      <p class="amiri-regular describe rtl">{{ text }}</p>
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
  display: inline;
}
.icon {
  overflow: hidden;
  display: none;
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
.icon .container::after {
  content: "S";
  position: absolute;
  top: -14%;
  left: 26%;
  font-size: 6rem;
  color: #00CFFF;
}
.icon .container div {
  width: 8px;
  height: 80px;
  background-color: purple;
  border-radius: 4px;
}
.icon .container div:nth-child(2) {
  transform: skewX(25deg);
  margin-right: 20px;
}
.icon .container div:nth-child(3) {
  transform: skewX(-25deg);
}
</style>
