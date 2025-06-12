<script setup lang="ts">
const props = defineProps<{
    navigation: any[]
}>()
</script>

<template>
        <ul>
            <li v-for="nav in navigation" :key="nav.path">
                <template v-if="nav.children">
                    {{ nav.title }}
                    <ContentTree v-if="nav.children" :navigation="nav.children"/>
                </template>
                <NuxtLink v-else :to="nav.path">{{ nav.title }}</NuxtLink>
            </li>
        </ul>
</template>