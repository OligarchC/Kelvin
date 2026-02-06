<template>
  <v-app class="app-shell">
    <div class="ambient">
      <span class="orb orb-a"></span>
      <span class="orb orb-b"></span>
      <span class="orb orb-c"></span>
    </div>

    <v-main class="main">
      <v-container class="content">
        <v-row justify="center">
          <v-col cols="12" md="9" lg="8">
            <v-card class="hero-card" elevation="12">
              <v-alert
                v-if="showAlert"
                class="love-alert"
                type="success"
                variant="tonal"
                border="start"
                closable
                @click:close="showAlert = false"
              >
                Best answer ever. I'm so excited.
              </v-alert>
              <div class="hero-grid">
                <section class="copy">
                  <p class="eyebrow">A night worth a yes</p>
                  <h1 class="title">
                    Will you be my Valentine?
                  </h1>
                  <p class="subtitle">
                    I planned a cozy, sweet evening just for us. Dessert, a
                    surprise, and all my heart.
                  </p>

                  <div class="actions">
                    <v-btn
                      class="cta"
                      size="large"
                      color="deep-purple-accent-4"
                      @click="acceptInvitation"
                    >
                      Yes, I will
                    </v-btn>
                    <v-btn
                      class="ghost"
                      size="large"
                      variant="outlined"
                      color="deep-purple-accent-4"
                      :style="noBtnStyle"
                      @mouseenter="dodgeNo"
                      @focus="dodgeNo"
                      @pointerdown.prevent="dodgeNo"
                      @touchstart.prevent="dodgeNo"
                      @click="dodgeNo"
                    >
                      No (try to catch me)
                    </v-btn>
                  </div>

                  <div class="details">
                    <div class="detail">
                      <span class="detail-label">When</span>
                      <span class="detail-value">February 14</span>
                    </div>
                    <div class="detail">
                      <span class="detail-label">Dress</span>
                      <span class="detail-value">Your favorite glow</span>
                    </div>
                  </div>
                </section>

                <section class="visual">
                  <div class="photo-card">
                    <div class="photo-glow"></div>
                    <img
                      class="photo-img"
                      :src="photoUrl"
                      alt="Brittany and Kelvin"
                    />
                    <div class="photo-inner">
                      <div class="sparkle"></div>
                      <div class="monogram">B</div>
                      <p class="note">For you, always.</p>
                    </div>
                  </div>
                </section>
              </div>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
      <div class="signature-wrap">
      <v-chip class="signature" size="small" variant="tonal">
        <v-icon icon="mdi-account-circle-outline" start></v-icon>
        Created by OligarchC
      </v-chip>
    </div>
    </v-main>

    <div v-if="showCinematic" class="cinema-overlay">
      <div class="cinema-frame">
        <div class="cinema-glow"></div>
        <div class="cinema-seal">
          <span class="cinema-heart">?</span>
          <span class="cinema-stamp">Yes</span>
        </div>
        <div class="cinema-copy">
          <p class="cinema-eyebrow">A moment to remember</p>
          <h2 class="cinema-title">Brittany, you just made my year.</h2>
          <p class="cinema-subtitle">February 14 � Our story begins</p>
        </div>
        <button class="cinema-close" @click="showCinematic = false">Close</button>
      </div>
    </div>
  </v-app>
</template>

<script setup>
import { computed, ref } from 'vue'
import photoUrl from './assets/Brittany.JPG'

const showAlert = ref(false)
const noBtnOffset = ref({ x: 0, y: 0 })
const showCinematic = ref(false)

const acceptInvitation = () => {
  showAlert.value = true
  showCinematic.value = true
}

const dodgeNo = () => {
  const maxX = 120
  const maxY = 80
  const rand = (range) => Math.floor((Math.random() * 2 - 1) * range)
  noBtnOffset.value = {
    x: rand(maxX),
    y: rand(maxY)
  }
}

const noBtnStyle = computed(() => ({
  transform: `translate(${noBtnOffset.value.x}px, ${noBtnOffset.value.y}px)`
}))
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Playfair+Display:wght@500;700&family=Space+Grotesk:wght@400;500;600&display=swap');

