<script setup>
import { ref } from 'vue'
import { normalizePageHash, generateTimelineItems } from './functions'
import { PAGE_ACTIVITIES, PAGE_PROGRESS, PAGE_TIMELINE } from './constants'
import TheHeader from './components/TheHeader.vue'
import TheNav from './components/TheNav.vue'
import TheTimline from './pages/TheTimline.vue'
import TheActivities from './pages/TheActivities.vue'
import TheProgress from './pages/TheProgress.vue'

const currentPage = ref(normalizePageHash())

const timelineItems = generateTimelineItems()

const activities = ['Coding', 'Reading', 'Training']

function goTo(page) {
  currentPage.value = page
}
</script>

<template>
  <TheHeader @navigate="goTo($event)" />

  <main class="flex flex-grow flex-col">
    <TheTimline v-show="currentPage === PAGE_TIMELINE" :timeline-items="timelineItems" />
    <TheActivities v-show="currentPage === PAGE_ACTIVITIES" :activities="activities" />
    <TheProgress v-show="currentPage === PAGE_PROGRESS" />
  </main>

  <TheNav :current-page="currentPage" @navigate="goTo($event)" />
</template>
