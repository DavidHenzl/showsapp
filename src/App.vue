<script setup>
  import BreakingBadCardsSuspense from '@/components/BreakingBadCardsSuspense.vue'
  import RickMortyCards from '@/components/RickMortyCards.vue'
  import Hero from './components/Hero.vue'
  import { ref } from 'vue'

  const isBreakingBad = ref(false)
</script>

<template>
  <main>
    <Hero
      :isBreakingBad="isBreakingBad"
      @selectShow="isBreakingBad = !isBreakingBad"
    />
    <KeepAlive>
      <Component :is="isBreakingBad ? BreakingBadCardsSuspense : RickMortyCards" />
    </KeepAlive>
  </main>
</template>
