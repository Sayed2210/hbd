<template>
  <div style="display: none">
    <div ref="youtubePlayer"></div>
  </div>

  <div
    v-if="currentSection === 'landing'"
    class="min-h-screen gradient-bg flex items-center justify-center relative overflow-hidden"
  >
    <!-- Floating Hearts -->
    <div
      v-for="particle in particles"
      :key="particle.id"
      class="floating-heart absolute text-pink-400 opacity-30"
      :style="{
        left: particle.left + '%',
        top: particle.top + '%',
        '--duration': particle.duration + 's',
        '--delay': particle.delay + 's',
        fontSize: particle.size + 'px',
      }"
    >
      ❤️
    </div>

    <div class="text-center z-10 px-4 fade-in-up">
      <h1
        class="dancing text-6xl md:text-8xl text-pink-600 mb-6 heartbeat-hover"
      >
        Happy Birthday<br />My Love 💖
      </h1>
      <p class="playfair text-2xl md:text-3xl text-pink-700 italic mb-12">
        To the one who makes my heart sing
      </p>
      <button
        @click="currentSection = 'timeline'"
        class="bg-gradient-to-r from-pink-500 to-rose-500 text-white px-10 py-4 rounded-full text-lg font-semibold shadow-lg hover:shadow-xl transform hover:scale-105 transition-all duration-300 heartbeat-hover"
      >
        Enter My Heart ❤️
      </button>
    </div>
  </div>

  <!-- Navigation Menu -->
  <div
    v-if="currentSection !== 'landing'"
    class="fixed top-0 left-0 right-0 bg-white/90 backdrop-blur-sm shadow-md z-50 px-4 py-3"
  >
    <div class="w-full mx-auto flex justify-between items-center">
      <h2 class="dancing text-2xl text-pink-600">Our Love Story 💕</h2>
      <div class="flex gap-2 md:gap-4 overflow-x-auto">
        <button
          @click="currentSection = 'timeline'"
          :class="
            currentSection === 'timeline'
              ? 'bg-pink-500 text-white'
              : 'bg-pink-100 text-pink-600'
          "
          class="px-3 py-2 rounded-lg text-sm whitespace-nowrap hover:bg-pink-400 hover:text-white transition-colors"
        >
          Timeline
        </button>
        <!-- <button
          @click="currentSection = 'letters'"
          :class="
            currentSection === 'letters'
              ? 'bg-pink-500 text-white'
              : 'bg-pink-100 text-pink-600'
          "
          class="px-3 py-2 rounded-lg text-sm whitespace-nowrap hover:bg-pink-400 hover:text-white transition-colors"
        >
          Letters
        </button> -->
        <button
          @click="currentSection = 'gallery'"
          :class="
            currentSection === 'gallery'
              ? 'bg-pink-500 text-white'
              : 'bg-pink-100 text-pink-600'
          "
          class="px-3 py-2 rounded-lg text-sm whitespace-nowrap hover:bg-pink-400 hover:text-white transition-colors"
        >
          Gallery
        </button>
        <button
          @click="currentSection = 'reasons'"
          :class="
            currentSection === 'reasons'
              ? 'bg-pink-500 text-white'
              : 'bg-pink-100 text-pink-600'
          "
          class="px-3 py-2 rounded-lg text-sm whitespace-nowrap hover:bg-pink-400 hover:text-white transition-colors"
        >
          Why I Love You
        </button>
        <button
          @click="currentSection = 'final'"
          :class="
            currentSection === 'final'
              ? 'bg-pink-500 text-white'
              : 'bg-pink-100 text-pink-600'
          "
          class="px-3 py-2 rounded-lg text-sm whitespace-nowrap hover:bg-pink-400 hover:text-white transition-colors"
        >
          Surprise
        </button>
      </div>
    </div>
  </div>

  <!-- Timeline Section -->
  <div
    v-if="currentSection === 'timeline'"
    class="min-h-screen gradient-bg pt-24 pb-12 px-4"
  >
    <div class="w-full mx-auto">
      <h2 class="dancing text-5xl md:text-6xl text-pink-600 text-center mb-16">
        Our Love Story ✨
      </h2>

      <div class="relative">
        <div class="timeline-line hidden md:block"></div>

        <div
          v-for="(event, index) in timeline"
          :key="index"
          class="mb-12 fade-in-up"
          :style="{ animationDelay: index * 0.2 + 's' }"
        >
          <div
            class="flex flex-col md:flex-row items-center gap-4"
            :class="index % 2 === 0 ? 'md:flex-row' : 'md:flex-row-reverse'"
          >
            <div
              class="md:w-1/2"
              :class="
                index % 2 === 0
                  ? 'md:text-right md:pr-12'
                  : 'md:text-left md:pl-12'
              "
            >
              <div
                class="bg-white rounded-2xl p-6 shadow-lg hover:shadow-xl transition-shadow"
              >
                <div class="text-4xl mb-3">{{ event.emoji }}</div>
                <h3 class="playfair text-2xl font-bold text-pink-700 mb-2">
                  {{ event.title }}
                </h3>
                <p class="text-sm text-pink-500 mb-3">{{ event.date }}</p>
                <p class="text-gray-700 leading-relaxed">
                  {{ event.description }}
                </p>
              </div>
            </div>
            <div
              class="hidden md:flex w-12 h-12 bg-pink-500 rounded-full items-center justify-center text-white text-xl shadow-lg z-10"
            >
              ❤️
            </div>
            <div class="md:w-1/2"></div>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- Love Letters Section -->
  <div
    v-if="currentSection === 'letters'"
    class="min-h-screen gradient-bg pt-24 pb-12 px-4"
  >
    <div class="w-full mx-auto">
      <h2 class="dancing text-5xl md:text-6xl text-pink-600 text-center mb-16">
        Love Letters 💌
      </h2>

      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
        <div
          v-for="(letter, index) in letters"
          :key="index"
          class="card-flip"
          :class="{ 'card-flipped': openLetter === index }"
        >
          <div class="card-flip-inner relative h-80">
            <!-- Front -->
            <div
              class="card-front absolute w-full h-full bg-white rounded-2xl shadow-lg p-8 flex flex-col items-center justify-center cursor-pointer hover:shadow-xl transition-shadow"
              @click="openLetter = index"
            >
              <div class="text-6xl mb-4">{{ letter.icon }}</div>
              <h3 class="dancing text-3xl text-pink-600 mb-4">
                {{ letter.title }}
              </h3>
              <p class="text-pink-400 text-sm">Click to open</p>
            </div>

            <!-- Back -->
            <div
              class="card-back absolute w-full h-full bg-gradient-to-br from-pink-50 to-rose-50 rounded-2xl shadow-lg p-6 overflow-y-auto"
            >
              <button
                @click="openLetter = null"
                class="absolute top-4 right-4 text-pink-400 hover:text-pink-600"
              >
                ✕
              </button>
              <h3 class="dancing text-2xl text-pink-600 mb-4">
                {{ letter.title }}
              </h3>
              <p class="playfair text-gray-700 leading-relaxed italic">
                {{ letter.content }}
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- Gallery Section -->
  <div
    v-if="currentSection === 'gallery'"
    class="min-h-screen gradient-bg pt-24 pb-12 px-4"
  >
    <div class="w-full mx-auto">
      <h2 class="dancing text-5xl md:text-6xl text-pink-600 text-center mb-8">
        Our Memories 📸
      </h2>

      <div class="mb-8 flex justify-center">
        <button
          @click="toggleMusic"
          class="bg-white rounded-full px-6 py-3 shadow-lg hover:shadow-xl transition-shadow flex items-center gap-2 text-pink-600"
        >
          <span class="w-5 h-5">{{ musicPlaying ? "⏸️" : "▶️" }}</span>
          {{ musicPlaying ? "Pause Music" : "Play Music" }}
        </button>
      </div>
      <!-- Hidden audio element -->

      <div class="bg-white rounded-3xl shadow-2xl p-8 mb-4">
        <swiper
          :effect="'coverflow'"
          :grabCursor="true"
          :centeredSlides="true"
          :slidesPerView="1"
          :coverflowEffect="{
            rotate: 50,
            stretch: 0,
            depth: 100,
            modifier: 1,
            slideShadows: true,
          }"
          :navigation="true"
          :loop="true"
          :modules="modules"
          class="mySwiper h-96"
        >
          <swiper-slide
            v-for="(image, index) in galleryImages"
            :key="index"
            class="swiper-slide"
          >
            <div class="text-center">
              <div
                class="bg-gradient-to-br from-pink-200 to-rose-200 rounded-2xl w-96 h-96 flex items-center justify-center mb-4"
              >
                <img
                  :src="image.icon"
                  alt="Gallery Image"
                  class="object-cover aspect-square"
                />
              </div>
              <p class="playfair text-lg text-gray-700 italic">
                {{ image.caption }}
              </p>
            </div>
          </swiper-slide>
        </swiper>
      </div>
    </div>
  </div>

  <!-- Why I Love You Section -->
  <div
    v-if="currentSection === 'reasons'"
    class="min-h-screen gradient-bg pt-24 pb-12 px-4"
  >
    <div class="w-full mx-auto">
      <h2 class="dancing text-5xl md:text-6xl text-pink-600 text-center mb-16">
        Why I Love You 💕
      </h2>

      <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
        <div
          v-for="(reason, index) in reasons"
          :key="index"
          class="bg-white rounded-2xl p-6 shadow-lg hover:shadow-xl transition-all hover:-translate-y-1 fade-in-up"
          :style="{ animationDelay: index * 0.1 + 's' }"
        >
          <div class="flex items-start gap-4">
            <div class="text-3xl">{{ reason.icon }}</div>
            <div>
              <h3 class="playfair text-xl font-bold text-pink-700 mb-2">
                {{ reason.title }}
              </h3>
              <p class="text-gray-600">{{ reason.description }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- Final Surprise Section -->
  <div
    v-if="currentSection === 'final'"
    class="min-h-screen gradient-bg flex items-center justify-center relative overflow-hidden px-4"
  >
    <!-- Confetti -->
    <div
      v-for="piece in confettiPieces"
      :key="piece.id"
      class="confetti-piece"
      :style="{
        left: piece.left + '%',
        top: '-10px',
        backgroundColor: piece.color,
        animationDelay: piece.delay + 's',
      }"
    ></div>

    <div class="text-center z-10 max-w-2xl">
      <div v-if="!showFinal" class="fade-in-up">
        <h2 class="dancing text-4xl md:text-5xl text-pink-600 mb-8">
          One More Thing... 🎁
        </h2>
        <p class="playfair text-xl text-gray-700 mb-12 italic">
          Before we end this journey, I want to tell you something special...
        </p>
        <button
          @click="revealFinal"
          class="bg-gradient-to-r from-pink-500 to-rose-500 text-white px-12 py-4 rounded-full text-lg font-semibold shadow-lg hover:shadow-xl transform hover:scale-105 transition-all heartbeat-hover"
        >
          Reveal My Heart 💝
        </button>
      </div>

      <div v-else class="fade-in-up">
        <div class="text-8xl mb-8 heartbeat-hover inline-block">💍</div>
        <h2 class="dancing text-5xl md:text-7xl text-pink-600 mb-6">
          I Choose You
        </h2>
        <p class="playfair text-3xl md:text-4xl text-pink-700 mb-6 italic">
          Today. Tomorrow. Always.
        </p>
        <p class="text-xl text-gray-700 leading-relaxed max-w-xl mx-auto">
          Every moment with you is a gift. Every laugh, every smile, every quiet
          moment together. You are my best friend, my partner, my everything.
          Happy Birthday, my love. Here's to forever with you. ❤️
        </p>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from "vue";
