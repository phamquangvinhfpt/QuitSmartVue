<template>
  <section class="py-20 px-4 bg-gray-50">
    <div class="container mx-auto">
      <div 
        ref="headerSection"
        class="text-center mb-16"
      >
        <h2 class="text-4xl font-bold text-gray-900 mb-4">Lộ trình phục hồi sức khỏe</h2>
        <p class="text-xl text-gray-600 max-w-2xl mx-auto">
          Cơ thể bạn sẽ phục hồi như thế nào sau khi ngừng hút thuốc
        </p>
      </div>

      <div class="max-w-4xl mx-auto">
        <div class="relative">
          <!-- Timeline line -->
          <div 
            ref="timelineLine"
            class="absolute left-8 top-0 bottom-0 w-0.5 bg-green-300 opacity-100"
          ></div>
          
          <div class="space-y-8">
            <div 
              v-for="(milestone, index) in healthTimeline" 
              :key="milestone.time"
              :ref="(el) => { timelineItems[index] = el as HTMLElement }"
              class="relative flex items-start"
            >
              <!-- Timeline dot -->
              <div 
                :ref="(el) => { timelineDots[index] = el as HTMLElement }"
                class="absolute left-6 w-4 h-4 bg-green-500 rounded-full border-4 border-white shadow-lg opacity-100 scale-100"
              ></div>
              
              <!-- Content -->
              <div class="ml-16 bg-white rounded-lg shadow-md p-6 w-full transform hover:scale-105 transition-all duration-500 hover:shadow-xl">
                <div class="flex items-center mb-3">
                  <Clock class="h-5 w-5 text-green-600 mr-2 animate-spin" style="animation-duration: 4s;" />
                  <span class="font-bold text-green-800">{{ milestone.time }}</span>
                </div>
                <h4 class="text-lg font-semibold text-gray-900 mb-2">{{ milestone.title }}</h4>
                <p class="text-gray-600">{{ milestone.description }}</p>
                <div v-if="milestone.benefits" class="mt-3">
                  <ul class="space-y-1">
                    <li 
                      v-for="(benefit, benefitIndex) in milestone.benefits" 
                      :key="benefit"
                      :ref="(el) => { benefitItems[index * 10 + benefitIndex] = el as HTMLElement }"
                      class="text-sm text-gray-600 flex items-center opacity-0 transform translate-x-4"
                    >
                      <CheckCircle class="h-3 w-3 text-green-500 mr-2 animate-pulse" />
                      {{ benefit }}
                    </li>
                  </ul>
                </div>
              </div>
            </div>
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
import { Clock, CheckCircle } from 'lucide-vue-next'

// Register ScrollTrigger plugin
gsap.registerPlugin(ScrollTrigger)

// Animation refs
const headerSection = ref<HTMLElement>()
const timelineLine = ref<HTMLElement>()
const timelineItems = ref<(HTMLElement | null)[]>([])
const timelineDots = ref<(HTMLElement | null)[]>([])
const benefitItems = ref<(HTMLElement | null)[]>([])

// Animation functions
const animateTimeline = () => {
  if (!headerSection.value || !timelineLine.value || !timelineItems.value || !timelineDots.value || !benefitItems.value) {
    console.warn('Required elements not found for animation')
    return
  }

  // Set initial states but keep timeline line and dots visible
  gsap.set(headerSection.value, { opacity: 0, y: 50 })
  gsap.set(timelineItems.value.filter(el => el !== null), { opacity: 0, x: 50 })
  gsap.set(benefitItems.value.filter(el => el !== null), { opacity: 0, x: 20 })
  
  // Keep timeline line visible but scale from 0
  gsap.set(timelineLine.value, { scaleY: 0, transformOrigin: "top" })

  const tl = gsap.timeline()

  tl.to(headerSection.value, {
    opacity: 1,
    y: 0,
    duration: 0.8,
    ease: "power2.out"
  })
  .to(timelineLine.value, {
    scaleY: 1,
    duration: 1.5,
    ease: "power2.inOut"
  }, "-=0.4")
  .to(timelineItems.value.filter(el => el !== null), {
    opacity: 1,
    x: 0,
    duration: 0.6,
    stagger: 0.2,
    ease: "power2.out"
  }, "-=1.2")

  // Animate benefits with a delay
  gsap.delayedCall(1, () => {
    gsap.to(benefitItems.value.filter(el => el !== null), {
      opacity: 1,
      x: 0,
      duration: 0.4,
      stagger: 0.05,
      ease: "power2.out"
    })
  })
}

