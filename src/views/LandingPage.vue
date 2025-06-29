<template>
  <div class="min-h-screen bg-gradient-to-b from-green-50 to-white">
    <!-- Header -->
    <header class="border-b glass sticky top-0 z-50">
      <div class="container mx-auto px-4 sm:px-6 lg:px-8 py-3 sm:py-4 flex justify-between items-center">
        <div class="flex items-center space-x-2 animate-float-slow">
          <Heart class="h-6 w-6 sm:h-8 sm:w-8 text-green-600 animate-pulse-glow" />
          <span class="text-lg sm:text-2xl font-bold text-gradient-green">QuitSmart</span>
        </div>
        <div class="flex items-center space-x-2 sm:space-x-4">
          <button class="px-3 py-2 sm:px-4 sm:py-2 text-sm sm:text-base text-gray-600 hover:text-gray-900 transition-all duration-300 hover:scale-105 hover:cursor-pointer">
            Đăng nhập
          </button>
          <button class="px-4 py-2 sm:px-6 sm:py-2 text-sm sm:text-base bg-green-600 text-white rounded-lg hover:bg-green-700 transition-all duration-300 hover:scale-105 hover:shadow-lg hover-glow hover:cursor-pointer">
            Đăng ký ngay
          </button>
        </div>
      </div>
    </header>

    <!-- Hero Section -->
    <section class="py-12 sm:py-16 lg:py-20 px-4 sm:px-6 lg:px-8">
      <div class="container mx-auto text-center">
        <div 
          ref="heroBadge"
          class="inline-block mb-4 px-3 py-2 sm:px-4 sm:py-2 bg-green-100 text-green-800 rounded-full text-xs sm:text-sm font-medium"
        >
          Ứng dụng cai thuốc lá thông minh
        </div>
        <h1 
          ref="heroTitle"
          class="text-3xl sm:text-4xl lg:text-5xl font-bold text-gray-900 mb-4 sm:mb-6 leading-tight"
        >
          Hành trình cai thuốc lá
          <span class="text-green-600 block">thành công của bạn</span>
        </h1>
        <p 
          ref="heroSubtitle"
          class="text-base sm:text-lg lg:text-xl text-gray-600 mb-6 sm:mb-8 max-w-2xl mx-auto px-4"
        >
          Theo dõi tiến trình, nhận động viên và đạt được mục tiêu cai thuốc lá với sự hỗ trợ của công nghệ thông minh
        </p>
        <div 
          ref="heroButtons"
          class="flex flex-col sm:flex-row gap-4 sm:gap-0 sm:space-x-4 items-center justify-center px-4"
        >
          <button class="w-full sm:w-auto px-6 py-3 sm:px-8 sm:py-4 bg-green-600 text-white rounded-lg text-base sm:text-lg font-semibold hover:bg-green-700 transition-all duration-300 hover:scale-105 hover:shadow-lg hover:cursor-pointer">
            Bắt đầu ngay hôm nay
          </button>
          <button class="w-full sm:w-auto px-6 py-3 sm:px-8 sm:py-4 border border-gray-300 text-gray-700 rounded-lg text-base sm:text-lg font-semibold hover:bg-gray-50 transition-all duration-300 hover:scale-105 hover:shadow-lg hover:cursor-pointer">
            Tìm hiểu thêm
          </button>
        </div>

        <!-- Stats -->
        <div 
          ref="statsSection"
          class="grid grid-cols-1 sm:grid-cols-3 gap-6 sm:gap-8 mt-12 sm:mt-16 max-w-4xl mx-auto px-4"
        >
          <div class="text-center transform hover:scale-105 transition-transform duration-300 p-4 bg-white rounded-lg shadow-sm">
            <div 
              ref="statUsers"
              class="text-2xl sm:text-3xl font-bold text-green-600"
            >0+</div>
            <div class="text-sm sm:text-base text-gray-600">Người dùng thành công</div>
          </div>
          <div class="text-center transform hover:scale-105 transition-transform duration-300 p-4 bg-white rounded-lg shadow-sm">
            <div 
              ref="statSuccess"
              class="text-2xl sm:text-3xl font-bold text-green-600"
            >0%</div>
            <div class="text-sm sm:text-base text-gray-600">Tỷ lệ thành công</div>
          </div>
          <div class="text-center transform hover:scale-105 transition-transform duration-300 p-4 bg-white rounded-lg shadow-sm">
            <div 
              ref="statDays"
              class="text-2xl sm:text-3xl font-bold text-green-600"
            >0 ngày</div>
            <div class="text-sm sm:text-base text-gray-600">Thời gian trung bình</div>
          </div>
        </div>
      </div>
    </section>

    <!-- Features Section -->
    <section id="features" class="py-12 sm:py-16 lg:py-20 px-4 sm:px-6 lg:px-8 bg-gray-50">
      <div class="container mx-auto">
        <div 
          ref="featuresHeader"
          class="text-center mb-12 sm:mb-16"
        >
          <h2 class="text-3xl sm:text-4xl font-bold text-gray-900 mb-4">Tính năng nổi bật</h2>
          <p class="text-base sm:text-lg lg:text-xl text-gray-600 max-w-2xl mx-auto px-4">
            Hệ thống hỗ trợ toàn diện giúp bạn cai thuốc lá hiệu quả
          </p>
        </div>

        <div 
          ref="featuresGrid"
          class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6 sm:gap-8"
        >
          <div 
            v-for="(feature, index) in features" 
            :key="feature.id"
            :ref="(el) => { featureCards[index] = el as HTMLElement }"
            class="bg-white rounded-lg shadow-lg hover:shadow-xl transition-all duration-500 p-6 transform hover:scale-105 hover:-translate-y-2"
          >
            <component :is="feature.icon" :class="`h-10 w-10 sm:h-12 sm:w-12 ${feature.color} mb-4 transform transition-transform duration-300 hover:rotate-12`" />
            <h3 class="text-lg sm:text-xl font-bold text-gray-900 mb-2">{{ feature.title }}</h3>
            <p class="text-sm sm:text-base text-gray-600 mb-4">{{ feature.description }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Health Information Section -->
    <HealthInfo />

    <!-- Health Recovery Timeline Section -->
    <HealthTimeline />

    <!-- Quit Methods Section -->
    <QuitMethods />

    <!-- Success Stories Section -->
    <section class="py-12 sm:py-16 lg:py-20 px-4 sm:px-6 lg:px-8">
      <div class="container mx-auto">
        <div 
          ref="storiesHeader"
          class="text-center mb-12 sm:mb-16"
        >
          <h2 class="text-3xl sm:text-4xl font-bold text-gray-900 mb-4">Câu chuyện thành công</h2>
          <p class="text-base sm:text-lg lg:text-xl text-gray-600 max-w-2xl mx-auto px-4">
            Những người dùng thực tế đã thành công cai thuốc với QuitSmart
          </p>
        </div>

        <div 
          ref="storiesGrid"
          class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6 sm:gap-8"
        >
          <div 
            v-for="(story, index) in successStories" 
            :key="story.id"
            :ref="(el) => { storyCards[index] = el as HTMLElement }"
            class="bg-white rounded-lg shadow-lg p-6 text-center transform hover:scale-105 transition-all duration-500 hover:shadow-xl"
          >
            <div class="w-12 h-12 sm:w-16 sm:h-16 bg-gray-200 rounded-full mx-auto mb-4 flex items-center justify-center transform transition-transform duration-300 hover:rotate-12">
              <User class="h-6 w-6 sm:h-8 sm:w-8 text-gray-500" />
            </div>
            <h4 class="text-base sm:text-lg font-bold text-gray-900 mb-2">{{ story.name }}</h4>
            <div class="text-sm text-gray-600 mb-4">
              <span class="font-semibold text-green-600">{{ story.smokeFreedays }} ngày</span> không hút thuốc
            </div>
            <p class="text-sm sm:text-base text-gray-600 italic mb-4 line-clamp-3">"{{ story.quote }}"</p>
            <div class="text-xs sm:text-sm text-gray-500">
              Tiết kiệm: <span class="font-semibold text-green-600">{{ story.moneySaved.toLocaleString() }}đ</span>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- CTA Section -->
    <section class="py-12 sm:py-16 lg:py-20 px-4 sm:px-6 lg:px-8 animate-gradient">
      <div class="container mx-auto text-center">
        <h2 
          ref="ctaTitle"
          class="text-3xl sm:text-4xl font-bold text-white mb-4"
        >
          Sẵn sàng bắt đầu hành trình cai thuốc?
        </h2>
        <p 
          ref="ctaSubtitle"
          class="text-base sm:text-lg lg:text-xl text-green-100 mb-6 sm:mb-8 max-w-2xl mx-auto px-4"
        >
          Hàng ngàn người đã thành công với QuitSmart. Bạn cũng có thể làm được!
        </p>
        <div 
          ref="ctaButtons"
          class="flex flex-col sm:flex-row gap-4 sm:gap-0 sm:space-x-4 items-center justify-center px-4"
        >
          <button class="w-full sm:w-auto px-6 py-3 sm:px-8 sm:py-4 bg-white text-green-600 rounded-lg text-base sm:text-lg font-semibold hover:bg-gray-100 transition-all duration-300 hover:scale-110 hover:shadow-xl transform animate-float hover:cursor-pointer">
            Đăng ký miễn phí
          </button>
          <button class="w-full sm:w-auto px-6 py-3 sm:px-8 sm:py-4 border-2 border-white text-white rounded-lg text-base sm:text-lg font-semibold hover:bg-white hover:text-green-600 transition-all duration-300 hover:scale-110 hover:shadow-xl transform animate-float-slow hover:cursor-pointer">
            Xem demo
          </button>
        </div>
      </div>
    </section>

    <!-- Footer -->
    <footer class="bg-gray-900 text-white py-8 sm:py-12 px-4 sm:px-6 lg:px-8">
      <div class="container mx-auto">
        <!-- Logo section - separate row on mobile -->
        <div class="mb-8 text-center sm:text-left">
          <div class="flex items-center justify-center sm:justify-start space-x-2 mb-4">
            <Heart class="h-5 w-5 sm:h-6 sm:w-6 text-green-500" />
            <span class="text-lg sm:text-xl font-bold">QuitSmart</span>
          </div>
          <p class="text-sm sm:text-base text-gray-400 max-w-md mx-auto sm:mx-0">Ứng dụng hỗ trợ cai thuốc lá thông minh và hiệu quả</p>
        </div>
        
        <!-- Links grid - 3 columns on mobile -->
        <div class="grid grid-cols-3 gap-4 sm:gap-6 lg:gap-8 mb-8">
          <!-- Product links -->
          <div>
            <h4 class="text-sm sm:text-base font-semibold mb-3 sm:mb-4 text-white">Sản phẩm</h4>
            <ul class="space-y-2 text-xs sm:text-sm lg:text-base text-gray-400">
              <li><a href="#features" class="hover:text-white transition-colors block py-1">Tính năng</a></li>
              <li><a href="/pricing" class="hover:text-white transition-colors block py-1">Bảng giá</a></li>
              <li><a href="/demo" class="hover:text-white transition-colors block py-1">Demo</a></li>
            </ul>
          </div>
          
          <!-- Support links -->
          <div>
            <h4 class="text-sm sm:text-base font-semibold mb-3 sm:mb-4 text-white">Hỗ trợ</h4>
            <ul class="space-y-2 text-xs sm:text-sm lg:text-base text-gray-400">
              <li><a href="/help" class="hover:text-white transition-colors block py-1">Trợ giúp</a></li>
              <li><a href="/contact" class="hover:text-white transition-colors block py-1">Liên hệ</a></li>
              <li><a href="/faq" class="hover:text-white transition-colors block py-1">FAQ</a></li>
            </ul>
          </div>
          
          <!-- Legal links -->
          <div>
            <h4 class="text-sm sm:text-base font-semibold mb-3 sm:mb-4 text-white">Pháp lý</h4>
            <ul class="space-y-2 text-xs sm:text-sm lg:text-base text-gray-400">
              <li><a href="/privacy" class="hover:text-white transition-colors block py-1">Bảo mật</a></li>
              <li><a href="/terms" class="hover:text-white transition-colors block py-1">Điều khoản</a></li>
            </ul>
          </div>
        </div>
        
        <!-- Copyright section -->
        <div class="border-t border-gray-800 pt-6 sm:pt-8 text-center">
          <p class="text-sm sm:text-base text-gray-400">&copy; 2025 QuitSmart. Tất cả quyền được bảo lưu.</p>
        </div>
      </div>
    </footer>
  </div>
</template>

<script setup lang="ts">
import { ref, reactive, onMounted, nextTick } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'
import { 
  Heart, 
  Users, 
  Target, 
  Calendar, 
  TrendingUp, 
  Award, 
  MessageCircle, 
  User,
} from 'lucide-vue-next'

// Import components
import HealthInfo from '../components/landing-page/HealthInfo.vue'
import HealthTimeline from '../components/landing-page/HealthTimeline.vue'
import QuitMethods from '../components/landing-page/QuitMethods.vue'

// Register ScrollTrigger plugin
gsap.registerPlugin(ScrollTrigger)

// Animation refs
const heroBadge = ref<HTMLElement>()
const heroTitle = ref<HTMLElement>()
const heroSubtitle = ref<HTMLElement>()
const heroButtons = ref<HTMLElement>()
const statsSection = ref<HTMLElement>()
const statUsers = ref<HTMLElement>()
const statSuccess = ref<HTMLElement>()
const statDays = ref<HTMLElement>()
const featuresHeader = ref<HTMLElement>()
const featuresGrid = ref<HTMLElement>()
const featureCards = ref<(HTMLElement | null)[]>([])
const storiesHeader = ref<HTMLElement>()
const storiesGrid = ref<HTMLElement>()
const storyCards = ref<(HTMLElement | null)[]>([])
const ctaTitle = ref<HTMLElement>()
const ctaSubtitle = ref<HTMLElement>()
const ctaButtons = ref<HTMLElement>()

// GSAP timeline for animations
let heroTimeline: gsap.core.Timeline
let statsTimeline: gsap.core.Timeline

// Stats data
const stats = reactive({
  users: 10000,
  successRate: 85,
  avgDays: 30
})

// Features data
const features = ref([
  {
    id: 1,
    icon: Users,
    color: 'text-green-600',
    title: 'Hồ sơ cá nhân',
    description: 'Quản lý thông tin cá nhân và mục tiêu cai thuốc'
  },
  {
    id: 2,
    icon: Target,
    color: 'text-blue-600',
    title: 'Lập kế hoạch cai thuốc',
    description: 'Tạo kế hoạch cai thuốc phù hợp với bản thân'
  },
  {
    id: 3,
    icon: Calendar,
    color: 'text-purple-600',
    title: 'Nhật ký hàng ngày',
    description: 'Theo dõi tiến trình cai thuốc mỗi ngày'
  },
  {
    id: 4,
    icon: TrendingUp,
    color: 'text-orange-600',
    title: 'Thống kê tiến trình',
    description: 'Xem báo cáo chi tiết về quá trình cai thuốc'
  },
  {
    id: 5,
    icon: Award,
    color: 'text-yellow-600',
    title: 'Hệ thống huy hiệu',
    description: 'Nhận huy hiệu khi đạt được các mốc quan trọng'
  },
  {
    id: 6,
    icon: MessageCircle,
    color: 'text-pink-600',
    title: 'Thông điệp động viên',
    description: 'Nhận động lực tích cực mỗi ngày'
  }
])

// Animation functions
const animateHeroSection = () => {
  if (!heroBadge.value || !heroTitle.value || !heroSubtitle.value || !heroButtons.value) {
    console.warn('Required elements not found for animation')
    return
  }

  // Set initial opacity to 0 before animating
  gsap.set([heroBadge.value, heroTitle.value, heroSubtitle.value, heroButtons.value], { opacity: 0 })

  heroTimeline = gsap.timeline()
  
  heroTimeline
    .to(heroBadge.value, {
      opacity: 1,
      y: 0,
      duration: 0.8,
      ease: "power2.out"
    })
    .to(heroTitle.value, {
      opacity: 1,
      y: 0,
      duration: 1,
      ease: "power2.out"
    }, "-=0.6")
    .to(heroSubtitle.value, {
      opacity: 1,
      y: 0,
      duration: 0.8,
      ease: "power2.out"
    }, "-=0.8")
    .to(heroButtons.value, {
      opacity: 1,
      y: 0,
      scale: 1,
      duration: 0.8,
      ease: "back.out(1.7)"
    }, "-=0.6")
}

const animateStats = () => {
  if (!statsSection.value) {
    console.warn('Required elements not found for animation')
    return
  }

  statsTimeline = gsap.timeline()

  // Animate stats container first
  statsTimeline.from(statsSection.value, {
    opacity: 0,
    y: 50,
    duration: 1,
    ease: "power2.out"
  })

  // Animate counter numbers
  const animateCounter = (element: HTMLElement | undefined, endValue: number, suffix: string = '') => {
    if (!element) return
    
    const obj = { value: 0 }
    gsap.to(obj, {
      value: endValue,
      duration: 2,
      ease: "power2.out",
      onUpdate: () => {
        const currentValue = Math.round(obj.value)
        if (suffix === '+') {
          element.textContent = currentValue.toLocaleString() + suffix
        } else if (suffix === '%') {
          element.textContent = currentValue + suffix
        } else {
          element.textContent = currentValue + ' ' + suffix
        }
      }
    })
  }

  // Start counters after container animation
  statsTimeline.call(() => {
    animateCounter(statUsers.value, stats.users, '+')
    animateCounter(statSuccess.value, stats.successRate, '%')
    animateCounter(statDays.value, stats.avgDays, 'ngày')
  }, [], 0.5)
}

const animateFeatures = () => {
  if (!featuresHeader.value || !featuresGrid.value) {
    console.warn('Required elements not found for animation')
    return
  }

  // Set initial opacity to 0 before animating
  gsap.set([featuresHeader.value, featuresGrid.value], { opacity: 0 })
  gsap.set(featureCards.value.filter(el => el !== null), { opacity: 0 })

  const tl = gsap.timeline()
  
  tl.to(featuresHeader.value, {
    opacity: 1,
    y: 0,
    duration: 0.8,
    ease: "power2.out"
  })
  .to(featuresGrid.value, {
    opacity: 1,
    y: 0,
    duration: 0.8,
    ease: "power2.out"
  }, "-=0.4")
  .to(featureCards.value.filter(el => el !== null), {
    opacity: 1,
    y: 0,
    scale: 1,
    duration: 0.6,
    stagger: 0.15,
    ease: "back.out(1.7)"
  }, "-=0.4")
}

const animateStories = () => {
  if (!storiesHeader.value || !storiesGrid.value) {
    console.warn('Required elements not found for animation')
    return
  }

  // Set initial opacity to 0 before animating
  gsap.set([storiesHeader.value, storiesGrid.value], { opacity: 0 })
  gsap.set(storyCards.value.filter(el => el !== null), { opacity: 0 })

  const tl = gsap.timeline()
  
  tl.to(storiesHeader.value, {
    opacity: 1,
    y: 0,
    duration: 0.8,
    ease: "power2.out"
  })
  .to(storiesGrid.value, {
    opacity: 1,
    y: 0,
    duration: 0.8,
    ease: "power2.out"
  }, "-=0.4")
  .to(storyCards.value.filter(el => el !== null), {
    opacity: 1,
    y: 0,
    scale: 1,
    duration: 0.8,
    stagger: 0.2,
    ease: "back.out(1.7)"
  }, "-=0.4")
}

const animateCTA = () => {
  if (!ctaTitle.value || !ctaSubtitle.value || !ctaButtons.value) {
    console.warn('Required elements not found for animation')
    return
  }

  // Set initial opacity to 0 before animating
  gsap.set([ctaTitle.value, ctaSubtitle.value, ctaButtons.value], { opacity: 0 })

  const tl = gsap.timeline()
  
  tl.to(ctaTitle.value, {
    opacity: 1,
    y: 0,
    duration: 0.8,
    ease: "power2.out"
  })
  .to(ctaSubtitle.value, {
    opacity: 1,
    y: 0,
    duration: 0.8,
    ease: "power2.out"
  }, "-=0.6")
  .to(ctaButtons.value, {
    opacity: 1,
    y: 0,
    scale: 1,
    duration: 0.8,
    ease: "back.out(1.7)"
  }, "-=0.4")
}

// Setup ScrollTrigger animations
const setupScrollAnimations = () => {
  // Stats section animation
  ScrollTrigger.create({
    trigger: statsSection.value,
    start: "top 80%",
    onEnter: animateStats,
    once: true
  })

  // Features section animation  
  ScrollTrigger.create({
    trigger: featuresHeader.value,
    start: "top 80%",
    onEnter: animateFeatures,
    once: true
  })

  // Stories section animation
  ScrollTrigger.create({
    trigger: storiesHeader.value,
    start: "top 80%", 
    onEnter: animateStories,
    once: true
  })

  // CTA section animation
  ScrollTrigger.create({
    trigger: ctaTitle.value,
    start: "top 80%",
    onEnter: animateCTA,
    once: true
  })
}

onMounted(async () => {
  await nextTick()
  
  // Start hero animations immediately
  animateHeroSection()
  
  // Setup scroll-triggered animations with a small delay
  setTimeout(() => {
    setupScrollAnimations()
  }, 500)
})

// Success stories
const successStories = ref([
  {
    id: 1,
    name: 'Anh Minh, 35 tuổi',
    smokeFreedays: 180,
    quote: 'QuitSmart giúp tôi theo dõi tiến trình rất rõ ràng. Thấy số tiền tiết kiệm tăng lên mỗi ngày là động lực lớn!',
    moneySaved: 5400000
  },
  {
    id: 2,
    name: 'Chị Lan, 28 tuổi',
    smokeFreedays: 365,
    quote: 'Hệ thống huy hiệu rất thú vị, giúp tôi có động lực tiếp tục. Giờ tôi đã 1 năm không hút thuốc!',
    moneySaved: 10950000
  },
  {
    id: 3,
    name: 'Anh Tuấn, 42 tuổi',
    smokeFreedays: 90,
    quote: 'Nhật ký hàng ngày giúp tôi nhận ra những trigger và cách kiểm soát cơn thèm thuốc hiệu quả.',
    moneySaved: 2700000
  }
])
</script>

<style scoped>
.container {
  max-width: 1200px;
}
</style>