import { Swiper, SwiperSlide } from "swiper/vue";
import { EffectCoverflow, Pagination, Navigation } from "swiper/modules";
import "swiper/css";
import "swiper/css/effect-coverflow";
import "swiper/css/pagination";
import "swiper/css/navigation";

import image1 from "./assets/1.jpeg";
import image2 from "./assets/2.jpeg";
import image4 from "./assets/4.jpeg";
import image5 from "./assets/5.jpeg";

// Types
interface Particle {
  id: number;
  left: number;
  top: number;
  delay: number;
  duration: number;
  size: number;
}

interface ConfettiPiece {
  id: number;
  left: number;
  delay: number;
  color: string;
}

interface TimelineEvent {
  date: string;
  title: string;
  description: string;
  emoji: string;
}

interface Letter {
  icon: string;
  title: string;
  content: string;
}

interface GalleryImage {
  icon: string;
  caption: string;
}

interface Reason {
  icon: string;
  title: string;
  description: string;
}

// Reactive state
const currentSection = ref<string>("landing");
const openLetter = ref<number | null>(null);
const showFinal = ref<boolean>(false);
const musicPlaying = ref<boolean>(false);
const particles = ref<Particle[]>([]);
const confettiPieces = ref<ConfettiPiece[]>([]);
const modules = [EffectCoverflow, Pagination, Navigation];

