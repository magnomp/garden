<script setup lang="ts">
const route = useRoute()

const { data } = await useAsyncData('content', () => queryContent(route.path).findOne())

useHead({
  title: data.value?.title
})

const youtubeRegex = /https:\/\/www.youtube.com\/watch\?(.*)/

const youtube = computed(() => {
  const match = data.value?.externalLink?.match(youtubeRegex)
  if (match) {
    const params = new URLSearchParams(match[1])
    return params.get('v')
  }
  else
    return null
})

</script>

<template>
  <main>
    <div class="font-sans py-4">
      <p class="text-base md:text-sm text-green-500 font-bold">&lt; <a href="/"
          class="text-base md:text-sm text-green-500 font-bold no-underline hover:underline">BACK TO INDEX</a></p>
      <p class="text-sm md:text-base font-normal text-gray-600">{{ data?._path?.split('/').slice(1, -1).join(' / ') }}</p>
      <h1 class="font-bold font-sans break-normal text-gray-900 pt-6 pb-2 text-3xl md:text-4xl">{{ data!.title }}</h1>
    </div>
    <div>
      <iframe v-if="youtube" width="560" height="315" :src="`https://www.youtube.com/embed/${youtube}`"></iframe>
      <ContentRenderer :value="data!" />
    </div>
  </main>
</template>