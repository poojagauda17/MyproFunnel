<template id="home">
  <div class="banner-container">
    <!-- Left Side Content -->
    <div class="banner-left-container">
      <h1 class="banner-main-heading">
        <span class="highlight">Attention:</span> Coaches and Course Creators
      </h1>
      <p class="highlight-heading">
        An All-in-One Digital Marketing & Automation Tool with 
        <span class="highlight">Chatbot & IVR</span> For Your Coaching Business.
      </p>
       <p class="highlight-heading">
        Launch Your Course within <span class="highlight">30 Minutes</span> 
       </p>


      <!-- Call To Action Button -->
      <div class="call-action-btn">
        <div class="call-action-text">🚀 Book A Free One-On-One Call Now!</div>
        <div class="call-action-price"> FOR FREE VALUE ₹1999/-</div>
      </div>
    </div>

    <!-- Right Side Image -->
    <div class="banner-right-container">
      <img src="@/assets/banner-logo.png" alt="Banner Image" >
    </div>
  </div>
  
</template>

<script setup lang="ts">
// logic if needed
</script>

<style scoped>
/* Banner Container */
.banner-container {
  background: linear-gradient(to right, #000000, #24248f, #4b0082);
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 5% 5%;
  gap: 40px;
}

/* Left Content */
.banner-left-container {
  flex: 1;
  max-width: 600px;
  color: #fff;
}

.banner-main-heading {
  font-size: 48px;
  font-weight: 800;
  line-height: 1.3;
  margin-bottom: 20px;
}

.banner-main-heading .highlight {
  color: #ffcc00;
}
.highlight{
    color: #ffcc00; 
}

.highlight-heading {
  font-size: 24px;
  line-height: 1.6;
  margin-bottom: 30px;
}

/* Call to Action */
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

/* Right Image */
.banner-right-container {
  flex: 1;
  display: flex;
  justify-content: center;
}

.banner-right-container img {
  max-width: 90%;
  height: auto;
  animation: float 3s ease-in-out infinite;
}

/* Floating Animation */
@keyframes float {
  0% { transform: translateY(0px); }
  50% { transform: translateY(-10px); }
  100% { transform: translateY(0px); }
}

/* Responsive */
@media (max-width: 992px) {
  .banner-container {
    flex-direction: column;
    text-align: center;
    height: auto;
    padding: 60px 20px;
  }

  .banner-right-container {
    margin-top: 30px;
  }

  .banner-main-heading {
    font-size: 36px;
  }

  .highlight-heading {
    font-size: 20px;
  }

  .call-action-btn {
    font-size: 18px;
    padding: 15px 22px;
  }
}
</style>
