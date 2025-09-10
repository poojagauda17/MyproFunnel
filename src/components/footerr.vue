<template>
  <footer class="site-footer">
    <!-- wave divider -->
    <svg class="footer-wave" viewBox="0 0 1440 110" preserveAspectRatio="none" aria-hidden="true">
      <path d="M0,64 C180,120 360,120 540,96 C720,72 900,16 1080,24 C1260,32 1350,64 1440,80 L1440,110 L0,110 Z" fill="#062761"/>
    </svg>

    <div class="footer-wrap">
      <!-- top grid -->
      <div class="footer-grid">
        <!-- Brand / About -->
        <div class="col">
          <div class="brand">
            <img class="brand-logo" src="@/assets/logo.webp" alt="MyProFunnels" />
            <div class="brand-name">MyProFunnels</div>
          </div>
          <p class="brand-copy">
            All-in-one digital marketing & automation built for coaches and course creators.
            Launch faster, scale smarter.
          </p>

          <div class="socials">
            <a href="#" aria-label="LinkedIn" class="sbtn" title="LinkedIn">
              <svg viewBox="0 0 24 24" width="18" height="18" aria-hidden="true">
                <path d="M4.98 3.5C4.98 4.88 3.86 6 2.5 6S0 4.88 0 3.5 1.12 1 2.5 1s2.48 1.12 2.48 2.5zM.5 8h4V23h-4V8zm7.5 0h3.8v2.05h.05c.53-1 1.83-2.05 3.77-2.05C19.9 8 22 10.06 22 13.77V23h-4v-8.13c0-1.94-.69-3.27-2.41-3.27-1.32 0-2.11.89-2.46 1.75-.13.31-.16.75-.16 1.19V23h-4V8z" fill="currentColor"/>
              </svg>
            </a>
            <a href="#" aria-label="YouTube" class="sbtn" title="YouTube">
              <svg viewBox="0 0 24 24" width="18" height="18" aria-hidden="true">
                <path d="M23.5 6.2a3 3 0 0 0-2.1-2.1C19.5 3.6 12 3.6 12 3.6s-7.5 0-9.4.5A3 3 0 0 0 .5 6.2C0 8.1 0 12 0 12s0 3.9.5 5.8a3 3 0 0 0 2.1 2.1c1.9.5 9.4.5 9.4.5s7.5 0 9.4-.5a3 3 0 0 0 2.1-2.1C24 15.9 24 12 24 12s0-3.9-.5-5.8zM9.6 15.6V8.4L15.8 12l-6.2 3.6z" fill="currentColor"/>
              </svg>
            </a>
            <a href="#" aria-label="Twitter/X" class="sbtn" title="Twitter">
              <svg viewBox="0 0 24 24" width="18" height="18" aria-hidden="true">
                <path d="M18.2 2H21l-6.5 7.4L22.8 22H16l-5-6.7L5 22H2l7.2-8.3L1.5 2H8l4.3 5.8L18.2 2zM16 20h1.7L7.9 4H6.1L16 20z" fill="currentColor"/>
              </svg>
            </a>
          </div>
        </div>

        <!-- Important Links -->
        <div class="col">
          <h4 class="col-title">Important links</h4>
          <ul class="list">
            <li><a href="#">Terms & Conditions</a></li>
            <li><a href="#">Privacy Policy</a></li>
            <li><a href="#">Cancellation & Refund</a></li>
            <li><a href="#">Contact us</a></li>
          </ul>
        </div>

        <!-- Resources -->
        <div class="col">
          <h4 class="col-title">Resources</h4>
          <ul class="list">
            <li><a href="#">Free Webinar</a></li>
            <li><a href="#">Success Stories</a></li>
            <li><a href="#">Pricing & Plans</a></li>
            <li><a href="#">Help Center</a></li>
          </ul>
        </div>

        <!-- Contact -->
        <div class="col">
          <h4 class="col-title">Get in touch</h4>
          <ul class="contact">
            <li><span class="c-badge">E</span> support@myprofunnels.com</li>
            <li><span class="c-badge">P</span> +91 98XX-XXX-XXX</li>
            <li><span class="c-badge">A</span> Mumbai, Maharashtra, IN</li>
          </ul>
          <!-- <a href="#" class="mini-cta">Book a free call</a> -->
             <div class="cta-section">
  <button class="cta-btn">
    🚀 Book A Free Call Now!
  </button>
</div>
        </div>
      </div>

      <!-- Disclaimer card -->
      <div class="disclaimer">
        Please be advised that the content shown on this page is not intended to serve as a guarantee.
        We do not and cannot make guarantees about your ability to get results or earn any money with our ideas,
        information, tools, or strategies. Your results are up to you. We aim to provide great content and strategies
        that worked for us and our clients. All terms, privacy policies, and disclaimers can be accessed on the next page.
      </div>

      <!-- bottom bar -->
      <div class="footbar">
        <div class="copy">© {{ new Date().getFullYear() }} MyProFunnels Dot Com. All rights reserved.</div>
        <div class="links">
          <a href="#">T&C</a>
          <a href="#">Privacy</a>
          <a href="#">Refunds</a>
          <a href="#">Contact</a>
        </div>
      </div>
    </div>
  </footer>
