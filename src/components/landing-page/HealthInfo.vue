<template>
  <section class="py-20 px-4">
    <div class="container mx-auto">
      <div 
        ref="headerSection"
        class="text-center mb-16"
      >
        <h2 class="text-4xl font-bold text-gray-900 mb-4">Thông tin hữu ích</h2>
        <p class="text-xl text-gray-600 max-w-2xl mx-auto">
          Hiểu rõ tác hại của thuốc lá và lợi ích của việc cai thuốc
        </p>
      </div>

      <div 
        ref="cardsSection"
        class="grid grid-cols-1 lg:grid-cols-2 gap-12"
      >
        <!-- Harms of Smoking -->
        <div class="bg-red-50 border border-red-200 rounded-lg p-8 transform hover:scale-105 transition-all duration-500 hover:shadow-xl">
          <div class="flex items-center mb-6">
            <AlertTriangle class="h-6 w-6 text-red-600 mr-2 animate-pulse" />
            <h3 class="text-2xl font-bold text-red-800">Tác hại của thuốc lá</h3>
          </div>
          <div class="space-y-4">
            <div 
              v-for="(harm, index) in smokingHarms" 
              :key="harm.title"
              :ref="(el) => { harmItems[index] = el as HTMLElement }"
              class="flex items-start space-x-3"
            >
              <div class="w-2 h-2 bg-red-500 rounded-full mt-2 flex-shrink-0 animate-pulse"></div>
              <div>
                <h4 class="font-semibold text-red-800">{{ harm.title }}</h4>
                <p class="text-sm text-red-700">{{ harm.description }}</p>
              </div>
            </div>
          </div>
        </div>

        <!-- Benefits of Quitting -->
        <div class="bg-green-50 border border-green-200 rounded-lg p-8 transform hover:scale-105 transition-all duration-500 hover:shadow-xl">
          <div class="flex items-center mb-6">
            <Heart class="h-6 w-6 text-green-600 mr-2 animate-bounce" />
            <h3 class="text-2xl font-bold text-green-800">Lợi ích khi cai thuốc</h3>
          </div>
          <div class="space-y-4">
            <div 
              v-for="(benefit, index) in quittingBenefits" 
              :key="benefit.title"
              :ref="(el) => { benefitItems[index] = el as HTMLElement }"
              class="flex items-start space-x-3"
            >
              <div class="w-2 h-2 bg-green-500 rounded-full mt-2 flex-shrink-0 animate-pulse"></div>
              <div>
                <h4 class="font-semibold text-green-800">{{ benefit.title }}</h4>
                <p class="text-sm text-green-700">{{ benefit.description }}</p>
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
import { AlertTriangle, Heart } from 'lucide-vue-next'

// Register ScrollTrigger plugin
gsap.registerPlugin(ScrollTrigger)

// Animation refs
const headerSection = ref<HTMLElement>()
const cardsSection = ref<HTMLElement>()
const harmItems = ref<(HTMLElement | null)[]>([])
const benefitItems = ref<(HTMLElement | null)[]>([])

// Animation functions
const animateSection = () => {
  if (!headerSection.value || !cardsSection.value) {
    console.warn('Required elements not found for animation')
    return
  }

  // Set initial opacity to 0 before animating
  gsap.set([headerSection.value, cardsSection.value], { opacity: 0 })
  gsap.set(harmItems.value.filter(el => el !== null), { opacity: 0 })
  gsap.set(benefitItems.value.filter(el => el !== null), { opacity: 0 })

  const tl = gsap.timeline()

  tl.to(headerSection.value, {
    opacity: 1,
    y: 0,
    duration: 0.8,
    ease: "power2.out"
  })
  .to(cardsSection.value, {
    opacity: 1,
    y: 0,
    duration: 0.8,
    ease: "power2.out"
  }, "-=0.4")
  .to(harmItems.value.filter(el => el !== null), {
    opacity: 1,
    x: 0,
    duration: 0.6,
    stagger: 0.1,
    ease: "power2.out"
  }, "-=0.4")
  .to(benefitItems.value.filter(el => el !== null), {
    opacity: 1,
    x: 0,
    duration: 0.6,
    stagger: 0.1,
    ease: "power2.out"
  }, "-=0.8")
}

// Setup ScrollTrigger
const setupScrollAnimation = () => {
  ScrollTrigger.create({
    trigger: headerSection.value,
    start: "top 80%",
    onEnter: animateSection,
    once: true
  })
}

onMounted(async () => {
  await nextTick()
  setupScrollAnimation()
})

// Smoking harms data
const smokingHarms = ref([
  {
    title: 'Ung thư',
    description: 'Tăng nguy cơ ung thư phổi, họng, bàng quang và nhiều cơ quan khác lên 10-20 lần'
  },
  {
    title: 'Bệnh tim mạch',
    description: 'Gây tắc nghẽn động mạch, tăng nguy cơ đột quỵ và nhồi máu cơ tim lên 2-4 lần'
  },
  {
    title: 'Hệ hô hấp',
    description: 'Viêm phổi mãn tính, hen suyễn, giảm 50% chức năng phổi so với người không hút'
  },
  {
    title: 'Tài chính',
    description: 'Chi phí mua thuốc lá và điều trị bệnh tật trung bình 50-100 triệu/năm'
  },
  {
    title: 'Ngoại hình',
    description: 'Da xấu, răng vàng, mùi hôi, lão hóa sớm 5-10 năm so với tuổi thực'
  },
  {
    title: 'Gia đình',
    description: 'Khói thuốc thụ động gây hại cho vợ/chồng và con cái, tăng nguy cơ bệnh tật'
  }
])

// Quitting benefits data
const quittingBenefits = ref([
  {
    title: 'Sức khỏe cải thiện',
    description: 'Hệ hô hấp, tim mạch phục hồi nhanh chóng, giảm 90% nguy cơ ung thư sau 10 năm'
  },
  {
    title: 'Tiết kiệm tiền',
    description: 'Tiết kiệm 20-50 triệu đồng mỗi năm từ việc không mua thuốc lá'
  },
  {
    title: 'Ngoại hình',
    description: 'Da sáng khỏe, răng trắng, hết mùi thuốc lá, trông trẻ trung hơn'
  },
  {
    title: 'Gia đình',
    description: 'Bảo vệ người thân khỏi khói thuốc thụ động, làm gương tốt cho con cái'
  },
  {
    title: 'Năng lượng',
    description: 'Tăng thể lực, giảm mệt mỏi, cải thiện khả năng tập trung và làm việc'
  },
  {
    title: 'Tự tin',
    description: 'Tăng lòng tự trọng, tự hào về thành tích cai thuốc thành công'
  }
])
</script>

<style scoped>
.container {
  max-width: 1200px;
}

@keyframes float {
  0%, 100% { transform: translateY(0px); }
  50% { transform: translateY(-10px); }
}

.animate-float {
  animation: float 3s ease-in-out infinite;
}
</style>