const youtubePlayer = ref<HTMLDivElement | null>(null);
let player: any = null;

onMounted(() => {
  // Check if API is already loaded
  if ((window as any).YT) {
    initPlayer();
  } else {
    // Load YouTube IFrame API
    const tag = document.createElement("script");
    tag.src = "https://www.youtube.com/iframe_api";
    const firstScriptTag = document.getElementsByTagName("script")[0];
    firstScriptTag?.parentNode?.insertBefore(tag, firstScriptTag);

    // Initialize player when API is ready
    (window as any).onYouTubeIframeAPIReady = () => {
      initPlayer();
    };
  }
});

const initPlayer = () => {
  if (!youtubePlayer.value) {
    console.error("YouTube player element not found");
    return;
  }

  player = new (window as any).YT.Player(youtubePlayer.value, {
    height: "0",
    width: "0",
    videoId: "z4KMUyXeXEk",
    playerVars: {
      autoplay: 0,
      controls: 0,
      loop: 1,
      playlist: "z4KMUyXeXEk",
    },
    events: {
      onReady: (event: any) => {
        console.log(event, "YouTube player ready");
      },
    },
  });
};

const toggleMusic = () => {
  if (!player || !player.playVideo) {
    console.error("Player not ready");
    return;
  }
  if (musicPlaying.value) {
    player.pauseVideo();
  } else {
    player.playVideo();
  }

  musicPlaying.value = !musicPlaying.value;
};