</template>

<style scoped>
:root{
  --bg1:#062761;
  --bg2:#041a49;
  --ink:#eaf3ff;
  --muted:#b6c7e3;
  --accent:#19c37d;
  --gold:#f7c948;
  --white: #fff;
}

/* container */
.site-footer{
  position: relative;
  color: var(--ink);
  background: radial-gradient(1200px 600px at 10% -20%, rgba(25,195,125,.16), transparent 60%),
              linear-gradient(180deg, var(--bg1), var(--bg2));
  overflow: hidden;
}

/* subtle twinkle dots */
.site-footer::before{
  content:"";
  position:absolute; inset:0;
  background-image:
    radial-gradient(2px 2px at 20% 30%, rgba(255,255,255,.18), transparent 60%),
    radial-gradient(2px 2px at 70% 10%, rgba(255,255,255,.16), transparent 60%),
    radial-gradient(2px 2px at 40% 80%, rgba(255,255,255,.12), transparent 60%);
  pointer-events:none;
}

.footer-wave{
  display:block; width:100%; height:110px;
}

/* wrap */
.footer-wrap{
  /* max-width: 1200px; */
  margin: 0 auto;
  padding: 20px 5% 32px;
  background-color: #062761;
}

/* grid */
.footer-grid{
  display:grid;
  grid-template-columns: 1.3fr 1fr 1fr 1fr;
  gap: 28px;
}

@media (max-width: 980px){
  .footer-grid{ grid-template-columns: 1fr 1fr; }
}
@media (max-width: 620px){
  .footer-grid{ grid-template-columns: 1fr; }
}

/* brand */
.brand{
  display:flex; align-items:center; gap:12px; margin-bottom:8px;
}
.brand-logo{ width:40px; height:40px; object-fit:contain;     border-radius: 50%; }
.brand-name{ font-weight:900; letter-spacing:.4px; font-size:20px; }
.brand-copy{ color: var(--white); line-height:1.6; margin: 6px 0 14px; }

/* socials */
.socials{ display:flex; gap:10px; }
.sbtn{
  display:grid; place-items:center; width:34px; height:34px; border-radius:10px;
  background: linear-gradient(135deg, #0e3a85, #0b2c6a);
  color:#dfeaff; border:1px solid rgba(255,255,255,.12);
  box-shadow: 0 8px 18px rgba(0,0,0,.25);
  transition: transform .2s ease, box-shadow .2s ease, color .2s ease;
}
.sbtn:hover{ transform: translateY(-2px); box-shadow: 0 12px 24px rgba(0,0,0,.35); color:var(--gold); }

/* columns */
.col-title{ font-weight:800; margin: 6px 0 10px; }
.list{ list-style:none; padding:0; margin:0; display:grid; gap:8px; }
.list a{ color: #dfeaff; text-decoration:none; }
.list a:hover{ color:var(--gold); text-decoration:underline; }

/* contact */
.contact{ list-style:none; padding:0; margin:0 0 12px; display:grid; gap:8px; color: var(--ink); }
.c-badge{
  display:inline-grid; place-items:center; width:18px; height:18px; border-radius:4px;
  background: rgba(255,255,255,.12); color:#fff; font-size:11px; font-weight:800; margin-right:8px;
}
.mini-cta{
  display:inline-block;
  color:#fff; background:#ffd21e; border-radius:999px; padding:8px 14px; font-weight:800;
  text-decoration:none; box-shadow: 0 10px 20px rgba(0,0,0,.25);
  transition: transform .2s ease, box-shadow .2s ease;
}
.mini-cta:hover{ transform: translateY(-2px); box-shadow: 0 14px 28px rgba(0,0,0,.35); }

/* disclaimer */
.disclaimer{
  margin: 22px 0 18px;
  padding: 14px 16px;
  background: rgba(255,255,255,.08);
  border:1px solid rgba(255,255,255,.15);
  border-radius: 12px;
  color: var(--white);
  line-height: 1.6;
}
div{
    color: white;
}
/* bottom bar */
.footbar{
  display:flex; gap:16px; justify-content:space-between; align-items:center;
  border-top: 1px solid rgba(255,255,255,.12);
  padding-top: 12px;
}
.copy{ color:#cfdaf3; font-size: 14px; }
.links{ display:flex; gap:14px; }
.links a{ color:#fff; text-decoration:none; font-size:14px; }
.links a:hover{ color: var(--gold); text-decoration:underline; }
.cta-section {
  display: flex;
  justify-content: center;
  margin-top: 3%;
}

.cta-btn {
    background: #ffcc00;
    color: #000;
    border: transparent;
    border-radius: 30px;
    padding: 18px 28px;
    display: inline-block;
    text-align: center;
    font-size: 12px;
    cursor: pointer;
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.2);
    transition: all 0.3s 
ease-in-out;
}

.cta-btn:hover {
  transform: translateY(-3px);
  box-shadow: 0 10px 28px rgba(0,0,0,0.25);
}

.cta-btn .cta-sub {
  display: block;
  font-size: 14px;
  font-weight: 500;
  margin-top: 4px;
  color: #333;
}
</style>
