<template>
  <main>
    <div class="big-wrapper light">
      <img src="@/assets/shape.png" class="shape" alt="" />

      <Header />

      <Showcase />

      <Footer />
    </div>
  </main>
</template>

<script setup>
import { onMounted } from 'vue'

import Header from '@/components/Header.vue'
import Showcase from '@/components/Showcase.vue'
import Footer from '@/components/Footer.vue'

let main, toggle_btn, big_wrapper, hamburger_menu, dark = false

function declare()
{
  main = document.querySelector('main')
  toggle_btn = document.querySelector('.toggle-btn')
  big_wrapper = document.querySelector('.big-wrapper')
  hamburger_menu = document.querySelector('.hamburger-menu')
}

function toggleAnimation()
{
  dark = !dark

  let clone = big_wrapper.cloneNode(true)

  if (dark) {
    clone.classList.remove('light')
    clone.classList.add('dark')
  } else {
    clone.classList.remove('dark')
    clone.classList.add('light')
  }

  clone.classList.add('copy')
  main.appendChild(clone)

  document.body.classList.add('stop-scrolling')

  clone.addEventListener('animationend', () => {
    document.body.classList.remove('stop-scrolling')

    big_wrapper.remove()
    clone.classList.remove('copy')

    declare()
    events()
  })
}

function events()
{
  toggle_btn.addEventListener('click', toggleAnimation)

  hamburger_menu.addEventListener('click', () => {
    big_wrapper.classList.toggle('active')
  })
}

onMounted(() => {
  declare()
  events()
})
</script>

<style scoped>

</style>
