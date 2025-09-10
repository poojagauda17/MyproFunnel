<template>
  <section class="tc" aria-label="Testimonials">
    <header class="tc__head">
      <h3 class="tc__title">Customer Reviews</h3>
    </header>

    <div
      class="tc__stage"
      ref="stage"
      @mouseenter="pause"
      @mouseleave="play"
      tabindex="0"
      @keydown.left.prevent="prev"
      @keydown.right.prevent="next"
    >
      <!-- prev -->
      <button class="tc__nav tc__nav--prev" @click="prev" aria-label="Previous">
        <svg viewBox="0 0 24 24" width="18" height="18">
          <path fill="currentColor" d="M15.41 7.41 14 6l-6 6 6 6 1.41-1.41L10.83 12z"/>
        </svg>
      </button>

      <!-- cards -->
      <ul class="tc__stack">
        <li
          v-for="(s, i) in slides"
          :key="i"
          class="tc__wrap"
          :class="{
            'is-center': delta(i) === 0,
            'is-left'  : delta(i) === -1,
            'is-right' : delta(i) === 1
          }"
          :style="styleFor(i)"
        >
          <article class="card">
            <div class="card__avatar">
              <img :src="s.avatar" :alt="s.name" />
            </div>
            <div class="card__name">{{ s.name }}</div>
            <div class="card__role">{{ s.role }}</div>
            <blockquote class="card__quote">“ {{ s.text }} ”</blockquote>
          </article>
        </li>
      </ul>

      <!-- next -->
      <button class="tc__nav tc__nav--next" @click="next" aria-label="Next">
        <svg viewBox="0 0 24 24" width="18" height="18">
          <path fill="currentColor" d="M8.59 16.59 10 18l6-6-6-6-1.41 1.41L13.17 12z"/>
        </svg>
      </button>
    </div>

    <!-- dots -->
    <div class="tc__dots">
      <button
        v-for="(s, i) in slides"
        :key="'d'+i"
        :class="['tc__dot', { active: current === i }]"
        @click="go(i)"
        aria-label="Go to testimonial"
      />
    </div>
  </section>
</template>

<script setup>
import { ref, computed, onMounted, onBeforeUnmount } from 'vue'

/* Dummy data – replace with yours */
const slides = [
  {
    name: 'Hanna Lisem',
    role: 'Project Manager',
    text: 'Nam libero tempore, cum soluta nobis est eligendi optio cumque nihil impedit quo minus id quod maxime placeat.',
    avatar: 'https://i.pravatar.cc/120?img=32',
  },
  {
    name: 'Ronne Galle',
    role: 'Project Manager',
    text: 'Nam libero tempore, cum soluta nobis est eligendi optio cumque nihil impedit quo minus id quod maxime placeat.',
    avatar: 'https://i.pravatar.cc/120?img=12',
  },
  {
    name: 'Missy Limana',
    role: 'Engineer',
    text: 'Nam libero tempore, cum soluta nobis est eligendi optio cumque nihil impedit quo minus id quod maxime placeat.',
    avatar: 'https://i.pravatar.cc/120?img=5',
  },
  {
    name: 'Arun Mehta',
    role: 'Coach',
    text: 'Landing pages + calendar + payments = all-in-one. Conversions up, headache down.',
    avatar: 'https://i.pravatar.cc/120?img=8',
  },
  {
    name: 'Isha Kulkarni',
    role: 'Educator',
    text: 'Teen tools hata diye. Analytics clean hai, funnels reliable. Team ko bahut pasand aaya.',
    avatar: 'https://i.pravatar.cc/120?img=48',
  },
]

/* Carousel state */
const current = ref(1) // center the second card initially (like screenshot)
function next() { current.value = (current.value + 1) % slides.length }
function prev() { current.value = (current.value - 1 + slides.length) % slides.length }
function go(i)   { current.value = i }

/* Offset helper (-1,0,1 relative to current) */
function delta(i) {
  const n = slides.length
  let d = i - current.value
  if (d > n/2) d -= n
  if (d < -n/2) d += n
  // clamp to -1..1 for the "three card" look
  if (d > 1) d = 2
  if (d < -1) d = -2
  return d
}

