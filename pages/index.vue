<template>
    <!--Title-->
    <div class="font-sans">
        <h1 class="font-bold font-sans break-normal text-gray-900 pt-6 pb-2 text-3xl md:text-4xl">Welcome to my digital
            garden</h1>
    </div>

    <p>This is my digital garden, a place where I share my thoughts and notes on be it courses, lectures, books, etc. A place where
        everything is unfinished by definition, where I am free to publish partial thoughts and either remove or modify them
        at will. Just like a real garden which is always a work in progress.</p>
    <p>Although the garden itself is in english, I might write in portuguese as well, usually acording with the origin
        material I`m consuming.</p>

    <ContentNavigation v-slot="{ navigation }">
    <ContentTree :navigation="navigation" />
</ContentNavigation></template>