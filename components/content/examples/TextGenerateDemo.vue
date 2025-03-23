<template>
    <ClientOnly>
      <div class="flex h-64 items-center justify-center max-lg:w-full min-md:flex-1">
        <TextGenerateEffect
          :words="words"
        />
      </div>
    </ClientOnly>
  </template>
  
<script setup lang="ts">
const content = "Nuxt is an open source framework that makes web development intuitive and powerful.Create performant and production-grade full-stack web apps and websites with confidence."
const contentList = content.split(" ")

const words = ref("")
const {pause} = useIntervalFn(()=>{
  if(!contentList.length) {
    pause()
    return
  }
  const word = contentList.shift() + " "
  words.value += word
}, () => Math.random() * 200)

</script>
  
  