// Data
const timeline = ref<TimelineEvent[]>([
  {
    date: "NO Date i can't remember",
    title: "The Day We Met",
    description:
      "The universe conspired to bring us together. I still remember how my heart skipped a beat when I first saw you.",
    emoji: "✨",
  },
  {
    date: "Dec 25, 2024",
    title: "First Message",
    description:
      "You replied to my message, and suddenly my world had color again. Those late-night conversations became my favorite part of the day.",
    emoji: "💬",
  },
  {
    date: "February 10, 2024",
    title: "Our First Date",
    description:
      "Coffee turned into hours of conversation. Time stopped, and I knew you were someone truly special.",
    emoji: "☕",
  },
  {
    date: "NO Date i can't remember",
    title: "First 'I Love You'",
    description:
      "Three words that changed everything. My heart was yours from that moment on.",
    emoji: "💕",
  },
  // {
  //   date: "June 5, 2023",
  //   title: "Our First Trip Together",
  //   description:
  //     "Adventure with you by my side. Every destination is perfect when I'm with you.",
  //   emoji: "✈️",
  // },
  {
    date: "Today",
    title: "Your Special Day",
    description:
      "Celebrating the most incredible person I know. Thank you for being you.",
    emoji: "🎂",
  },
]);

const letters = ref<Letter[]>([
  {
    icon: "💌",
    title: "My Dearest",
    content:
      "From the moment you walked into my life, everything changed. You brought light into my darkest days and made my happiest moments even brighter. Your laugh is my favorite sound, your smile is my favorite sight, and your happiness is my greatest mission.",
  },
  {
    icon: "🌹",
    title: "My Beautiful",
    content:
      "You are more beautiful than any sunset, more precious than any treasure. But it's not just your beauty that captivates me—it's your kind heart, your brilliant mind, and the way you make everyone around you feel special.",
  },
  {
    icon: "💝",
    title: "My Forever",
    content:
      "I don't know what I did to deserve you, but I thank the stars every day that you chose me. You are my best friend, my partner in crime, my safe place. With you, I am home.",
  },
  {
    icon: "🌟",
    title: "My Inspiration",
    content:
      "You inspire me to be better every single day. Your strength amazes me, your compassion humbles me, and your love completes me. Thank you for being exactly who you are.",
  },
  {
    icon: "💖",
    title: "My Everything",
    content:
      "Words cannot express how deeply I love you. You are my first thought in the morning and my last thought at night. Every moment with you is a blessing I never take for granted.",
  },
  {
    icon: "🦋",
    title: "My Love",
    content:
      "Happy Birthday to the person who makes my world infinitely better. May this year bring you all the joy, love, and happiness you bring to others. I love you more than words can say.",
  },
]);