.app-shell {
  min-height: 100vh;
  color: #1b1026;
  background: radial-gradient(circle at top, #fdf1f6 0%, #f7e1f2 35%, #f2d5ee 100%);
  font-family: 'Space Grotesk', system-ui, sans-serif;
}

.main {
  position: relative;
  z-index: 1;
}

.content {
  padding-top: clamp(32px, 8vh, 96px);
  padding-bottom: clamp(32px, 8vh, 96px);
}

.ambient {
  position: absolute;
  inset: 0;
  overflow: hidden;
  pointer-events: none;
  z-index: 0;
}

.orb {
  position: absolute;
  border-radius: 999px;
  filter: blur(0px);
  opacity: 0.5;
  mix-blend-mode: multiply;
  animation: float 10s ease-in-out infinite;
}

.orb-a {
  width: 260px;
  height: 260px;
  background: radial-gradient(circle, #ffd6e5 0%, #f6a8d8 65%, transparent 70%);
  top: -80px;
  left: -30px;
}

.orb-b {
  width: 320px;
  height: 320px;
  background: radial-gradient(circle, #d6f0ff 0%, #a6c8ff 60%, transparent 70%);
  bottom: -120px;
  right: -40px;
  animation-delay: -3s;
}

.orb-c {
  width: 200px;
  height: 200px;
  background: radial-gradient(circle, #ffe2b6 0%, #ffc98a 60%, transparent 70%);
  top: 35%;
  right: 15%;
  animation-delay: -6s;
}

.hero-card {
  position: relative;
  padding: clamp(24px, 5vw, 48px);
  border-radius: 28px;
  background: rgba(255, 255, 255, 0.85);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.6);
  box-shadow: 0 24px 60px rgba(91, 46, 104, 0.25);
  animation: reveal 1s ease both;
  overflow: hidden;
}

.love-alert {
  margin-bottom: 24px;
  border-radius: 16px;
  font-weight: 600;
}

.hero-grid {
  display: grid;
  gap: clamp(24px, 4vw, 48px);
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  align-items: center;
}

.copy {
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.eyebrow {
  text-transform: uppercase;
  letter-spacing: 0.2em;
  font-size: 0.72rem;
  color: #8f4e88;
  font-weight: 600;
}

.title {
  font-family: 'Playfair Display', serif;
  font-size: clamp(2.2rem, 4vw, 3.6rem);
  line-height: 1.1;
  margin: 0;
}

.subtitle {
  font-size: 1.05rem;
  color: #4d2f5f;
  margin: 0;
  max-width: 26rem;
}

.actions {
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
  position: relative;
}

.cta {
  text-transform: none;
  font-weight: 600;
  letter-spacing: 0.02em;
}

.ghost {
  text-transform: none;
  transition: transform 0.18s ease;
}

.details {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(140px, 1fr));
  gap: 12px;
  margin-top: 12px;
}

.detail {
  padding: 12px 16px;
  border-radius: 16px;
  background: rgba(250, 233, 244, 0.8);
  border: 1px solid rgba(221, 160, 211, 0.5);
}

.detail-label {
  display: block;
  font-size: 0.75rem;
  text-transform: uppercase;
  letter-spacing: 0.16em;
  color: #9a5f93;
}

.detail-value {
  font-weight: 600;
  color: #2a1736;
}

.visual {
  display: grid;
  gap: 16px;
  justify-items: center;
}

.photo-card {
  position: relative;
  width: min(280px, 80vw);
  aspect-ratio: 3 / 4;
  border-radius: 28px;
  overflow: hidden;
  background: linear-gradient(135deg, #2e143f, #5f2a73 60%, #9a4a90);
  box-shadow: 0 22px 50px rgba(52, 19, 77, 0.45);
}

.photo-img {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  filter: saturate(1.05) contrast(1.05);
}

.photo-glow {
  position: absolute;
  inset: -40% 0 0 -30%;
  background: radial-gradient(circle, rgba(255, 214, 229, 0.8) 0%, transparent 60%);
  animation: pulse 6s ease-in-out infinite;
}

.photo-inner {
  position: absolute;
  inset: 18px;
  border-radius: 22px;
  border: 1px solid rgba(255, 255, 255, 0.4);
  background: linear-gradient(160deg, rgba(255, 255, 255, 0.08), rgba(255, 255, 255, 0.02));
  display: grid;
  place-items: center;
  text-align: center;
  color: #fdf5ff;
  padding: 16px;
}

.sparkle {
  position: absolute;
  top: 18px;
  right: 18px;
  width: 60px;
  height: 60px;
  border-radius: 50%;
  background: radial-gradient(circle, rgba(255, 255, 255, 0.9) 0%, transparent 70%);
  opacity: 0.7;
  animation: twinkle 4s ease-in-out infinite;
}

.monogram {
  font-family: 'Playfair Display', serif;
  font-size: 4rem;
  letter-spacing: 0.1em;
}

.note {
  margin: 0;
  font-size: 1rem;
  letter-spacing: 0.08em;
  text-transform: uppercase;
}

.ticker {
  display: flex;
  gap: 12px;
  font-weight: 600;
  color: #7a3c80;
  text-transform: uppercase;
  letter-spacing: 0.3em;
  font-size: 0.7rem;
  animation: scroll 10s linear infinite;
}

.ticker span {
  padding: 6px 12px;
  border-radius: 999px;
  background: rgba(255, 255, 255, 0.7);
  border: 1px solid rgba(215, 157, 205, 0.5);
}


@keyframes reveal {
  from {
    opacity: 0;
    transform: translateY(18px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes float {
  0%, 100% {
    transform: translateY(0px);
  }
  50% {
    transform: translateY(18px);
  }
}

@keyframes pulse {
  0%, 100% {
    transform: translateY(0) scale(1);
    opacity: 0.7;
  }
  50% {
    transform: translateY(10px) scale(1.05);
    opacity: 0.9;
  }
}

@keyframes twinkle {
  0%, 100% {
    transform: scale(1);
    opacity: 0.5;
  }
  50% {
    transform: scale(1.1);
    opacity: 0.9;
  }
}

@keyframes scroll {
  0% {
    transform: translateX(0);
  }
  100% {
    transform: translateX(20px);
  }
}

@keyframes confetti-fall {
  0% {
    transform: translateY(-20%) rotate(0deg);
    opacity: 0;
  }
  15% {
    opacity: 1;
  }
  100% {
    transform: translateY(140%) rotate(240deg);
    opacity: 0;
  }
}

.cinema-overlay {
  position: fixed;
  inset: 0;
  display: grid;
  place-items: center;
  background: rgba(16, 8, 24, 0.55);
  backdrop-filter: blur(6px);
  z-index: 2000;
  animation: reveal 0.6s ease both;
}

.cinema-frame {
  width: min(520px, 90vw);
  border-radius: 36px;
  padding: clamp(28px, 4vw, 44px);
  color: #fdf7ff;
  background: radial-gradient(circle at top, rgba(255, 255, 255, 0.12) 0%, rgba(45, 17, 66, 0.9) 45%, rgba(20, 8, 30, 0.95) 100%);
  box-shadow: 0 40px 120px rgba(14, 6, 26, 0.65);
  position: relative;
  overflow: hidden;
  display: grid;
  gap: 28px;
  text-align: center;
}

.cinema-glow {
  position: absolute;
  inset: -40% 10% auto;
  height: 220px;
  background: radial-gradient(circle, rgba(255, 226, 198, 0.7) 0%, transparent 70%);
  opacity: 0.6;
  animation: pulse 6s ease-in-out infinite;
}

.cinema-seal {
  width: 140px;
  height: 140px;
  margin: 0 auto;
  border-radius: 50%;
  background: radial-gradient(circle, #ffb6d9 0%, #ff7eb8 60%, #c84c87 100%);
  display: grid;
  place-items: center;
  box-shadow: 0 18px 40px rgba(255, 120, 175, 0.45);
  position: relative;
  animation: seal-pop 0.8s ease both;
}

.cinema-heart {
  font-size: 2.6rem;
  color: #fff;
}

.cinema-stamp {
  position: absolute;
  bottom: -12px;
  right: -6px;
  background: #fff3fb;
  color: #8f2f6c;
  font-weight: 700;
  padding: 6px 16px;
  border-radius: 999px;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  font-size: 0.7rem;
}

.cinema-copy {
  display: grid;
  gap: 10px;
}

.cinema-eyebrow {
  text-transform: uppercase;
  letter-spacing: 0.35em;
  font-size: 0.7rem;
  opacity: 0.7;
  margin: 0;
}

.cinema-title {
  font-family: 'Playfair Display', serif;
  font-size: clamp(1.9rem, 4vw, 2.8rem);
  margin: 0;
}

.cinema-subtitle {
  margin: 0;
  opacity: 0.8;
}

.cinema-close {
  justify-self: center;
  background: rgba(255, 255, 255, 0.12);
  border: 1px solid rgba(255, 255, 255, 0.25);
  color: #fff;
  border-radius: 999px;
  padding: 8px 18px;
  font-size: 0.7rem;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  cursor: pointer;
}

@keyframes seal-pop {
  0% {
    transform: scale(0.6);
    opacity: 0;
  }
  60% {
    transform: scale(1.05);
    opacity: 1;
  }
  100% {
    transform: scale(1);
  }
}

.signature-wrap {
  display: flex;
  justify-content: center;
  margin: 0 0 32px;
}
.signature {
  margin: 0 auto 32px;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  color: rgba(41, 21, 56, 0.7);
}
@media (max-width: 600px) {
  .actions {
    flex-direction: column;
    align-items: stretch;
  }

  .ticker {
    justify-content: center;
    flex-wrap: wrap;
    animation: none;
  }
}
</style>

