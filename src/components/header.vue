<template>
  <header :class="['site-nav', { 'is-scrolled': scrolled }]">
    <div class="nav-inner">
      <!-- Brand -->
      <a class="brand" href="#home" @click.prevent="go('home')">
        <!-- <span class="logo-dot"></span> -->
        MyProFunnels
      </a>

      <!-- Mobile toggle -->
      <button class="nav-toggle" @click="open = !open" :aria-expanded="open.toString()" aria-label="Toggle menu">
        <span></span><span></span><span></span>
      </button>

      <!-- Links -->
      <nav :class="['links', { open }]">
        <a
          v-for="item in items"
          :key="item.id"
          href="#"
          :class="{ active: active === item.id }"
          @click.prevent="go(item.id)"
        >
          {{ item.label }}
        </a>
      </nav>
    </div>
  </header>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'

const items = [
  { id: 'home',     label: 'Home' },
  { id: 'solution', label: 'Solution' },
  { id: 'bonuses',  label: 'Bonuses' },
  { id: 'coach',    label: 'Coach' },
]

const open = ref(false)
const active = ref('home')
const scrolled = ref(false)
const HEADER_HEIGHT = 68

function go(id) {
  open.value = false
  active.value = id
  const el = document.getElementById(id)
  if (!el) return
  const y = el.getBoundingClientRect().top + window.pageYOffset - HEADER_HEIGHT - 6
  window.scrollTo({ top: y, behavior: 'smooth' })
}

function onScroll() {
  scrolled.value = window.scrollY > 8
  // simple scroll-spy
  let current = 'home'
  for (const it of items) {
    const sec = document.getElementById(it.id)
    if (!sec) continue
    const offsetTop = sec.offsetTop - HEADER_HEIGHT - 20
    if (window.scrollY >= offsetTop) current = it.id
  }
  active.value = current
}

onMounted(() => {
  window.addEventListener('scroll', onScroll, { passive: true })
  // ensure anchors stop below sticky header
  items.forEach(it => {
    const sec = document.getElementById(it.id)
    if (sec) sec.style.scrollMarginTop = HEADER_HEIGHT + 12 + 'px'
  })
  onScroll()
})
onBeforeUnmount(() => window.removeEventListener('scroll', onScroll))
</script>

<style scoped>
.site-nav{
  position: sticky;
  top: 0;
  z-index: 1000;
  backdrop-filter: blur(10px);
  background: linear-gradient(to right, #000000, #24248f, #4b0082);
  border-bottom: 1px solid rgba(255,255,255,.12);
  transition: box-shadow .25s ease, background .25s ease;
}
.site-nav.is-scrolled{
  box-shadow: 0 10px 24px rgba(0,0,0,.24);
  background: linear-gradient(180deg, rgba(6,17,45,.85), rgba(6,17,45,.70));
}

.nav-inner{
  max-width: 1200px;
  margin: 0 auto;
  padding: 14px 5%;
  display: flex;
  align-items: center;
  justify-content: space-between;
    background: linear-gradient(to right, #000000, #24248f, #4b0082);

}

.brand{
  display: flex; align-items: center; gap: .6rem;
  color: #fff; font-weight: 900; text-decoration: none; letter-spacing: .3px;
}
.logo-dot{
  width: 12px; height: 12px; border-radius: 50%;
  background: linear-gradient(135deg, #19c37d, #00a7ff);
  box-shadow: 0 0 0 3px rgba(0,167,255,.15);
}

.links{ display: flex; gap: 24px; align-items: center; }
.links a{
  position: relative;
  color: #cfe5ff; text-decoration: none;
  font-weight: 700; font-size: 14.5px;
  padding: 8px 2px;
  transition: color .2s ease;
}
.links a:hover{ color: #fff; }
.links a.active{ color:#fff; }
.links a.active::after,
.links a:hover::after{
  content: '';
  position: absolute; left: 0; right: 0; bottom: 0;
  height: 3px; border-radius: 2px;
  background: linear-gradient(90deg, #19c37d, #00a7ff);
}

/* mobile */
.nav-toggle{ display:none; background:none; border:none; cursor:pointer; margin-left:auto; }
.nav-toggle span{
  display:block; width:24px; height:2px; background:#e8f2ff; margin:5px 0;
}

@media (max-width: 860px){
  .nav-toggle{ display:block; }
  .links{
    position: fixed;
    top: 64px; right: 12px; left: 12px;
    background: rgba(8,22,56,.96);
    border: 1px solid rgba(255,255,255,.12);
    border-radius: 14px;
    padding: 14px;
    display: grid;
    gap: 6px;
    transform: scale(.98);
    opacity: 0;
    pointer-events: none;
    transition: opacity .2s ease, transform .2s ease;
  }
  .links.open{
    opacity: 1;
    transform: scale(1);
    pointer-events: auto;
  }
  .links a{ padding: 12px 8px; }
}
</style>
