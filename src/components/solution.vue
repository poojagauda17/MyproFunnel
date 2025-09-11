<template>
  <section class="unique-solution" id="solution">
    <h2 class="simplest-solution-heading">
      Providing The Simplest Solution For The Most Complex Problem
    </h2>
    <div class="simplest-solution-subheading">
      By Providing Everything <span class="accent">UNLIMITED</span>
    </div>

    <!-- FILTER CHIPS -->
    <div class="chips">
      <button class="chip" :class="{ active: active === 'all' }" @click="active = 'all'">All</button>
      <button v-for="c in cats" :key="c" class="chip" :class="{ active: active === c }" @click="active = c">
        {{ c }}
      </button>
    </div>

    <!-- GRID with spotlight -->
    <div class="solution-section fancy-grid" @pointermove="onMove" @mouseleave="resetMove">
      <article v-for="f in filtered" :key="f.title" class="problem-solving-containers fancy-card">
        <span class="ribbon">FREE</span>

        <div class="solution-img">
          <img :src="f.img" :alt="f.title" @error="onImgError(f)" />
        </div>

        <div class="solution-heading">{{ f.title }}</div>

        <div class="solution-pricing">
          <span class="text-through">₹ {{ f.mrp }} / Month</span>
          <!-- <span class="free-pill">FREE</span> -->
        </div>

        <p class="hover-desc">{{ f.desc }}</p>
        <span class="shine"></span>
      </article>
    </div>

    <!-- ✨ ADDED: Animated price ribbon -->
    <div class="price-ribbon" ref="priceRibbonRef" aria-label="Price ribbon">
      <div class="price-ribbon__inner">
        <span class="price-ribbon__rupee">₹</span>
        <span class="price-ribbon__amount">{{ priceFormatted }}</span>
        <span class="price-ribbon__suffix">
          /- PER MONTH, IF YOU PURCHASE THESE WORLD CLASS TOOLS.
        </span>
      </div>
      <span class="price-ribbon__shine" aria-hidden="true"></span>
    </div>
    <!-- ✨ /ADDED -->

    <div class="cta-action">
      <div class="call-action-btn">
        <div class="call-action-text">🚀 Book A Free One-On-One Call Now!</div>
        <div class="call-action-price"> FOR FREE VALUE ₹1999/-</div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, computed, onMounted, onBeforeUnmount } from 'vue'

const cats = ['Build', 'Automate', 'Engage', 'Manage']
const active = ref('all')

/* ✅ USE PUBLIC PATHS (works in dev + build even under subpath) */
const BASE = import.meta.env.BASE_URL || '/' // e.g. '/' or '/your-subdir/'

