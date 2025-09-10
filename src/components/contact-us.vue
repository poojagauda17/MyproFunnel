<template>
  <section class="sc">
    <div class="sc__wrap">
      <!-- Dark left panel that overlaps the white card -->
      <aside class="panel">
        <h4>Contact Us</h4>

        <ul class="plist">
          <li>
            <span class="pico">📍</span>
            <div class="ptext">45, Avenue de Paris<br />South Park</div>
          </li>
          <li>
            <span class="pico">🔗</span>
            <div class="ptext">https://yourdomain.com</div>
          </li>
          <li>
            <span class="pico">✉️</span>
            <div class="ptext">hello@yourdomain.com</div>
          </li>
          <li>
            <span class="pico">📞</span>
            <div class="ptext">+91 98765 43210</div>
          </li>
        </ul>

        <div class="social">
          <a href="#" aria-label="Facebook" class="sico fb">f</a>
          <a href="#" aria-label="Twitter" class="sico tw">t</a>
          <a href="#" aria-label="Dribbble" class="sico dr">d</a>
        </div>
      </aside>

      <!-- Main white card with the form -->
      <div class="card">
        <form class="form" @submit.prevent="submit">
          <h3 class="ftitle">Get in Touch</h3>
          <p class="fsub">Please fill the form to contact us.</p>

          <input
            v-model.trim="f.name"
            type="text"
            class="in"
            placeholder="Your name"
            required
          />
          <input
            v-model.trim="f.email"
            type="email"
            class="in"
            placeholder="Email"
            required
          />
          <input
            v-model.trim="f.number"
            type="number"
            class="in"
            placeholder="Number"
            required
          />
          <textarea
            v-model.trim="f.msg"
            class="in area"
            placeholder="Your message"
            rows="4"
            required
          ></textarea>

          <button type="submit" class="btn">SEND</button>

          <transition name="toast">
            <div v-if="sent" class="toast">Thanks! We’ll get back to you.</div>
          </transition>
        </form>
      </div>
    </div>
  </section>
</template>

<script setup>
import { reactive, ref } from 'vue'

const f = reactive({ name: '', email: '', msg: '' })
const sent = ref(false)

function submit() {
  if (!f.name || !f.email || !f.msg) return
  sent.value = true
  setTimeout(() => (sent.value = false), 2500)
  f.name = ''
  f.email = ''
  f.msg = ''
}
</script>

<style scoped>
/* ===== Background (soft blue) ===== */
.sc{
  padding: 40px 5% 60px;
  /* background: radial-gradient(1000px 600px at -10% -10%, #bfe3ff 0%, #a6d3ff 30%, #93c6f8 60%, #8cc2f6 100%); */
}

/* ===== Centered wrap ===== */
.sc__wrap{
  max-width: 900px;
  margin: 0 auto;
  position: relative;
}

/* ===== Main white card ===== */
.card{
  background: #ffffff;
  border-radius: 8px;
  box-shadow: 0 24px 60px rgba(20, 40, 70, .18);
  min-height: 380px;
}

/* ===== Form area on the right ===== */
.form{
  padding: 32px 34px 28px 330px;  /* leave space for the overlapping panel */
  position: relative;
}
.ftitle{
  margin: 0;
  color: #1e2b3a;
  font-weight: 900;
  font-size: 22px;
}
.fsub{ margin: 6px 0 16px; color: #7b8a99; }

.in{
  width: 100%;
  background: #f3f7fb;
  border: 1px solid #edf2f7;
  border-radius: 6px;
  height: 25px;
  font-size: 14px;
  padding: 10px 12px;
  color: #223043;
  outline: none;
  margin-bottom: 12px;
}
.in:focus{
  border-color: #bcd8ff;
  box-shadow: 0 0 0 3px rgba(90, 160, 255, .18);
}
.area{ height: auto; resize: vertical; padding-top: 12px; }

/* SEND button (rounded pill) */
.btn{
  display: inline-block;
  min-width: 120px;
  background: #10326f;
  color: #fff;
  border: none;
  border-radius: 22px;
  padding: 10px 18px;
  font-weight: 900;
  letter-spacing: .03em;
  box-shadow: 0 12px 28px rgba(88,160,255,.35);
  cursor: pointer;
}
.btn:hover{ filter: brightness(1.03); transform: translateY(-1px); }

/* success toast */
.toast{
  margin-top: 10px;
  background: #e8f6ff;
  border: 1px solid #cfeaff;
  color: #0b3a63;
  padding: 8px 10px;
  border-radius: 6px;
  font-weight: 800;
}
.toast-enter-from{ opacity: 0; transform: translateY(6px); }
.toast-leave-to  { opacity: 0; transform: translateY(6px); }
.toast-enter-active, .toast-leave-active{ transition: all .2s ease; }

/* ===== Left dark panel (overlaps the card) ===== */
.panel{
  position: absolute;
  left: -22px;
  top: 30px;
  width: 270px;
  height: 352px;
  background: #10326f;
  color: #e9f1f7;
  border-radius: 6px;
  box-shadow: 0 22px 50px rgba(12, 36, 69, .4);
  padding: 18px 16px 12px;
}
.panel h4{
  margin: 2px 0 10px;
  font-size: 18px;
  font-weight: 900;
}

/* contact lines */
.plist{ list-style: none; margin: 10px 0 14px; padding: 0; display: grid; gap: 12px; }
.plist li{ display: grid; grid-template-columns: 22px 1fr; align-items: start; gap: 10px; }
.pico{ width: 22px; text-align: center; filter: saturate(.9) brightness(1.02); }
.ptext{ line-height: 1.35; font-size: 14px; opacity: .95; }

/* social icons row */
.social{ display: flex; gap: 8px; margin-top: 6px; }
.sico{
  width: 28px; height: 28px; display: grid; place-items: center;
  background: rgba(255,255,255,.08);
  color: #dce9f6; text-decoration:none; border-radius: 4px;
  font-weight: 900; text-transform: uppercase; font-size: 13px;
}
.sico:hover{ background: rgba(255,255,255,.16); }

/* ===== Responsive ===== */
@media (max-width: 760px){
  .form{ padding: 220px 18px 22px; }
  .panel{ position: relative; left: 0; top: -18px; width: auto; }
}
</style>
