# QuitSmart Vue.js Landing Page

QuitSmart là một ứng dụng hỗ trợ cai thuốc lá thông minh và hiệu quả. Đây là trang landing page được xây dựng bằng Vue.js 3, TypeScript và Tailwind CSS.

## 🚀 Tính năng chính

- **Responsive Design**: Tối ưu cho mọi thiết bị từ mobile đến desktop
- **Modern UI/UX**: Giao diện hiện đại với hiệu ứng mượt mà
- **Rich Animations**: Sử dụng GSAP với ScrollTrigger cho animations mượt mà và performance cao
- **Vue 3 Composition API**: Sử dụng API mới nhất của Vue.js
- **TypeScript**: Type safety và developer experience tốt hơn
- **Tailwind CSS**: Utility-first CSS framework
- **Lucide Icons**: Bộ icon đẹp và nhất quán
- **ScrollTrigger**: Scroll-triggered animations tối ưu hiệu năng với GSAP

## 📋 Nội dung trang

1. **Hero Section**: Giới thiệu chính và CTA buttons
2. **Stats Section**: Thống kê người dùng và tỷ lệ thành công
3. **Features Section**: 6 tính năng chính của ứng dụng
4. **Health Information**: So sánh tác hại thuốc lá vs lợi ích cai thuốc
5. **Health Timeline**: Lộ trình phục hồi sức khỏe theo thời gian
6. **Quit Methods**: 4 phương pháp cai thuốc được hỗ trợ
7. **Success Stories**: Câu chuyện thành công của người dùng thực
8. **CTA Section**: Kêu gọi hành động cuối trang
9. **Footer**: Thông tin liên hệ và links

## 🛠️ Cài đặt và chạy

### Yêu cầu hệ thống
- Node.js 18+ hoặc Bun
- Git

### Cài đặt dependencies
```bash
# Sử dụng bun (recommended)
bun install

# Hoặc sử dụng npm
npm install

# Hoặc sử dụng yarn
yarn install
```

### Chạy development server
```bash
# Sử dụng bun
bun run dev

# Hoặc sử dụng npm
npm run dev

# Hoặc sử dụng yarn
yarn dev
```

Server sẽ chạy tại: http://localhost:5173

### Build production
```bash
bun run build
```

### Preview production build
```bash
bun run preview
```

## 📁 Cấu trúc thư mục

```
src/
├── components/          # Reusable components
│   ├── HealthInfo.vue   # Health information section
│   ├── HealthTimeline.vue # Health recovery timeline
│   └── QuitMethods.vue  # Quit methods section
├── views/               # Page components
│   └── LandingPage.vue  # Main landing page
├── router/              # Vue Router configuration
├── stores/              # Pinia stores (if needed)
├── assets/              # Static assets
└── main.ts              # Application entry point
```
## 🎨 Components

### HealthInfo.vue
Component hiển thị thông tin so sánh tác hại của thuốc lá và lợi ích khi cai thuốc:
- Tác hại: Ung thư, bệnh tim mạch, hệ hô hấp, tài chính, ngoại hình, gia đình
- Lợi ích: Sức khỏe, tiết kiệm, ngoại hình, gia đình, năng lượng, tự tin

### HealthTimeline.vue 
Component timeline hiển thị quá trình phục hồi sức khỏe:
- 20 phút: Nhịp tim và huyết áp bình thường
- 12 giờ: Khí carbon monoxide giảm
- 2 tuần: Tuần hoàn và phổi cải thiện
- 1 tháng: Giảm nguy cơ nhiễm trùng
- 3 tháng: Chức năng phổi phục hồi
- 1 năm: Giảm 50% nguy cơ bệnh tim
- 5 năm: Giảm nguy cơ đột quỵ
- 10 năm: Giảm 50% nguy cơ ung thư phổi

### QuitMethods.vue
Component hiển thị 4 phương pháp cai thuốc:
- Cai đột ngột (65% success rate)
- Cai từ từ (78% success rate)  
- Thay thế thói quen (72% success rate)
- Hỗ trợ y tế (85% success rate)

## 📱 Responsive Design

Website được tối ưu cho:
- **Mobile**: < 768px
- **Tablet**: 768px - 1024px  
- **Desktop**: > 1024px

Sử dụng Tailwind CSS breakpoints:
- `sm:` (640px+)
- `md:` (768px+)
- `lg:` (1024px+)
- `xl:` (1280px+)

## 🎯 Performance Optimizations

- **Lazy Loading**: Components được import động
- **Code Splitting**: Tự động tách code theo routes
- **Tree Shaking**: Loại bỏ code không sử dụng
- **Asset Optimization**: Images và assets được tối ưu
- **CSS Purging**: Tailwind CSS tự động xóa classes không dùng

## 🔧 Customization

### Thay đổi màu sắc
Chỉnh sửa trong Tailwind config hoặc trực tiếp trong components:
- Primary: `green-600`
- Secondary: `blue-600`, `purple-600`, etc.
- Text: `gray-900`, `gray-600`

### Thêm animations
Sử dụng Tailwind transition classes:
- `transition-colors`
- `transition-shadow`
- `hover:scale-105`

### Custom fonts
Thêm vào `src/assets/main.css`:
```css
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap');

body {
  font-family: 'Inter', sans-serif;
}
```

## 🚀 Deploy

### Vercel (Recommended)
```bash
# Install Vercel CLI
npm i -g vercel

# Deploy
vercel --prod
```

### Netlify
```bash
# Build
bun run build

# Upload dist/ folder to Netlify
```

### GitHub Pages
```bash
# Install gh-pages
npm install --save-dev gh-pages

# Add to package.json scripts
"deploy": "gh-pages -d dist"

# Deploy
npm run build && npm run deploy
```

## 📝 Notes

- File được tạo với Bun làm package manager
- Sử dụng Vite làm build tool
- TypeScript được cấu hình strict mode
- ESLint với Biome formatter
- Vue DevTools hỗ trợ debugging

## 🤝 Contributing

1. Fork repository
2. Tạo feature branch: `git checkout -b feature/new-feature`
3. Commit changes: `git commit -am 'Add new feature'`
4. Push branch: `git push origin feature/new-feature`
5. Tạo Pull Request

## 📄 License

MIT License - xem file LICENSE để biết thêm chi tiết.