const features = [
  { title: 'Unlimited Landing Pages',     mrp: '5000', img: `http://localhost:5173/src/assets/solution/landing-page.png`, tag: 'Build',
    desc:'Har campaign ke liye high-converting landing pages with tracking & A/B testing.' },
  { title: 'Unlimited Website Pages',     mrp: '5000', img: `http://localhost:5173/src/assets/solution/domain.png`,       tag: 'Build',
    desc:'Multiple branded sites/pages—speed, SEO & security optimizations baked-in.' },
  { title: 'Unlimited Emails',            mrp: '3000', img: `http://localhost:5173/src/assets/solution/letter.png`,       tag: 'Engage',
    desc:'Broadcasts, drips & automations—no caps. Real-time analytics included.' },
  { title: 'Unlimited WhatsApp Messages', mrp: '2500', img: `http://localhost:5173/src/assets/solution/whatsapp.png`,     tag: 'Engage',
    desc:'WhatsApp broadcasts, reminders & journeys that drive quick replies.' },
  { title: 'Unlimited Automations',       mrp: '5000', img: `http://localhost:5173/src/assets/solution/automation.png`,   tag: 'Automate',
    desc:'Drag-and-drop flows—lead capture se onboarding tak sab auto-pilot pe.' },
  { title: 'Unlimited Calendar Set up',   mrp: '3000', img: `http://localhost:5173/src/assets/solution/time.png`,         tag: 'Manage',
    desc:'Book, reschedule, reminders—Google Calendar & Zoom integration.' },
  { title: 'Unlimited Contact Forms',     mrp: '3000', img: `http://localhost:5173/src/assets/solution/contact-form.png`, tag: 'Build',
    desc:'Custom forms, validations & routing—no more generic Google Forms.' },
  { title: 'Unlimited Contacts Storing',  mrp: '2000', img: `http://localhost:5173/src/assets/solution/book.png`,         tag: 'Manage',
    desc:'Enriched profiles, segments & tags—perfect for targeted campaigns.' },
  { title: 'Unlimited Surveys',           mrp: '2000', img: `http://localhost:5173/src/assets/solution/survey.png`,       tag: 'Manage',
    desc:'Enriched profiles, segments & tags—perfect for targeted campaigns.' },
  { title: 'Unlimited LMS',               mrp: '2000', img: `http://localhost:5173/src/assets/solution/dashboard.png`,    tag: 'Manage',
    desc:'Enriched profiles, segments & tags—perfect for targeted campaigns.' },
  { title: 'Unlimited Hosting Space',     mrp: '2000', img: `http://localhost:5173/src/assets/solution/disk-usage.png`,   tag: 'Manage',
    desc:'Enriched profiles, segments & tags—perfect for targeted campaigns.' },
  { title: 'Unlimited Payments (only 2% charges)', mrp: '2000', img: `http://localhost:5173/src/assets/solution/payment-method.png`, tag: 'Manage',
    desc:'Enriched profiles, segments & tags—perfect for targeted campaigns.' },
  { title: 'Unlimited Payments Pages',    mrp: '2000', img: `http://localhost:5173/src/assets/solution/donation.png`,     tag: 'Manage',
    desc:'Enriched profiles, segments & tags—perfect for targeted campaigns.' },
  { title: 'Unlimited Zoom Webinars / Meetings (500 People)', mrp: '2000', img: `http://localhost:5173/src/assets/solution/zoom.png`, tag: 'Manage',
    desc:'Enriched profiles, segments & tags—perfect for targeted campaigns.' },
  { title: 'Unlimited Staff Adding Facility', mrp: '2000', img: `http://localhost:5173/src/assets/solution/add.png`,      tag: 'Manage',
    desc:'Enriched profiles, segments & tags—perfect for targeted campaigns.' },
  { title: 'Unlimited Mobile / Web Push', mrp: '2000', img: `http://localhost:5173/src/assets/solution/notification.png`, tag: 'Manage',
    desc:'Enriched profiles, segments & tags—perfect for targeted campaigns.' },
  { title: 'Unlimited Live Supports',     mrp: '2000', img: `http://localhost:5173/src/assets/solution/live-chat.png`,    tag: 'Manage',
    desc:'Enriched profiles, segments & tags—perfect for targeted campaigns.' },
  { title: 'Unlimited Happiness!!!',      mrp: '2000', img: `http://localhost:5173/src/assets/solution/happy.png`,        tag: 'Manage',
    desc:'Enriched profiles, segments & tags—perfect for targeted campaigns.' },
]

const filtered = computed(() => (active.value === 'all' ? features : features.filter(f => f.tag === active.value)))

function onMove(e) {
  const el = e.currentTarget
  const r = el.getBoundingClientRect()
  const x = ((e.clientX - r.left) / r.width) * 100
  const y = ((e.clientY - r.top) / r.height) * 100
  el.style.setProperty('--mx', x + '%')
  el.style.setProperty('--my', y + '%')
}
function resetMove(e) {
  const el = e.currentTarget
  el.style.removeProperty('--mx')
  el.style.removeProperty('--my')
}

/* Helpful debug: logs broken image URL in console (remove later) */
function onImgError(f) {
  // eslint-disable-next-line no-console
  console.warn('Image not found:', f.img)
}

/* ---------------------------
   ✨ Price ribbon count-up
---------------------------- */
const priceRibbonRef = ref(null)
const priceCurrent = ref(0)
const PRICE_TARGET = 89500
const priceFormatted = computed(() =>
  priceCurrent.value.toLocaleString('en-IN', { maximumFractionDigits: 0 })
)
let priceStarted = false
let priceRAF = 0
let priceObs