// Setup ScrollTrigger
const setupScrollAnimation = () => {
  ScrollTrigger.create({
    trigger: headerSection.value,
    start: "top 80%",
    onEnter: animateTimeline,
    once: true
  })
}

onMounted(async () => {
  await nextTick()
  setupScrollAnimation()
})

// Health recovery timeline
const healthTimeline = ref([
  {
    time: '20 phút',
    title: 'Nhịp tim và huyết áp bình thường',
    description: 'Nhịp tim và huyết áp giảm xuống mức bình thường, cải thiện tuần hoàn máu.',
    benefits: ['Giảm căng thẳng', 'Tim đập đều hơn']
  },
  {
    time: '12 giờ',
    title: 'Khí carbon monoxide giảm',
    description: 'Lượng carbon monoxide trong máu giảm xuống mức bình thường, oxy tăng.',
    benefits: ['Thở dễ hơn', 'Giảm đau đầu']
  },
  {
    time: '2 tuần',
    title: 'Tuần hoàn và phổi cải thiện',
    description: 'Tuần hoàn máu tốt hơn, chức năng phổi tăng lên đến 30%.',
    benefits: ['Ít ho hơn', 'Thể lực tăng', 'Da sáng hơn']
  },
  {
    time: '1 tháng',
    title: 'Giảm nguy cơ nhiễm trùng',
    description: 'Hệ miễn dịch mạnh hơn, giảm nguy cơ nhiễm trùng đường hô hấp.',
    benefits: ['Ít bị cảm lạnh', 'Vết thương lành nhanh hơn']
  },
  {
    time: '3 tháng',
    title: 'Chức năng phổi phục hồi',
    description: 'Chức năng phổi cải thiện đáng kể, giảm ho và khó thở.',
    benefits: ['Thở sâu hơn', 'Ít mệt mỏi', 'Giọng nói rõ hơn']
  },
  {
    time: '1 năm',
    title: 'Giảm 50% nguy cơ bệnh tim',
    description: 'Nguy cơ mắc bệnh tim mạch giảm một nửa so với khi còn hút thuốc.',
    benefits: ['Tim khỏe mạnh', 'Huyết áp ổn định', 'Cholesterol cải thiện']
  },
  {
    time: '5 năm',
    title: 'Giảm nguy cơ đột quỵ',
    description: 'Nguy cơ đột quỵ giảm xuống gần bằng người không hút thuốc.',
    benefits: ['Mạch máu khỏe', 'Trí nhớ tốt hơn']
  },
  {
    time: '10 năm',
    title: 'Giảm 50% nguy cơ ung thư phổi',
    description: 'Nguy cơ ung thư phổi giảm một nửa, các loại ung thư khác cũng giảm.',
    benefits: ['Phổi sạch hơn', 'Giảm nguy cơ ung thư']
  }
])
</script>

<style scoped>
.container {
  max-width: 1200px;
}

@keyframes glow {
  0%, 100% { box-shadow: 0 0 5px rgba(34, 197, 94, 0.5); }
  50% { box-shadow: 0 0 20px rgba(34, 197, 94, 0.8), 0 0 30px rgba(34, 197, 94, 0.6); }
}

.timeline-dot:hover {
  animation: glow 2s ease-in-out infinite;
}
</style>