/* Card transform per position */
const SHIFT = 380 // px horizontal shift between cards (desktop)
function styleFor(i) {
  const d = delta(i)
  let x = 0, s = 1, o = 1, blur = 0, z = 3

  if (d === -1) { x = -SHIFT; s = 0.9;  o = 0.45; blur = 1.2; z = 1 }
  if (d ===  1) { x =  SHIFT; s = 0.9;  o = 0.6;  blur = 0.8; z = 2 }
  if (d !== 0 && Math.abs(d) > 1) { o = 0; z = 0 }

  return {
    transform: `translate(calc(-50% + ${x}px), -50%) scale(${s})`,
    opacity: String(o),
    filter: `blur(${blur}px)`,
    zIndex: String(z),
    pointerEvents: d === 0 ? 'auto' : 'none'
  }
}

/* Autoplay with pause on hover / off-screen */
let timer = 0, io
const stage = ref(null)
function play() { if (!timer) timer = setInterval(next, 4000) }
function pause() { clearInterval(timer); timer = 0 }

onMounted(() => {
  io = new IntersectionObserver((entries) => {
    entries[0].isIntersecting ? play() : pause()
  }, { threshold: 0.25 })
  io.observe(stage.value)
})
onBeforeUnmount(() => { pause(); io && io.disconnect() })
</script>

<style scoped>
:root{
  --bg: #f3f7ff;
  --ink: #0f2338;
  --muted: #7b8ca7;
  --card: #ffffff;
  --shadow: 0 18px 40px rgba(14, 30, 70, 0.15);
  --radius: 16px;
  --primary: #2da7ff;
}

/* Section */
.tc{
  padding: 32px 5% 34px;
  background: linear-gradient(180deg, #f8fbff, #eff6ff);
  color: var(--ink);
}
.tc__head { text-align: center; margin-bottom: 10px; }
.tc__title { font-size: clamp(18px, 3vw, 22px); font-weight: 800; }

/* Stage */
.tc__stage{
  position: relative;
  margin: 18px auto 0;
  max-width: 1100px;
  height: 320px;
}
.tc__stack{ position: relative; height: 100%; }
.tc__wrap{
  position: absolute; left: 50%; top: 50%;
  transition: transform .45s cubic-bezier(.2,.7,.2,1),
              opacity .35s ease, filter .35s ease, z-index .2s ease;
  will-change: transform, opacity, filter;
}

/* Card design */
.card{
  width: 360px;
  border-radius: var(--radius);
  background: var(--card);
  box-shadow: var(--shadow);
  padding: 22px 22px 18px;
  text-align: center;
}
.card__avatar{
  width: 84px; height: 84px; border-radius: 50%;
  margin: 0 auto 10px; overflow: hidden;
  box-shadow: 0 8px 20px rgba(0,0,0,.1);
}
.card__avatar img{ width: 100%; height: 100%; object-fit: cover; display: block; }
.card__name{ font-weight: 800; color: var(--primary); margin-top: 2px; }
.card__role{ color: var(--muted); font-size: 13px; margin-top: 2px; }
.card__quote{
  margin-top: 10px;
  color: #3b4e68;
  font-size: 14px;
  line-height: 1.6;
}

/* Nav arrows */
.tc__nav{
  position:absolute; top:50%; transform:translateY(-50%);
  width:38px; height:38px; border-radius:50%;
  border:1px solid rgba(0,0,0,.1);
  background:#fff; color:#334e73;
  display:grid; place-items:center;
  box-shadow: 0 10px 24px rgba(0,0,0,.1);
  cursor:pointer;
  transition: transform .2s ease, background .2s ease;
  z-index: 5;
}
.tc__nav:hover{ transform: translateY(-50%) scale(1.05); background:#f9fbff; }
.tc__nav--prev{ left: -6px; }
.tc__nav--next{ right: -6px; }

/* Dots */
.tc__dots{ display:flex; gap:8px; justify-content:center; margin-top: 12px; }
.tc__dot{
  width:7px; height:7px; border-radius:50%;
  background:#9db3d4; border:none; cursor:pointer;
}
.tc__dot.active{
  background: var(--primary);
  box-shadow: 0 0 0 4px rgba(45,167,255,.18);
}

/* Responsiveness */
@media (max-width: 980px){
  .card{ width: 320px; }
}
@media (max-width: 720px){
  .tc__stage{ height: 360px; }
  .card{ width: 92vw; max-width: 420px; }
}
</style>
