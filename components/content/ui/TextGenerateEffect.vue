<template>
    <div :class="cn('leading-snug tracking-wide', props.class)">
      <div ref="scope">
        <span
          v-for="(word, idx) in words"
          :key="word.word + idx"
          class="inline-block"
          :style="{
            ...spanStyle,
            whiteSpace: 'break-spaces',
            opacity: timestamp > word.time + 1000 ? 1 : 0,
            filter: timestamp > word.time + 1000 ? 'blur(0px)' : 'blur(10px)'
          }"
        >
          {{ word.word }}
        </span>
      </div>
    </div>
  </template>
  
  <script setup lang="ts">
  import { computed, type HTMLAttributes, ref } from "vue";
  
  import { cn } from "@/lib/utils";
  
  const props = withDefaults(
    defineProps<{
      words: string;
      filter?: boolean;
      duration?: number;
      delay?: number;
      class?: HTMLAttributes["class"];
    }>(),
    { duration: 0.7, delay: 0, filter: true },
  );
  
  const scope = ref(null);
  const timestamp = useTimestamp({ offset: 0 })
  const spanStyle = computed(() => ({
    transition: `opacity ${props.duration}s, filter ${props.duration}s`,
  }));

  const words = ref<{
    word: string,
    time: number
  }[]>([])

  watch(()=> props.words, (newVal, oldValue) => {
    if(newVal.length > oldValue.length) {
      const newWord = newVal.slice(oldValue.length, newVal.length)
      words.value.push({
        word: newWord,
        time: Date.now()
      })
    }

  })
 
  </script>
