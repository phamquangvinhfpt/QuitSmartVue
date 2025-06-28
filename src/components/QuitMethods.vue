<template>
  <section class="py-20 px-4 bg-gray-50">
    <div class="container mx-auto">
      <div 
        ref="headerSection"
        class="text-center mb-16"
      >
        <h2 class="text-4xl font-bold text-gray-900 mb-4">Phương pháp cai thuốc được hỗ trợ</h2>
        <p class="text-xl text-gray-600 max-w-2xl mx-auto">
          QuitSmart hỗ trợ nhiều phương pháp cai thuốc khác nhau phù hợp với từng cá nhân
        </p>
      </div>

      <div 
        ref="methodsGrid"
        class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6"
      >
        <div 
          v-for="(method, index) in quitMethods" 
          :key="method.id"
          :ref="(el) => { methodCards[index] = el as HTMLElement }"
          class="bg-white rounded-lg shadow-md p-6 text-center hover:shadow-lg transition-all duration-500 transform hover:scale-110 hover:-translate-y-2"
        >
          <div 
            :class="`w-12 h-12 ${method.bgColor} rounded-full mx-auto mb-4 flex items-center justify-center transform transition-all duration-500 hover:rotate-12 hover:scale-125`"
          >
            <component 
              :is="method.icon" 
              :class="`h-6 w-6 ${method.iconColor} transition-transform duration-300`" 
            />
          </div>
          <h4 class="font-bold text-gray-900 mb-2">{{ method.name }}</h4>
          <p class="text-sm text-gray-600 mb-3">{{ method.description }}</p>
          <div class="text-xs text-gray-500">
            Tỷ lệ thành công: 
            <span 
              :ref="(el) => { successRates[index] = el as HTMLElement }"
              class="font-semibold text-green-600"
            >0%</span>
          </div>
          
          <!-- Progress bar animation -->
          <div class="w-full bg-gray-200 rounded-full h-2 mt-3 overflow-hidden">
            <div 
              :ref="(el) => { progressBars[index] = el as HTMLElement }"
              class="h-2 rounded-full transition-all duration-1000 ease-out"
              :class="getProgressBarColor(method.successRate)"
              style="width: 0%"
            ></div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref, onMounted, nextTick } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'
import { Zap, TrendingUp, Brain, Shield } from 'lucide-vue-next'

// Register ScrollTrigger plugin
gsap.registerPlugin(ScrollTrigger)

// Animation refs
const headerSection = ref<HTMLElement>()
const methodsGrid = ref<HTMLElement>()
const methodCards = ref<(HTMLElement | null)[]>([])
const successRates = ref<(HTMLElement | null)[]>([])
const progressBars = ref<(HTMLElement | null)[]>([])

// Get progress bar color based on success rate
const getProgressBarColor = (rate: number) => {
  if (rate >= 80) return 'bg-green-500'
  if (rate >= 70) return 'bg-blue-500'
  if (rate >= 60) return 'bg-yellow-500'
  return 'bg-red-500'
}

// Animation functions
const animateMethods = () => {
  if (!headerSection.value || !methodsGrid.value) {
    console.warn('Required elements not found for animation')
    return
  }

  // Set initial opacity to 0 before animating
  gsap.set([headerSection.value, methodsGrid.value], { opacity: 0 })
  gsap.set(methodCards.value.filter(el => el !== null), { opacity: 0 })

  const tl = gsap.timeline()

  tl.to(headerSection.value, {
    opacity: 1,
    y: 0,
    duration: 0.8,
    ease: "power2.out"
  })
  .to(methodsGrid.value, {
    opacity: 1,
    y: 0,
    duration: 0.8,
    ease: "power2.out"
  }, "-=0.4")
  .to(methodCards.value.filter(el => el !== null), {
    opacity: 1,
    y: 0,
    scale: 1,
    duration: 0.8,
    stagger: 0.15,
    ease: "back.out(1.7)",
    onComplete: () => {
      // Animate success rates and progress bars
      quitMethods.value.forEach((method, index) => {
        const rateEl = successRates.value[index]
        const barEl = progressBars.value[index]
        
        // Animate success rate number
        if (rateEl) {
          const obj = { value: 0 }
          gsap.to(obj, {
            value: method.successRate,
            duration: 1.5,
            ease: "power2.out",
            onUpdate: () => {
              (rateEl as HTMLElement).textContent = Math.round(obj.value) + '%'
            }
          })
        }

        // Animate progress bar
        if (barEl) {
          gsap.to(barEl, {
            width: `${method.successRate}%`,
            duration: 1.5,
            delay: index * 0.2,
            ease: "power2.out"
          })
        }
      })
    }
  }, "-=0.4")
}

// Setup ScrollTrigger
const setupScrollAnimation = () => {
  ScrollTrigger.create({
    trigger: headerSection.value,
    start: "top 80%",
    onEnter: animateMethods,
    once: true
  })
}

onMounted(async () => {
  await nextTick()
  setupScrollAnimation()
})

// Quit methods
const quitMethods = ref([
  {
    id: 1,
    name: 'Cai đột ngột',
    description: 'Ngừng hút thuốc hoàn toàn ngay lập tức',
    icon: Zap,
    bgColor: 'bg-red-100',
    iconColor: 'text-red-600',
    successRate: 65
  },
  {
    id: 2,
    name: 'Cai từ từ',
    description: 'Giảm dần số lượng thuốc lá mỗi ngày',
    icon: TrendingUp,
    bgColor: 'bg-blue-100',
    iconColor: 'text-blue-600',
    successRate: 78
  },
  {
    id: 3,
    name: 'Thay thế thói quen',
    description: 'Thay thế việc hút thuốc bằng hoạt động khác',
    icon: Brain,
    bgColor: 'bg-purple-100',
    iconColor: 'text-purple-600',
    successRate: 72
  },
  {
    id: 4,
    name: 'Hỗ trợ y tế',
    description: 'Kết hợp với thuốc hoặc liệu pháp thay thế',
    icon: Shield,
    bgColor: 'bg-green-100',
    iconColor: 'text-green-600',
    successRate: 85
  }
])
</script>

<style scoped>
.container {
  max-width: 1200px;
}

@keyframes bounce-slow {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-5px); }
}

.animate-bounce-slow {
  animation: bounce-slow 2s ease-in-out infinite;
}

@keyframes shimmer {
  0% { background-position: -200px 0; }
  100% { background-position: 200px 0; }
}

.shimmer {
  background: linear-gradient(90deg, transparent, rgba(255,255,255,0.4), transparent);
  background-size: 200px 100%;
  animation: shimmer 1.5s infinite;
}
</style>
