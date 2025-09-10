<template >
  <section class="bonuses-unique" id="bonuses">
    <h2 class="bonuses-title">₹ UNLIMITED BONUSES TOO</h2>

    <div class="bonus-grid">
      <article class="bonus-ticket" v-for="(b, i) in bonuses" :key="i">
        <!-- colored stub -->
        <span class="stub"></span>

        <!-- letter coin -->
        <div class="ticket-icon">{{ b.icon }}</div>

        <!-- content -->
        <div class="ticket-content">
          <h3 class="ticket-title">{{ b.title }}</h3>
          <div class="ticket-sub">Included with your plan</div>
        </div>

        <!-- price stamp -->
        <div class="price-stamp">₹ {{ b.price }}/-</div>

        <!-- shimmer -->
        <span class="shine"></span>
       
      </article>
    </div>
    <div class="cta-action">
       <div class="call-action-btn">
        <div class="call-action-text">🚀 Book A Free One-On-One Call Now!</div>
        <div class="call-action-price"> FOR FREE VALUE ₹1999/-</div>
      </div>
    </div>
  </section>
</template>

<script setup>
const bonuses = [
  { icon: 'F', title: 'Fb / Insta Progressive Ads Manager', price: '25,000' },
  { icon: 'G', title: 'Google My Business Page Manager', price: '3,000' },
  { icon: 'Y', title: 'YouTube / Fb / Insta Content Strategy', price: '15,000' },
  { icon: '2', title: '2025 Business Pro Plan Calendar', price: '15,000' },
  { icon: 'A', title: 'Android / iOS App to Manage', price: '35,000' },
  { icon: 'S', title: 'SSL Authentication For Free', price: '599' },
  { icon: 'S', title: 'Social Media Platforms Optimization', price: '3,000' },
  { icon: 'A', title: 'Affiliate Marketing Tool', price: '1,000' },
  { icon: 'S', title: 'SEO Support', price: '5,000' },
  { icon: 'C', title: 'Community Channel Facility', price: '3,000' },
  { icon: 'S', title: 'Sales Pitch Guidance', price: '25,000' },
  { icon: 'D', title: 'DONE FOR YOU SERVICES', price: '25,000' }
]
</script>

<style scoped>
:root{
  --ink:#0f2438;
  --muted:#5d6a79;
  --section:#0b1e3a;           /* section background */
  --ticket:#ffffff;
  --ring:rgba(12,59,120,.14);
}

/* section bg */
.bonuses-unique{
  padding: 64px 5% 90px;
  background:
    radial-gradient(1200px 600px at 12% -20%, rgba(25,195,125,.16), transparent 60%),
    linear-gradient(180deg, #071a33, #0a2142 60%, #0b1e3a);
}

.bonuses-title{
  text-align:center;
  color:#eaf3ff;
  font-weight:900;
  letter-spacing:.5px;
  font-size: clamp(22px, 3.2vw, 30px);
  margin:0 0 18px;
}
.bonuses-title::after{
  content:"";
  width:90px; height:4px; display:block; margin:10px auto 0;
  border-radius:3px;
  background: linear-gradient(90deg, #19c37d, #00a7ff);
}

/* grid */
.bonus-grid{
  display:grid; gap:18px;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
}

/* ticket card */
.bonus-ticket{
  position:relative;
  display:flex; align-items:center;
  background: #fff;
  border-radius: 16px;
  overflow:hidden;
  min-height: 106px;
  box-shadow: 0 14px 26px rgba(0,0,0,.18);
  border: 1px solid rgba(0,0,0,.06);
  transition: transform .25s ease, box-shadow .25s ease, border-color .25s ease;
}
.bonus-ticket:hover{
  transform: translateY(-6px);
  box-shadow: 0 22px 46px rgba(0,0,0,.28);
  border-color: var(--ring);
}

/* colored stub on left */
.stub{
  position:absolute; left:0; top:0; bottom:0; width:92px;
  background: linear-gradient(180deg, #19c37d, #00a7ff);
}
.bonus-ticket:nth-child(4n+2) .stub{ background: linear-gradient(180deg, #ff7a59, #ffb84d); }
.bonus-ticket:nth-child(4n+3) .stub{ background: linear-gradient(180deg, #8b5cf6, #22d3ee); }
.bonus-ticket:nth-child(4n+4) .stub{ background: linear-gradient(180deg, #f7c948, #19c37d); }

/* letter coin */
.ticket-icon{
  position:absolute; left:18px;
  width:56px; height:56px; border-radius:14px;
  display:grid; place-items:center;
  font-weight:900; font-size:18px; letter-spacing:.4px; color:#0b2c8c;
  background:
    radial-gradient(60% 60% at 30% 30%, rgba(255,255,255,.6), transparent 70%),
    linear-gradient(135deg, #f0f6ff, #ffffff 70%);
  box-shadow: inset 0 0 0 1px rgba(12,59,120,.18), 0 8px 16px rgba(0,0,0,.12);
  transition: transform .25s ease;
}
.bonus-ticket:hover .ticket-icon{ transform: scale(1.06); }

/* content area */
.ticket-content{
  padding: 16px 18px 16px 120px; /* make room for stub + icon */
  display:flex; flex-direction:column; gap:6px;
}
.ticket-title{
  color: var(--ink); margin:0;
  font-weight:900; font-size: 16px; line-height:1.25;
}
.ticket-sub{
  color: var(--muted); font-size: 13.5px;
}

/* rotated price stamp */
.price-stamp{
  position:absolute; top:12px; right:12px;
  transform: rotate(-8deg);
  background:#fff8d6; color:#1f2937;
  font-weight:900; font-size: 13px;
  padding: 6px 10px; border-radius:8px;
  border: 1px dashed #f59e0b;
  box-shadow: 0 8px 18px rgba(0,0,0,.12);
}

/* shimmer sweep */
.shine{
  pointer-events:none;
  position:absolute; left:-40%; top:0; width:40%; height:100%;
  background: linear-gradient(110deg, transparent 0%, rgba(255,255,255,.45) 45%, transparent 60%);
  transform: skewX(-20deg);
  transition: left .7s ease;
}
.bonus-ticket:hover .shine{ left:120%; }

/* responsive tweaks */
@media (max-width: 640px){
  .ticket-content{ padding: 16px 14px 16px 110px; }
  .ticket-title{ font-size:15px; }
}
.call-action-btn {
  background: #ffcc00;
  color: #000;
  border-radius: 30px;
  padding: 18px 28px;
  display: inline-block;
  text-align: center;
  font-size: 20px;
  font-weight: bold;
  cursor: pointer;
  box-shadow: 0 4px 20px rgba(0,0,0,0.2);
  transition: all 0.3s ease-in-out;
}
.cta-action{
  text-align: center;
  margin-top: 3%;
}
.call-action-btn:hover {
  background: #ffaa00;
  transform: scale(1.05);
}

.call-action-price {
  font-size: 16px;
  margin-top: 5px;
  font-weight: 500;
  color: #333;
}

</style>
