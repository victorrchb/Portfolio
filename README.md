# Victor Chabeau - Portfolio

A modern, responsive portfolio website showcasing my work as a Creative Front-End Developer. Built with Vue.js 3 and Vuetify 3, featuring smooth animations, mobile-first design, and an interactive dot matrix background.

## 🚀 Live Demo

[View Portfolio](https://your-portfolio-url.vercel.app)

## ✨ Features

- **Responsive Design**: Mobile-first approach with fullscreen sections on mobile devices
- **Interactive Background**: Animated floating dots with mouse interaction and performance optimization
- **Smooth Animations**: CSS transitions and Vue.js animations for enhanced user experience
- **Dark/Light Theme**: Toggle between themes with persistent user preferences
- **Accessibility**: ARIA labels, keyboard navigation, and screen reader support
- **Performance Optimized**: Lazy loading, optimized images, and efficient rendering
- **Modern UI/UX**: Clean, minimalist design with micro-interactions

## 🛠️ Tech Stack

### Frontend
- **Vue.js 3** - Progressive JavaScript framework
- **Vuetify 3** - Material Design component framework
- **TypeScript** - Type-safe JavaScript development
- **Vite** - Fast build tool and development server
- **SCSS** - Enhanced CSS with variables and mixins

### Development Tools
- **ESLint** - Code linting and quality assurance
- **Prettier** - Code formatting
- **Vue Router** - Single Page Application routing
- **Pinia** - State management
- **Auto-imports** - Automatic component and composable imports

### Deployment
- **Vercel** - Hosting and continuous deployment
- **GitHub** - Version control and collaboration

## 📱 Mobile Experience

The portfolio features a unique mobile experience with:
- **Fullscreen sections** that snap into place during scroll
- **Touch-optimized interactions** with haptic feedback alternatives
- **Performance-adaptive animations** that adjust based on device capabilities
- **Responsive typography** that scales perfectly across all screen sizes

## 🎨 Design System

- **Color Palette**: Dark theme with customizable light mode
- **Typography**: Roboto font family with responsive sizing
- **Spacing**: Consistent 8px grid system
- **Components**: Reusable Vue components with TypeScript support
- **Animations**: CSS transitions and Vue.js animations

## 🚀 Getting Started

### Prerequisites
- Node.js 18+ 
- npm, yarn, or pnpm

### Installation

1. Clone the repository
```bash
git clone https://github.com/victorrchb/portfolio.git
cd portfolio
```

2. Install dependencies
```bash
npm install
# or
yarn install
# or
pnpm install
```

3. Start development server
```bash
npm run dev
# or
yarn dev
# or
pnpm dev
```

4. Open [http://localhost:3000](http://localhost:3000) in your browser

### Build for Production

```bash
npm run build
# or
yarn build
# or
pnpm build
```

## 📁 Project Structure

```
src/
├── components/          # Reusable Vue components
│   ├── DottedParallax.vue  # Animated background component
│   ├── CursorManager.vue   # Custom cursor management
│   └── AppFooter.vue       # Footer component
├── layouts/            # Layout components
├── pages/              # Page components
├── plugins/            # Vue plugins configuration
├── router/             # Vue Router configuration
├── stores/             # Pinia stores
├── styles/             # Global styles and SCSS
└── assets/             # Static assets
```

## 🎯 Key Components

### DottedParallax
Interactive background with floating dots that respond to mouse movement and time-based animations. Optimized for performance across all devices.

### CursorManager
Custom cursor implementation with smooth animations and accessibility considerations.

### Responsive Design
Mobile-first approach with fullscreen sections and smooth scroll snap functionality.

## 🔧 Customization

### Theme Colors
Modify CSS custom properties in `src/styles/settings.scss`:

```scss
:root {
  --bg: #030301;
  --ink: #e8ecef;
  --panel: #232A2F;
}
```

### Animation Settings
Adjust animation parameters in `src/components/DottedParallax.vue`:

```typescript
const props = {
  gap: 24,        // Distance between dots
  dotSize: 2,     // Size of dots
  radius: 180,    // Mouse interaction radius
  strength: 28    // Animation strength
}
```

## 📈 Performance

- **Lighthouse Score**: 95+ across all metrics
- **Mobile Performance**: Optimized for 60fps animations
- **Bundle Size**: < 200KB gzipped
- **Load Time**: < 2s on 3G networks

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 📞 Contact

**Victor Chabeau**
- Email: victorchabeau03@gmail.com
- LinkedIn: [Victor Chabeau](https://www.linkedin.com/in/victor-chabeau-b5ab91232/)
- GitHub: [@victorrchb](https://github.com/victorrchb)
- Location: Paris, France

---

*Built with ❤️ using Vue.js 3, Vuetify 3, and modern web technologies*