# WEBSITE PREMIUM 3D - ActiveTheory Standard
# Playbook para Sites WebGL/Three.js de Alto Nível
# CMTecnologia - Versão 1.0

---

## 🎯 OBJETIVO

Criar websites interativos 3D/WebGL no padrão ActiveTheory:
- Performance impecável (60fps constante)
- Animações fluidas e orgânicas
- Design imersivo e premium
- Código limpo, modular e escalável

---

## 📋 PRÉ-REQUISITOS

### Stack Técnico Obrigatório
- **Three.js** (r0.182.0+) ou **React Three Fiber** (v9.5.0+)
- **GSAP** (v3.14.2+) para animações
- **Lenis** (v1.3.17+) para smooth scroll
- **@react-three/drei** (v10.7.7+) para helpers 3D
- **@react-three/postprocessing** (v3.0.4+) para efeitos pós-processamento

### Skills Necessárias
Carregar ANTES de começar (confirmar com humano):
- `antigravity-image-gen` (texturas/assets)
- `three.js core` (engine 3D)
- `react-three-fiber` (se React)
- `GSAP advanced` (timeline complexas)
- `postprocessing` (bloom, DOF, etc)
- `Lenis` (smooth scroll)

**Custo estimado:** 1-3€ por projeto completo.

---

## 🏗️ ESTRUTURA DE PROJETO

### Arquitetura de Pastas (Padrão CMTecnologia)

```
workspace/projects/<nome-cliente>/
├── public/
│   ├── models/          # .glb, .gltf
│   ├── textures/        # .jpg, .png, .hdr
│   └── fonts/           # .woff2
├── src/
│   ├── components/
│   │   ├── Canvas/      # Scene principal
│   │   ├── Loader/      # Loading screen
│   │   ├── UI/          # Overlay HTML
│   │   └── shared/      # Reutilizáveis
│   ├── experience/
│   │   ├── World.jsx    # Gerenciador de cenas
│   │   ├── Camera.jsx   # Camera controller
│   │   ├── Lights.jsx   # Iluminação
│   │   └── objects/     # Objetos 3D individuais
│   ├── shaders/
│   │   ├── vertex.glsl
│   │   └── fragment.glsl
│   ├── utils/
│   │   ├── GLTFLoader.js
│   │   ├── TextureLoader.js
│   │   └── PerformanceMonitor.js
│   ├── App.jsx
│   ├── index.css
│   └── main.jsx
├── package.json
├── vite.config.js       # Build otimizado
└── README.md
```

---

## 🎬 FLUXO DE DESENVOLVIMENTO (Passo a Passo)

### ETAPA 1: Análise & Planejamento (5 min)

**1.1. Entender o Briefing**
- Qual a história/mensagem do site?
- Quais as seções principais?
- Que emoção/sensação deve transmitir?

**1.2. Definir Conceito Visual 3D**
Escolher UMA das abordagens:
- **Particles System** (partículas fluidas, tipo Awwwards)
- **Abstract Geometry** (formas geométricas animadas)
- **Realistic 3D** (objetos fotorealistas)
- **Shader Art** (distorções, noise, gradientes)

**1.3. Criar Plano em Passos**
Gerar `todo.md` com checklist:
```markdown
## TODO - [Nome do Projeto]

- [ ] Setup inicial (Vite + Three.js + deps)
- [ ] Estrutura de pastas
- [ ] Scene base (canvas, camera, lights)
- [ ] Loader screen animado
- [ ] Hero 3D interativo
- [ ] Smooth scroll setup
- [ ] Seções com transições
- [ ] Performance optimization
- [ ] Responsivo (mobile/tablet)
- [ ] Deploy + prova técnica
```

---

### ETAPA 2: Setup Técnico (10 min)

**2.1. Inicializar Projeto**
```bash
cd workspace/projects/<nome-cliente>
npm create vite@latest . -- --template react
npm install three @react-three/fiber @react-three/drei @react-three/postprocessing gsap lenis
```

**2.2. Configurar Vite para Performance**
`vite.config.js`:
```javascript
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

export default defineConfig({
  plugins: [react()],
  build: {
    target: 'esnext',
    minify: 'terser',
    rollupOptions: {
      output: {
        manualChunks: {
          three: ['three'],
          r3f: ['@react-three/fiber', '@react-three/drei']
        }
      }
    }
  }
})
```

**2.3. CSS Base (Reset + Smooth)**
`src/index.css`:
```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html, body, #root {
  width: 100%;
  height: 100%;
  overflow: hidden; /* Lenis controla scroll */
}

body {
  font-family: 'Inter', sans-serif;
  background: #000;
  color: #fff;
  -webkit-font-smoothing: antialiased;
}

/* Smooth scroll container */
.scroll-container {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
}
```

