<script lang="ts" setup>
import Hero from "@/components/Hero.vue";
import HomeCards from "@/components/HomeCards.vue";
import JobListing from "@/components/JobListing.vue";
</script>

<template>
  <Hero title="Test title" subtitle="Test subtitle" />
  <HomeCards />
  <JobListing :limit="3" :show-button="true" />
</template>
