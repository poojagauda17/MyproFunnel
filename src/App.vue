<script setup lang="ts">
import Headerr from '@/components/header.vue'
import Banner from './components/banner.vue'
import Solution from './components/solution.vue'
import ReviewCarousel from './components/reviews-carousel.vue'
import Bonuses from './components/bonuses.vue'
import HeorTestimonial from './components/hero-testimonial.vue'
import ContactUs from './components/contact-us.vue'
import Footerr from './components/footerr.vue'




</script>

<template>
  <Headerr />
    <Banner />
    <Solution />
    <Bonuses />
    <ReviewCarousel />
    <HeorTestimonial />
    <ContactUs />
    <Footerr />
</template>

<style scoped>
:root{
   --white: #fff;
   --black: #000;
}
</style>