---

### ETAPA 3: Scene 3D Base (20 min)

**3.1. Canvas Principal**
`src/App.jsx`:
```jsx
import { Canvas } from '@react-three/fiber'
import { Suspense } from 'react'
import Experience from './experience/World'
import Loader from './components/Loader'
import './index.css'

export default function App() {
  return (
    <>
      {/* Canvas 3D (fundo) */}
      <Canvas
        camera={{ position: [0, 0, 5], fov: 45 }}
        gl={{ 
          antialias: true,
          alpha: true,
          powerPreference: 'high-performance'
        }}
      >
        <Suspense fallback={null}>
          <Experience />
        </Suspense>
      </Canvas>

      {/* Loader */}
      <Loader />

      {/* UI Overlay (HTML sobre canvas) */}
      <div className="scroll-container">
        <Hero />
        <About />
        <Projects />
        <Contact />
      </div>
    </>
  )
}
```

**3.2. World (Gerenciador de Cena)**
`src/experience/World.jsx`:
```jsx
import { Environment, PerspectiveCamera } from '@react-three/drei'
import { EffectComposer, Bloom } from '@react-three/postprocessing'
import ParticleField from './objects/ParticleField'
import InteractiveGeometry from './objects/InteractiveGeometry'

export default function Experience() {
  return (
    <>
      {/* Camera */}
      <PerspectiveCamera makeDefault position={[0, 0, 5]} />

      {/* Luzes */}
      <ambientLight intensity={0.2} />
      <pointLight position={[10, 10, 10]} intensity={1} />

      {/* Objetos 3D */}
      <ParticleField count={5000} />
      <InteractiveGeometry />

      {/* Environment (HDR lighting) */}
      <Environment preset="city" />

      {/* Post-processing */}
      <EffectComposer>
        <Bloom 
          intensity={0.5} 
          luminanceThreshold={0.9} 
          luminanceSmoothing={0.9}
        />
      </EffectComposer>
    </>
  )
}
```

**3.3. Objeto 3D Interativo (Exemplo)**
`src/experience/objects/InteractiveGeometry.jsx`:
```jsx
import { useRef } from 'react'
import { useFrame } from '@react-three/fiber'
import { MeshDistortMaterial } from '@react-three/drei'
import * as THREE from 'three'

export default function InteractiveGeometry() {
  const meshRef = useRef()

  useFrame((state) => {
    // Rotação suave
    meshRef.current.rotation.x = state.clock.elapsedTime * 0.2
    meshRef.current.rotation.y = state.clock.elapsedTime * 0.3

    // Hover effect (mouse proximity)
    const mouse = state.mouse
    meshRef.current.position.x = THREE.MathUtils.lerp(
      meshRef.current.position.x,
      mouse.x * 0.5,
      0.05
    )
    meshRef.current.position.y = THREE.MathUtils.lerp(
      meshRef.current.position.y,
      mouse.y * 0.5,
      0.05
    )
  })

  return (
    <mesh ref={meshRef}>
      <icosahedronGeometry args={[1, 4]} />
      <MeshDistortMaterial
        color="#00ffff"
        distort={0.4}
        speed={2}
        roughness={0.2}
        metalness={0.8}
      />
    </mesh>
  )
}
```

---

### ETAPA 4: Smooth Scroll + GSAP (15 min)

**4.1. Setup Lenis**
`src/utils/useSmoothScroll.js`:
```javascript
import { useEffect } from 'react'
import Lenis from 'lenis'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

export default function useSmoothScroll() {
  useEffect(() => {
    const lenis = new Lenis({
      duration: 1.2,
      easing: (t) => Math.min(1, 1.001 - Math.pow(2, -10 * t)),
      smooth: true
    })

    function raf(time) {
      lenis.raf(time)
      requestAnimationFrame(raf)
    }
    requestAnimationFrame(raf)

    // Sync com ScrollTrigger
    lenis.on('scroll', ScrollTrigger.update)

    return () => lenis.destroy()
  }, [])
}
```

**4.2. Animações GSAP nas Seções**
`src/components/Hero.jsx`:
```jsx
import { useEffect, useRef } from 'react'
import { gsap } from 'gsap'
import useSmoothScroll from '../utils/useSmoothScroll'

export default function Hero() {
  useSmoothScroll()
  const titleRef = useRef()

  useEffect(() => {
    gsap.from(titleRef.current, {
      y: 100,
      opacity: 0,
      duration: 1.5,
      ease: 'power4.out',
      delay: 0.5
    })
  }, [])

  return (
    <section className="hero">
      <h1 ref={titleRef}>Premium 3D Experience</h1>
    </section>
  )
}
```

