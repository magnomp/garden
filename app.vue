<script setup lang="ts">
import IconInstagram from '~icons/fa-brands/instagram'
import IconGithub from '~icons/fa-brands/github'
import IconLinkedin from '~icons/fa-brands/linkedin'

useHead({
  bodyAttrs: {
    class: "bg-gray-100 font-sans leading-normal tracking-normal"
  },
  script: [
    { src: "https://www.googletagmanager.com/gtag/js?id=G-QVZYXS32CY", async: true }
  ]
})

onMounted(() => {
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());

  gtag('config', 'G-QVZYXS32CY');
})

const scrollPos = ref(0)
const scroll = ref(0)
const isNavbarHidden = ref(false)
const isBrowser = typeof (window) != 'undefined'
const html = isBrowser ? document.documentElement : null
const body = isBrowser ? document.body : null

const onScroll = () => {
  scroll.value = (html!.scrollTop || body!.scrollTop) / ((html!.scrollHeight || body!.scrollHeight) - html!.clientHeight) * 100;
  scrollPos.value = window.scrollY
}

onMounted(() => {
  scrollPos.value = window.scrollY

  document.addEventListener('scroll', onScroll)
})

onUnmounted(() => {
  document.removeEventListener('scroll', onScroll)
})
</script>

<template>
  <div class="flex flex-col min-h-screen">
  <nav class="fixed w-full z-10 top-0" :class="{ 'bg-white': scrollPos > 10, shadow: scrollPos > 10 }">

    <div class="h-1 z-20 top-0" :style="`background:linear-gradient(to right, #4dc0b5 ${scroll}%, transparent 0);`"></div>

    <div class="w-full md:max-w-4xl mx-auto flex flex-wrap items-center justify-between mt-0 py-3">

      <div class="pl-4">
        <a class="text-gray-900 text-base no-underline hover:no-underline font-extrabold text-xl" href="/">
          Magno Machado / Digital garden
        </a>
      </div>

      <div class="block lg:hidden pr-4">
        <button @click="isNavbarHidden = !isNavbarHidden"
          class="flex items-center px-3 py-2 border rounded text-gray-500 border-gray-600 hover:text-gray-900 hover:border-green-500 appearance-none focus:outline-none">
          <svg class="fill-current h-3 w-3" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
            <title>Menu</title>
            <path d="M0 3h20v2H0V3zm0 6h20v2H0V9zm0 6h20v2H0v-2z" />
          </svg>
        </button>
      </div>

      <div v-show="!isNavbarHidden"
        class="w-full flex-grow lg:flex lg:items-center lg:w-auto lg:block mt-2 lg:mt-0 bg-gray-100 md:bg-transparent z-20"
        :class="{ 'bg-white': scrollPos > 10, 'bg-gray-100': scrollPos <= 10 }">

        <ul class="list-reset lg:flex justify-end flex-1 items-center list-none">
          <li class="mr-3">
            <a href="https://instagram.com/magnomp"><IconInstagram class="text-gray-900"/></a>
          </li>
          <li class="mr-3">
            <a href="https://github.com/magnomp"><IconGithub class="text-gray-900"/></a>
          </li>
          <li class="mr-3">
            <a href="https://www.linkedin.com/in/magno-machado-b5557110/"><IconLinkedin class="text-gray-900"/></a>
          </li>
        </ul>
      </div>
    </div>
  </nav>

  <!--Container-->
  <div class="container w-full md:max-w-3xl mx-auto pt-20 flex-grow">

    <div class="w-full px-4 md:px-6 text-xl text-gray-800 leading-normal" style="font-family:Georgia,serif;">

      <NuxtPage />

    </div>

  </div>
  <!--/container-->

  <footer class="bg-white border-t border-gray-400 shadow h-fit">
    <div class="container max-w-4xl mx-auto flex py-8">

      <div class="w-full mx-auto flex flex-wrap">
        <div class="flex w-full ">
          <div class="px-8">
            <p class="text-gray-600 text-xs md:text-base">Based on <a
                href="https://www.tailwindtoolbox.com/templates/minimal-blog">Minimal Blog</a> Tailwind CSS template by <a
                href="https://www.tailwindtoolbox.com">TailwindToolbox.com</a></p>
          </div>
        </div>
      </div>
    </div>
  </footer>
</div>
</template>
