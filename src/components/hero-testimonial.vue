<template >
  <section class="coach-unique" id="coach" >
    <!-- angled background band -->
    <div class="coach-band"></div>

    <div class="coach-shell">
      <!-- Left: Squircle portrait with layered halo -->
      <div class="portrait-stack">
        <div class="squircle-wrap">
          <span class="outer-ring"></span>
          <span class="inner-ring"></span>
          <img src="@/assets/neeraj.webp" alt="Coach" class="squircle-photo" />
          <span class="photo-glow"></span>
        </div>

        <!-- optional badge; keep or remove -->
        <div class="badge-chip">LIVE • 1-on-1</div>
      </div>

      <!-- Right: Quote glass card -->
      <article class="quote-glass">
        <span class="rail"></span>
        <div class="quote-icon">“</div>

        <h2 class="quote-title">The Coach’s Words</h2>

        <p class="quote-copy">
          I’ll <mark class="hl-alt">not show</mark> you, but will
          <mark class="hl">do with you</mark>
          to launch your course in the live webinar / one-on-one Zoom call itself.
        </p>

        <footer class="quote-sign">
          <div class="sign-name">Mr. Neeraj Shrivastava</div>
          <div class="sign-role">FOUNDER — MyProFunnels Ventures Private Limited</div>
          <span class="sign-underline"></span>
        </footer>
      </article>
    </div>
  </section>
</template>

<style scoped>
:root{
  --navy:#0b2c8c;
  --ink:#0f2438;
  --muted:#5e6a78;
  --accent:#19c37d;
  --gold:#f7c948;
  --sky:#e9f3ff;
}

/* ===== Section scaffold ===== */
.coach-unique{
  position:relative;
  padding: 90px 0 110px;   /* roomy */
  overflow:hidden;
  background: #f7fbff;
}

/* angled band behind content */
.coach-band{
  position:absolute; inset:0;
  background: linear-gradient(135deg,#00164a 0%, #06307a 55%, #0b2c8c 100%);
  clip-path: polygon(0 0, 100% 0, 100% 46%, 0 65%);
  opacity:.95;
}

/* content */
.coach-shell{
  position:relative;
  max-width: 1180px;
  margin: 0 auto;
  padding: 0 5%;
  display:grid;
  grid-template-columns: 440px 1fr;
  gap: 36px;
  align-items:center;
}

/* ===== Portrait stack: modern “squircle” with rings ===== */
.portrait-stack{ position:relative; display:flex; align-items:center; justify-content:center; }

.squircle-wrap{
  position:relative;
  width: 340px; height: 340px;
  border-radius: 32% / 35%;       /* squircle */
  overflow:hidden;
  translate: 0 22px;              /* overlap the angled band */
  box-shadow: 0 24px 60px rgba(0,0,0,.25);
}

.squircle-photo{
  width:100%; height:100%; object-fit:cover; display:block;
  filter: saturate(1.02) contrast(1.02);
}

/* double rings */
.outer-ring, .inner-ring{
  position:absolute; inset:-10px; border-radius: 32% / 35%;
  content:"";
  pointer-events:none;
}
.outer-ring{
  background:
    conic-gradient(from 0deg, var(--gold), #ffffff 22%, var(--accent) 55%, #7eb6ff 88%, var(--gold) 100%);
  mix-blend-mode: normal;
  z-index:-2;
  filter: blur(0.4px);
}
.inner-ring{
  inset:-4px;
  border: 6px solid #ffffff;
  z-index:1;
  box-shadow: inset 0 0 0 1px rgba(0,0,0,.05);
}

/* soft ambient glow */
.photo-glow{
  position:absolute; inset: -28px;
  border-radius: 32% / 35%;
  background: radial-gradient(40% 45% at 30% 25%, rgba(25,195,125,.25), transparent 60%),
              radial-gradient(45% 42% at 70% 75%, rgba(247,201,72,.22), transparent 60%);
  z-index:-3;
  filter: blur(10px);
}

/* tiny badge */
.badge-chip{
  position:absolute; bottom:-10px; right:18px;
  background:#111827; color:#fff; font-weight:800; letter-spacing:.2px;
  font-size:12px; padding:6px 10px; border-radius:999px;
  box-shadow: 0 10px 20px rgba(0,0,0,.25);
  border:1px solid rgba(255,255,255,.12);
}

/* ===== Quote glass card ===== */
.quote-glass{
  position:relative;
  background: rgba(255,255,255,.9);
  backdrop-filter: blur(8px);
  border-radius: 22px;
  padding: 28px 28px 24px 34px;
  box-shadow: 0 18px 42px rgba(0,0,0,.18);
  border: 1px solid rgba(11,44,140,.14);
}

/* vertical accent rail */
.rail{
  position:absolute; left:0; top:0; bottom:0; width:8px;
  background: linear-gradient(180deg, var(--accent), #00a7ff);
  border-top-left-radius:22px; border-bottom-left-radius:22px;
}

/* large decorative quote */
.quote-icon{
  position:absolute; top:-22px; left:18px;
  font-size:72px; line-height:1; font-weight:900;
  color: rgba(255,255,255,.85);
  text-shadow: 0 3px 14px rgba(11,44,140,.35);
}

/* title (kept small so focus is on copy) */
.quote-title{
  margin: 0 0 10px;
  font-weight:900; letter-spacing:.3px;
  font-size: clamp(18px,2.6vw,22px);
  color: var(--navy);
}

/* highlighted copy */
.quote-copy{
  color: var(--ink);
  font-size: clamp(15.5px,2.1vw,18px);
  line-height:1.65;
  margin: 0 0 18px;
}
.hl{
  background: linear-gradient(90deg, rgba(25,195,125,.22), rgba(25,195,125,0));
  padding: 0 .25em; border-radius: 6px; font-weight:900; color: var(--navy);
}
.hl-alt{
  background: linear-gradient(90deg, rgba(247,201,72,.28), rgba(247,201,72,0));
  padding: 0 .25em; border-radius: 6px; font-weight:900; color:#1b2a4c;
}

/* signature ribbon */
.quote-sign{ position:relative; padding-top:10px; }
.sign-name{ font-weight:900; color: var(--ink); font-size:16.5px; }
.sign-role{ color: var(--muted); font-size:13.5px; margin-top:2px; }
.sign-underline{
  position:absolute; left:0; bottom:-6px; height:4px; width:140px; border-radius:2px;
  background: linear-gradient(90deg, var(--navy), transparent);
}

/* ===== Responsive ===== */
@media (max-width: 980px){
  .coach-shell{ grid-template-columns: 1fr; gap: 22px; }
  .portrait-stack{ order: 1; }
  .quote-glass{ order: 2; }
  .squircle-wrap{ width: 300px; height: 300px; translate: 0 12px; }
}
@media (max-width: 520px){
  .squircle-wrap{ width: 260px; height: 260px; }
  .badge-chip{ right: 6px; }
}
</style>
