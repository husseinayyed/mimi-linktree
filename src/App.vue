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
  top: 50%;
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
</style>