const galleryImages = ref<GalleryImage[]>([
  {
    icon: image1,
    caption: "Our first photo together - the start of something beautiful",
  },
  {
    icon: image2,
    caption: "That time we laughed until we cried",
  },
  {
    icon: image4,
    caption: "Adventures and silly moments",
  },
  {
    icon: image5,
    caption: "Late night food runs and deep conversations",
  },
  // { icon: "./src/assets/6.jpeg", caption: "You make every moment special" },
]);

const reasons = ref<Reason[]>([
  {
    icon: "😊",
    title: "Your Smile",
    description: "It lights up my entire world and makes everything better",
  },
  {
    icon: "💫",
    title: "Your Kindness",
    description: "The way you care for others inspires me every day",
  },
  {
    icon: "🎵",
    title: "Your Laugh",
    description: "It's contagious, genuine, and my favorite sound",
  },
  {
    icon: "🧠",
    title: "Your Intelligence",
    description: "You challenge me to think and grow",
  },
  {
    icon: "💪",
    title: "Your Strength",
    description: "You face every challenge with grace and courage",
  },
  {
    icon: "🤗",
    title: "Your Warmth",
    description: "You make me feel safe, loved, and understood",
  },
  {
    icon: "🎨",
    title: "Your Creativity",
    description: "You see beauty and possibility everywhere",
  },
  {
    icon: "👂",
    title: "How You Listen",
    description: "You truly hear me and make me feel valued",
  },
  {
    icon: "🌈",
    title: "Your Optimism",
    description: "You find light even on the darkest days",
  },
  {
    icon: "💗",
    title: "Your Love",
    description: "The way you love makes me want to be a better person",
  },
]);

// Methods
const generateParticles = (): void => {
  particles.value = Array.from({ length: 20 }, (_, i) => ({
    id: i,
    left: Math.random() * 100,
    top: Math.random() * 100,
    delay: Math.random() * 5,
    duration: 8 + Math.random() * 4,
    size: 20 + Math.random() * 20,
  }));
};

const revealFinal = (): void => {
  showFinal.value = true;
  createConfetti();
};

const createConfetti = (): void => {
  const colors = ["#ff69b4", "#ff1493", "#ff85c1", "#ffa5d8", "#ff6b9d"];
  confettiPieces.value = Array.from(
    { length: 50 },
    (_, i) =>
      ({
        id: i,
        left: Math.random() * 100,
        delay: Math.random() * 2,
        color: colors[Math.floor(Math.random() * colors.length)] || colors[0],
      } as ConfettiPiece)
  );
};

// Lifecycle
onMounted(() => {
  generateParticles();
});