function startPriceCount(duration = 1200) {
  const start = performance.now()
  const from = 0
  const to = PRICE_TARGET
  const ease = (t) => 1 - Math.pow(1 - t, 3) // easeOutCubic

  function tick(now) {
    const p = Math.min(1, (now - start) / duration)
    priceCurrent.value = Math.round(from + (to - from) * ease(p))
    if (p < 1) priceRAF = requestAnimationFrame(tick)
  }
  priceRAF = requestAnimationFrame(tick)
}

onMounted(() => {
  priceObs = new IntersectionObserver((entries) => {
    const entry = entries[0]
    if (entry.isIntersecting && !priceStarted) {
      priceStarted = true
      startPriceCount()
    }
  }, { threshold: 0.4 })
  if (priceRibbonRef.value) priceObs.observe(priceRibbonRef.value)
})

onBeforeUnmount(() => {
  if (priceObs && priceRibbonRef.value) priceObs.unobserve(priceRibbonRef.value)
  cancelAnimationFrame(priceRAF)
})
</script>

<style scoped>
:root { --ink:#0f2438; --muted:#5c6977; --accent:#19c37d; --navy:#0b2c8c; --ring:rgba(12,59,120,.14); }

.unique-solution{
  padding:56px 5% 64px;
  background:
    radial-gradient(800px 420px at 8% -10%, rgba(25,195,125,.12), transparent 60%),
    radial-gradient(700px 400px at 96% -8%, rgba(11,44,140,.08), transparent 55%),
    #f7fbff;
}
.simplest-solution-heading{ text-align:center; color:var(--ink); font-weight:900; font-size:clamp(26px,3.8vw,42px); line-height:1.15; }
.simplest-solution-subheading{ text-align:center; color:var(--muted); margin:8px 0 18px; font-size:clamp(15px,2.2vw,18px); }
.accent{ color:var(--navy); font-weight:800; }

/* chips */
.chips{ display:flex; gap:10px; justify-content:center; flex-wrap:wrap; margin-bottom:18px; }
.chip{ border:1px solid rgba(11,44,140,.18); background:#fff; color:var(--ink); border-radius:999px; padding:8px 14px;
       font-weight:700; font-size:13.5px; cursor:pointer; transition:background .2s, transform .15s, box-shadow .2s; }
.chip:hover{ transform:translateY(-1px); box-shadow:0 8px 18px rgba(0,0,0,.08); }
.chip.active{ background:linear-gradient(90deg, #19c37d, #35d39d);; color:#fff; border-color:transparent; }

/* grid */
.solution-section.fancy-grid{ display:grid; grid-template-columns:repeat(4, minmax(220px,1fr)); gap:18px; --mx:50%; --my:50%; }
@media (max-width:1100px){ .solution-section.fancy-grid{ grid-template-columns:repeat(2, minmax(260px,1fr)); } }
@media (max-width:640px){ .solution-section.fancy-grid{ grid-template-columns:1fr; } }

/* cards */
.fancy-card{
  position:relative; border-radius:16px; padding:18px 18px 14px; text-align:center;
  background:
    radial-gradient(180px 120px at var(--mx) var(--my), rgba(25,195,125,.12), transparent 60%),
    linear-gradient(180deg, #fff 0%, #f6fbff 100%);
  border:1px solid rgba(0,0,0,.06); box-shadow:0 10px 24px rgba(0,0,0,.08);
  overflow:hidden; transition:transform .22s, box-shadow .22s, border-color .22s; min-height:190px;
}
.fancy-card:hover{ transform:translateY(-4px); box-shadow:0 18px 36px rgba(0,0,0,.16); border-color:var(--ring); }

/* ribbon */
.ribbon{
  position:absolute; top:10px; right:-38px; transform:rotate(35deg);
  background:linear-gradient(90deg, var(--accent), #35d39d); color:#35d39d; font-weight:900; font-size:11px; letter-spacing:.5px;
  padding:6px 40px; box-shadow:0 6px 16px rgba(25,195,125,.35);
}

/* icon badge */
.solution-img{
  width:64px; height:64px; margin:0 auto 10px; border-radius:14px; display:grid; place-items:center;
  background:
    radial-gradient(60% 60% at 30% 30%, rgba(25,195,125,.18), transparent 70%),
    linear-gradient(135deg, #f0f6ff 0%, #ffffff 70%);
  box-shadow: inset 0 0 0 1px rgba(12,59,120,.1);
}
.solution-img img{ width:34px; height:34px; object-fit:contain; display:block; }

/* title + pricing */
.solution-heading{ font-weight:800; color:var(--ink); font-size:17px; margin-bottom:4px; }
.solution-pricing{ display:flex; gap:10px; justify-content:center; align-items:center; margin-bottom:6px; padding-top: 5px;}
.text-through{ text-decoration:line-through; color: #5c6977; font-weight:700; font-size:13.5px; }
.free-pill{ background:var(--accent); color:#fff; font-weight:900; padding:4px 10px; border-radius:999px; font-size:12px; letter-spacing:.3px; }

/* hover desc */
.hover-desc{ color:var(--muted); font-size:13.8px; line-height:1.45; max-height:0; opacity:0; overflow:hidden;
             transition:max-height .32s ease, opacity .22s ease, margin-top .32s ease; }
.fancy-card:hover .hover-desc{ max-height:90px; opacity:1; margin-top:8px; }

/* shine sweep */
.shine{ position:absolute; top:0; left:-40%; width:40%; height:100%; transform:skewX(-20deg);
        background:linear-gradient(110deg, transparent 0%, rgba(255,255,255,.5) 45%, transparent 60%);
        transition:left .6s ease; pointer-events:none; }
.fancy-card:hover .shine{ left:120%; }

.cta-action{ text-align: center; margin-top: 3%; }
.call-action-btn{ background:#ffcc00; color:#000; border-radius:30px; padding:18px 28px; display:inline-block; text-align:center;
  font-size:20px; font-weight:bold; cursor:pointer; box-shadow:0 4px 20px rgba(0,0,0,0.2); transition:all .3s ease-in-out; }
.call-action-btn:hover{ background:#ffaa00; transform:scale(1.05); }
.call-action-price{ font-size:16px; margin-top:5px; font-weight:500; color:#333; }

/* ✨ Price ribbon styles */
.price-ribbon{
  position:relative;
  max-width: 1180px;
  margin: 18px auto 18px;
  border-radius: 16px;
  background: linear-gradient(90deg, #0017c9, #022f82, #0017c9);
  background-size: 220% 100%;
  animation: pr-bg-pan 9s linear infinite;
  box-shadow: 0 16px 32px rgba(0,0,0,.18), 0 0 0 1px rgba(255,255,255,.06) inset;
  overflow:hidden;
}
.price-ribbon::before{
  content:"";
  position:absolute; inset:0; border-radius:16px;
  box-shadow: 0 0 0 2px rgba(255,255,255,.08) inset, 0 0 40px rgba(0,60,255,.30) inset;
  pointer-events:none;
}
.price-ribbon__inner{
  padding: 16px 22px;
  text-align:center; color:#fff; font-weight:900; letter-spacing:.4px; text-transform:uppercase;
  position:relative; z-index:2;
}
.price-ribbon__rupee{ font-size:clamp(16px,2.2vw,18px); margin-right:2px; }
.price-ribbon__amount{ font-size:clamp(18px,2.6vw,20px); }
.price-ribbon__suffix{ font-size:clamp(13px,2.0vw,14px); opacity:.95; margin-left:.35rem; }
.price-ribbon__shine{
  position:absolute; top:0; bottom:0; left:-35%;
  width:35%; transform:skewX(-20deg);
  background: linear-gradient(110deg, transparent 0%, rgba(255,255,255,.45) 45%, transparent 60%);
  animation: pr-sweep 3.2s ease-in-out infinite; z-index:1; pointer-events:none;
}
@keyframes pr-bg-pan{
  0%{ background-position:0% 0%; } 50%{ background-position:100% 0%; } 100%{ background-position:0% 0%; }
}
@keyframes pr-sweep{
  0%{ left:-40%; opacity:0; } 15%{ opacity:.9; } 50%{ left:110%; opacity:0; } 100%{ left:110%; opacity:0; }
}
</style>