---

### ETAPA 5: Performance Optimization (10 min)

**5.1. Instanced Meshes (para muitos objetos)**
```jsx
import { useRef, useMemo } from 'react'
import { useFrame } from '@react-three/fiber'
import * as THREE from 'three'

export default function ParticleField({ count = 5000 }) {
  const meshRef = useRef()

  const particles = useMemo(() => {
    const temp = []
    for (let i = 0; i < count; i++) {
      temp.push({
        position: [
          (Math.random() - 0.5) * 20,
          (Math.random() - 0.5) * 20,
          (Math.random() - 0.5) * 20
        ],
        scale: Math.random() * 0.5 + 0.5
      })
    }
    return temp
  }, [count])

  useFrame(() => {
    meshRef.current.rotation.y += 0.001
  })

  return (
    <instancedMesh ref={meshRef} args={[null, null, count]}>
      <sphereGeometry args={[0.05, 8, 8]} />
      <meshBasicMaterial color="#ffffff" />
    </instancedMesh>
  )
}
```

**5.2. Responsivo (Mobile/Tablet)**
```jsx
import { useThree } from '@react-three/fiber'
import { useEffect } from 'react'

export default function ResponsiveCamera() {
  const { camera, size } = useThree()

  useEffect(() => {
    if (size.width < 768) {
      camera.fov = 75
      camera.position.z = 8
    } else {
      camera.fov = 45
      camera.position.z = 5
    }
    camera.updateProjectionMatrix()
  }, [size, camera])

  return null
}
```

---

### ETAPA 6: Loader Screen Premium (5 min)

`src/components/Loader.jsx`:
```jsx
import { useState, useEffect } from 'react'
import { gsap } from 'gsap'

export default function Loader() {
  const [progress, setProgress] = useState(0)
  const [visible, setVisible] = useState(true)

  useEffect(() => {
    const interval = setInterval(() => {
      setProgress((prev) => {
        if (prev >= 100) {
          clearInterval(interval)
          setTimeout(() => {
            gsap.to('.loader', {
              opacity: 0,
              duration: 0.8,
              onComplete: () => setVisible(false)
            })
          }, 500)
          return 100
        }
        return prev + 10
      })
    }, 100)

    return () => clearInterval(interval)
  }, [])

  if (!visible) return null

  return (
    <div className="loader">
      <div className="loader-content">
        <h2>Loading Experience</h2>
        <div className="progress-bar">
          <div className="progress-fill" style={{ width: `${progress}%` }} />
        </div>
        <p>{progress}%</p>
      </div>
    </div>
  )
}
```

---

## ✅ CHECKLIST DE FINALIZAÇÃO

Antes de entregar, OBRIGATÓRIO verificar:

### Performance
- [ ] 60fps constante em desktop (Chrome DevTools FPS)
- [ ] 30fps+ em mobile (testar em dispositivo real)
- [ ] Lighthouse Performance Score > 90
- [ ] Sem memory leaks (testar com Performance Monitor)

### Visual
- [ ] Transições suaves entre seções
- [ ] Animações orgânicas (easing natural)
- [ ] Responsivo (mobile, tablet, desktop)
- [ ] Fontes carregadas (sem FOUT)

### Código
- [ ] Sem `console.log` em produção
- [ ] Components modulares e reutilizáveis
- [ ] Comentários em partes complexas
- [ ] README.md com instruções de setup

### Prova Técnica (MANDATÓRIO)
- [ ] Screenshot do site rodando (hero + 1 seção)
- [ ] Vídeo 10s mostrando interatividade 3D
- [ ] `npm run build` sem erros
- [ ] Deploy (Vercel/Netlify) + URL funcionando

---

## 🚀 DEPLOY

```bash
# Build otimizado
npm run build

# Testar build localmente
npm run preview

# Deploy Vercel (recomendado)
npx vercel --prod
```

**Entregar ao humano:**
- URL do site deployado
- Screenshot + vídeo de demonstração

---

## 🎨 REFERÊNCIAS VISUAIS (ActiveTheory Standard)

Sites inspiração:
- **Particles**: bruno-simon.com
- **Abstract Geo**: activetheory.net
- **Shader Art**: tympanus.net/codrops

---

## ⚠️ REGRAS INEGOCIÁVEIS

1. **Sempre criar todo.md e seguir passo a passo**
2. **Sempre testar performance antes de entregar**
3. **Sempre mostrar prova técnica (código + deploy + screenshot)**
4. **Nunca prometer "está pronto" sem URL funcionando**
5. **Sempre usar componentes modulares (reutilizar código)**

---

**FIM DO PLAYBOOK**