// Watchers
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Dancing+Script:wght@400;700&family=Playfair+Display:ital,wght@0,400;0,700;1,400&family=Poppins:wght@300;400;600&display=swap");

body {
  margin: 0;
  font-family: "Poppins", sans-serif;
  overflow-x: hidden;
}

.dancing {
  font-family: "Dancing Script", cursive;
}
.playfair {
  font-family: "Playfair Display", serif;
}

@keyframes float {
  0%,
  100% {
    transform: translateY(0) rotate(0deg);
  }
  50% {
    transform: translateY(-30px) rotate(10deg);
  }
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes heartbeat {
  0%,
  100% {
    transform: scale(1);
  }
  25% {
    transform: scale(1.1);
  }
  50% {
    transform: scale(1);
  }
}

@keyframes confettiFall {
  0% {
    transform: translateY(-100vh) rotate(0deg);
    opacity: 1;
  }
  100% {
    transform: translateY(100vh) rotate(720deg);
    opacity: 0;
  }
}

@keyframes typewriter {
  from {
    width: 0;
  }
  to {
    width: 100%;
  }
}

.floating-heart {
  animation: float var(--duration) ease-in-out infinite;
  animation-delay: var(--delay);
}

.fade-in-up {
  animation: fadeInUp 0.8s ease-out forwards;
}

.heartbeat-hover:hover {
  animation: heartbeat 0.6s ease-in-out;
}

.confetti-piece {
  position: fixed;
  width: 10px;
  height: 10px;
  animation: confettiFall 3s linear forwards;
  z-index: 1000;
}

.gradient-bg {
  background: linear-gradient(
    135deg,
    #ffeef8 0%,
    #ffe4f1 25%,
    #ffd4e9 50%,
    #ffc4e1 75%,
    #ffb4d9 100%
  );
}

.card-flip {
  /* perspective: 1000px; */
  height: 320px;
}

.card-flip-inner {
  transition: transform 0.6s;
  transform-style: preserve-3d;
}

.card-flipped .card-flip-inner {
  transform: rotateY(180deg);
}

.card-front,
.card-back {
  backface-visibility: hidden;
}

.card-back {
  transform: rotateY(180deg);
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

.swiper {
  width: 100%;
  height: 100%;
}

.swiper-slide {
  display: flex;
  justify-content: center;
  align-items: center;
}

.timeline-line {
  position: absolute;
  left: 50%;
  top: 0;
  bottom: 0;
  width: 2px;
  background: linear-gradient(to bottom, #ffc4e1, #ff8fb3);
}

@media (max-width: 768px) {
  .timeline-line {
    left: 20px;
  }
}

/* Utility Classes (TailwindCSS-like) */
.min-h-screen {
  min-height: 100vh;
}
.flex {
  display: flex;
}
.grid {
  display: grid;
}
.hidden {
  display: none;
}
.absolute {
  position: absolute;
}
.relative {
  position: relative;
}
.fixed {
  position: fixed;
}
.overflow-hidden {
  overflow: hidden;
}
.overflow-x-auto {
  overflow-x: auto;
}
.overflow-y-auto {
  overflow-y: auto;
}

.items-center {
  align-items: center;
}
.items-start {
  align-items: start;
}
.justify-center {
  justify-content: center;
}
.justify-between {
  justify-content: space-between;
}
.flex-col {
  flex-direction: column;
}

.text-center {
  text-align: center;
}
.text-left {
  text-align: left;
}
.text-right {
  text-align: right;
}

.w-full {
  width: 100%;
}
.w-5 {
  width: 1.25rem;
}
.w-12 {
  width: 3rem;
}
.w-96 {
  width: 24rem;
}
.h-5 {
  height: 1.25rem;
}
.h-12 {
  height: 3rem;
}
.h-80 {
  height: 20rem;
}
.h-96 {
  height: 24rem;
}

.top-0 {
  top: 0;
}
.top-4 {
  top: 1rem;
}
.left-0 {
  left: 0;
}
.right-0 {
  right: 0;
}
.right-4 {
  right: 1rem;
}
.bottom-0 {
  bottom: 0;
}

.z-10 {
  z-index: 10;
}
.z-50 {
  z-index: 50;
}

.px-3 {
  padding-left: 0.75rem;
  padding-right: 0.75rem;
}
.px-4 {
  padding-left: 1rem;
  padding-right: 1rem;
}
.px-6 {
  padding-left: 1.5rem;
  padding-right: 1.5rem;
}
.px-10 {
  padding-left: 2.5rem;
  padding-right: 2.5rem;
}
.px-12 {
  padding-left: 3rem;
  padding-right: 3rem;
}
.py-2 {
  padding-top: 0.5rem;
  padding-bottom: 0.5rem;
}
.py-3 {
  padding-top: 0.75rem;
  padding-bottom: 0.75rem;
}
.py-4 {
  padding-top: 1rem;
  padding-bottom: 1rem;
}
.p-6 {
  padding: 1.5rem;
}
.p-8 {
  padding: 2rem;
}
.pt-24 {
  padding-top: 6rem;
}
.pb-12 {
  padding-bottom: 3rem;
}

.m-0 {
  margin: 0;
}
.mb-2 {
  margin-bottom: 0.5rem;
}
.mb-3 {
  margin-bottom: 0.75rem;
}
.mb-4 {
  margin-bottom: 1rem;
}
.mb-6 {
  margin-bottom: 1.5rem;
}
.mb-8 {
  margin-bottom: 2rem;
}
.mb-12 {
  margin-bottom: 3rem;
}
.mb-16 {
  margin-bottom: 4rem;
}
.mx-auto {
  margin-left: auto;
  margin-right: auto;
}

.gap-2 {
  gap: 0.5rem;
}
.gap-4 {
  gap: 1rem;
}
.gap-6 {
  gap: 1.5rem;
}
.gap-8 {
  gap: 2rem;
}

.grid-cols-1 {
  grid-template-columns: repeat(1, minmax(0, 1fr));
}

.text-sm {
  font-size: 0.875rem;
}
.text-lg {
  font-size: 1.125rem;
}
.text-xl {
  font-size: 1.25rem;
}
.text-2xl {
  font-size: 1.5rem;
}
.text-3xl {
  font-size: 1.875rem;
}
.text-4xl {
  font-size: 2.25rem;
}
.text-5xl {
  font-size: 3rem;
}
.text-6xl {
  font-size: 3.75rem;
}
.text-8xl {
  font-size: 6rem;
}

.font-semibold {
  font-weight: 600;
}
.font-bold {
  font-weight: 700;
}
.italic {
  font-style: italic;
}
.whitespace-nowrap {
  white-space: nowrap;
}
.leading-relaxed {
  line-height: 1.625;
}

.text-white {
  color: white;
}
.text-gray-600 {
  color: #4b5563;
}
.text-gray-700 {
  color: #374151;
}
.text-pink-400 {
  color: #f472b6;
}
.text-pink-500 {
  color: #ec4899;
}
.text-pink-600 {
  color: #db2777;
}
.text-pink-700 {
  color: #be185d;
}

.bg-white {
  background-color: white;
}
.bg-pink-100 {
  background-color: #fce7f3;
}
.bg-pink-500 {
  background-color: #ec4899;
}

.bg-gradient-to-r {
  background-image: linear-gradient(to right, var(--tw-gradient-stops));
}
.bg-gradient-to-br {
  background-image: linear-gradient(to bottom right, var(--tw-gradient-stops));
}
.from-pink-50 {
  --tw-gradient-from: #fdf2f8;
  --tw-gradient-stops: var(--tw-gradient-from),
    var(--tw-gradient-to, rgba(253, 242, 248, 0));
}
.from-pink-200 {
  --tw-gradient-from: #fbcfe8;
  --tw-gradient-stops: var(--tw-gradient-from),
    var(--tw-gradient-to, rgba(251, 207, 232, 0));
}
.from-pink-500 {
  --tw-gradient-from: #ec4899;
  --tw-gradient-stops: var(--tw-gradient-from),
    var(--tw-gradient-to, rgba(236, 72, 153, 0));
}
.to-rose-50 {
  --tw-gradient-to: #fff1f2;
}
.to-rose-200 {
  --tw-gradient-to: #fecdd3;
}
.to-rose-500 {
  --tw-gradient-to: #f43f5e;
}

.opacity-30 {
  opacity: 0.3;
}

.rounded-lg {
  border-radius: 0.5rem;
}
.rounded-xl {
  border-radius: 0.75rem;
}
.rounded-2xl {
  border-radius: 1rem;
}
.rounded-3xl {
  border-radius: 1.5rem;
}
.rounded-full {
  border-radius: 9999px;
}

.shadow-lg {
  box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1),
    0 4px 6px -2px rgba(0, 0, 0, 0.05);
}
.shadow-xl {
  box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1),
    0 10px 10px -5px rgba(0, 0, 0, 0.04);
}
.shadow-2xl {
  box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.25);
}
.shadow-md {
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1),
    0 2px 4px -1px rgba(0, 0, 0, 0.06);
}

.backdrop-blur-sm {
  backdrop-filter: blur(4px);
}

.cursor-pointer {
  cursor: pointer;
}

.transform {
  transform: translateX(0);
}
.transition-all {
  transition: all 0.3s ease;
}
.transition-shadow {
  transition: box-shadow 0.3s ease;
}
.transition-colors {
  transition: color 0.3s ease, background-color 0.3s ease;
}
.duration-300 {
  transition-duration: 300ms;
}

.hover\:shadow-xl:hover {
  box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1),
    0 10px 10px -5px rgba(0, 0, 0, 0.04);
}
.hover\:scale-105:hover {
  transform: scale(1.05);
}
.hover\:-translate-y-1:hover {
  transform: translateY(-0.25rem);
}
.hover\:bg-pink-400:hover {
  background-color: #f472b6;
}
.hover\:bg-pink-600:hover {
  background-color: #db2777;
}
.hover\:text-white:hover {
  color: white;
}
.hover\:text-pink-600:hover {
  color: #db2777;
}

.inline-block {
  display: inline-block;
}
.max-w-xl {
  max-width: 36rem;
}
.max-w-2xl {
  max-width: 42rem;
}
.max-w-4xl {
  max-width: 56rem;
}
.max-w-6xl {
  max-width: 72rem;
}

.w-full {
  width: 100%;
}
/* Responsive utilities */
@media (min-width: 768px) {
  .md\:flex {
    display: flex;
  }
  .md\:block {
    display: block;
  }
  .md\:hidden {
    display: none;
  }
  .md\:flex-row {
    flex-direction: row;
  }
  .md\:flex-row-reverse {
    flex-direction: row-reverse;
  }
  .md\:gap-4 {
    gap: 1rem;
  }
  .md\:grid-cols-2 {
    grid-template-columns: repeat(2, minmax(0, 1fr));
  }
  .md\:w-1\/2 {
    width: 50%;
  }
  .md\:text-right {
    text-align: right;
  }
  .md\:text-left {
    text-align: left;
  }
  .md\:pr-12 {
    padding-right: 3rem;
  }
  .md\:pl-12 {
    padding-left: 3rem;
  }
  .md\:text-5xl {
    font-size: 3rem;
  }
  .md\:text-6xl {
    font-size: 3.75rem;
  }
  .md\:text-7xl {
    font-size: 4.5rem;
  }
  .md\:text-8xl {
    font-size: 6rem;
  }
  .md\:text-3xl {
    font-size: 1.875rem;
  }
  .md\:text-4xl {
    font-size: 2.25rem;
  }
}

@media (min-width: 1024px) {
  .lg\:grid-cols-3 {
    grid-template-columns: repeat(3, minmax(0, 1fr));
  }
}

/* Swiper overrides */
.\!text-pink-500 {
  color: #ec4899 !important;
}
.\!bottom-0 {
  bottom: 0 !important;
}
</style>
