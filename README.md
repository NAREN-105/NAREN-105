<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Narendaran M | Full-Stack Engineer</title>
    
    <!-- Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800;900&family=JetBrains+Mono:wght@400;500;600;700&display=swap" rel="stylesheet">
    
    <!-- Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
    
    <!-- Three.js -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    
    <style>
        :root {
            --primary: #38BDF8;
            --primary-dim: #0EA5E9;
            --primary-glow: rgba(56, 189, 248, 0.3);
            --bg-deep: #020617;
            --bg-dark: #0F172A;
            --bg-card: rgba(15, 23, 42, 0.6);
            --bg-card-hover: rgba(30, 41, 59, 0.8);
            --text-primary: #F1F5F9;
            --text-secondary: #94A3B8;
            --text-muted: #64748B;
            --accent-orange: #FB923C;
            --accent-green: #22C55E;
            --accent-purple: #A78BFA;
            --border: rgba(56, 189, 248, 0.15);
            --border-hover: rgba(56, 189, 248, 0.4);
            --glass-blur: 20px;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        html {
            scroll-behavior: smooth;
        }

        body {
            font-family: 'Inter', sans-serif;
            background: var(--bg-deep);
            color: var(--text-primary);
            overflow-x: hidden;
            cursor: default;
        }

        /* Custom Scrollbar */
        ::-webkit-scrollbar {
            width: 6px;
        }
        ::-webkit-scrollbar-track {
            background: var(--bg-deep);
        }
        ::-webkit-scrollbar-thumb {
            background: var(--primary-dim);
            border-radius: 3px;
        }

        /* ═══════════════════════════════════ */
        /* LOADER */
        /* ═══════════════════════════════════ */
        #loader {
            position: fixed;
            inset: 0;
            background: var(--bg-deep);
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            z-index: 10000;
            transition: opacity 0.8s ease, visibility 0.8s ease;
        }
        #loader.hidden {
            opacity: 0;
            visibility: hidden;
        }
        .loader-3d {
            width: 120px;
            height: 120px;
            perspective: 600px;
        }
        .loader-cube {
            width: 100%;
            height: 100%;
            position: relative;
            transform-style: preserve-3d;
            animation: loaderSpin 2s infinite ease-in-out;
        }
        .loader-cube .face {
            position: absolute;
            width: 120px;
            height: 120px;
            border: 2px solid var(--primary);
            background: rgba(56, 189, 248, 0.05);
            backdrop-filter: blur(5px);
        }
        .loader-cube .face:nth-child(1) { transform: rotateY(0deg) translateZ(60px); }
        .loader-cube .face:nth-child(2) { transform: rotateY(90deg) translateZ(60px); }
        .loader-cube .face:nth-child(3) { transform: rotateY(180deg) translateZ(60px); }
        .loader-cube .face:nth-child(4) { transform: rotateY(-90deg) translateZ(60px); }
        .loader-cube .face:nth-child(5) { transform: rotateX(90deg) translateZ(60px); }
        .loader-cube .face:nth-child(6) { transform: rotateX(-90deg) translateZ(60px); }
        @keyframes loaderSpin {
            0% { transform: rotateX(0deg) rotateY(0deg); }
            50% { transform: rotateX(180deg) rotateY(180deg); }
            100% { transform: rotateX(360deg) rotateY(360deg); }
        }
        .loader-text {
            margin-top: 30px;
            font-family: 'JetBrains Mono', monospace;
            font-size: 14px;
            color: var(--primary);
            letter-spacing: 3px;
        }
        .loader-progress {
            width: 200px;
            height: 2px;
            background: rgba(56, 189, 248, 0.1);
            margin-top: 15px;
            border-radius: 1px;
            overflow: hidden;
        }
        .loader-progress-bar {
            height: 100%;
            width: 0%;
            background: linear-gradient(90deg, var(--primary), var(--accent-purple));
            border-radius: 1px;
            transition: width 0.3s ease;
        }

        /* ═══════════════════════════════════ */
        /* CURSOR */
        /* ═══════════════════════════════════ */
        .cursor-dot {
            width: 8px;
            height: 8px;
            background: var(--primary);
            border-radius: 50%;
            position: fixed;
            pointer-events: none;
            z-index: 9999;
            transition: transform 0.1s ease;
            mix-blend-mode: difference;
        }
        .cursor-ring {
            width: 40px;
            height: 40px;
            border: 1.5px solid var(--primary);
            border-radius: 50%;
            position: fixed;
            pointer-events: none;
            z-index: 9998;
            transition: all 0.15s ease-out;
            opacity: 0.5;
        }
        .cursor-ring.hover {
            transform: scale(1.5);
            border-color: var(--accent-orange);
            opacity: 0.8;
        }

        /* ═══════════════════════════════════ */
        /* 3D CANVAS */
        /* ═══════════════════════════════════ */
        #bg-canvas {
            position: fixed;
            inset: 0;
            z-index: 0;
        }

        /* ═══════════════════════════════════ */
        /* NAVIGATION */
        /* ═══════════════════════════════════ */
        .nav {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            z-index: 1000;
            padding: 20px 50px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            transition: all 0.4s ease;
        }
        .nav.scrolled {
            background: rgba(2, 6, 23, 0.85);
            backdrop-filter: blur(20px);
            border-bottom: 1px solid var(--border);
            padding: 15px 50px;
        }
        .nav-logo {
            font-family: 'JetBrains Mono', monospace;
            font-size: 20px;
            font-weight: 700;
            color: var(--primary);
            text-decoration: none;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        .nav-logo .logo-bracket {
            color: var(--text-muted);
        }
        .nav-links {
            display: flex;
            gap: 35px;
            list-style: none;
        }
        .nav-links a {
            color: var(--text-secondary);
            text-decoration: none;
            font-size: 14px;
            font-weight: 500;
            letter-spacing: 1px;
            text-transform: uppercase;
            position: relative;
            transition: color 0.3s ease;
        }
        .nav-links a::after {
            content: '';
            position: absolute;
            bottom: -5px;
            left: 0;
            width: 0;
            height: 2px;
            background: var(--primary);
            transition: width 0.3s ease;
        }
        .nav-links a:hover {
            color: var(--primary);
        }
        .nav-links a:hover::after {
            width: 100%;
        }
        .nav-cta {
            padding: 10px 25px;
            background: transparent;
            border: 1px solid var(--primary);
            color: var(--primary);
            font-family: 'Inter', sans-serif;
            font-size: 13px;
            font-weight: 600;
            letter-spacing: 1px;
            text-transform: uppercase;
            cursor: pointer;
            transition: all 0.3s ease;
            text-decoration: none;
        }
        .nav-cta:hover {
            background: var(--primary);
            color: var(--bg-deep);
            box-shadow: 0 0 30px var(--primary-glow);
        }

        /* Mobile Menu */
        .menu-toggle {
            display: none;
            flex-direction: column;
            gap: 6px;
            cursor: pointer;
            padding: 5px;
        }
        .menu-toggle span {
            width: 25px;
            height: 2px;
            background: var(--primary);
            transition: all 0.3s ease;
        }
        .menu-toggle.active span:nth-child(1) {
            transform: rotate(45deg) translate(5px, 5px);
        }
        .menu-toggle.active span:nth-child(2) {
            opacity: 0;
        }
        .menu-toggle.active span:nth-child(3) {
            transform: rotate(-45deg) translate(6px, -6px);
        }

        /* ═══════════════════════════════════ */
        /* SECTIONS BASE */
        /* ═══════════════════════════════════ */
        section {
            position: relative;
            z-index: 1;
        }
        .section-container {
            max-width: 1300px;
            margin: 0 auto;
            padding: 0 50px;
        }
        .section-label {
            font-family: 'JetBrains Mono', monospace;
            font-size: 13px;
            color: var(--primary);
            letter-spacing: 4px;
            text-transform: uppercase;
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            gap: 15px;
        }
        .section-label::before {
            content: '';
            width: 40px;
            height: 1px;
            background: var(--primary);
        }
        .section-title {
            font-size: clamp(36px, 5vw, 56px);
            font-weight: 800;
            line-height: 1.1;
            margin-bottom: 20px;
        }
        .section-title .highlight {
            background: linear-gradient(135deg, var(--primary), var(--accent-purple));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }
        .section-divider {
            width: 100%;
            height: 1px;
            background: linear-gradient(90deg, transparent, var(--border), transparent);
            margin: 0;
        }

        /* ═══════════════════════════════════ */
        /* HERO SECTION */
        /* ═══════════════════════════════════ */
        .hero {
            min-height: 100vh;
            display: flex;
            align-items: center;
            position: relative;
            overflow: hidden;
        }
        .hero-content {
            position: relative;
            z-index: 2;
        }
        .hero-tag {
            display: inline-flex;
            align-items: center;
            gap: 10px;
            padding: 8px 20px;
            background: var(--bg-card);
            border: 1px solid var(--border);
            border-radius: 50px;
            font-family: 'JetBrains Mono', monospace;
            font-size: 12px;
            color: var(--accent-green);
            margin-bottom: 30px;
            backdrop-filter: blur(10px);
        }
        .hero-tag .pulse {
            width: 8px;
            height: 8px;
            background: var(--accent-green);
            border-radius: 50%;
            animation: pulse 2s infinite;
        }
        @keyframes pulse {
            0%, 100% { opacity: 1; transform: scale(1); }
            50% { opacity: 0.5; transform: scale(1.5); }
        }
        .hero-title {
            font-size: clamp(48px, 7vw, 90px);
            font-weight: 900;
            line-height: 1;
            margin-bottom: 25px;
        }
        .hero-title .line {
            display: block;
        }
        .hero-title .line-2 {
            background: linear-gradient(135deg, var(--primary) 0%, var(--accent-purple) 50%, var(--accent-orange) 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            background-size: 200% 200%;
            animation: gradientShift 4s ease infinite;
        }
        @keyframes gradientShift {
            0%, 100% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
        }
        .hero-subtitle {
            font-size: 18px;
            color: var(--text-secondary);
            max-width: 600px;
            line-height: 1.7;
            margin-bottom: 40px;
        }
        .hero-buttons {
            display: flex;
            gap: 20px;
            flex-wrap: wrap;
        }
        .btn-primary {
            padding: 16px 40px;
            background: linear-gradient(135deg, var(--primary), var(--primary-dim));
            color: var(--bg-deep);
            font-family: 'Inter', sans-serif;
            font-size: 14px;
            font-weight: 700;
            letter-spacing: 1px;
            text-transform: uppercase;
            border: none;
            cursor: pointer;
            position: relative;
            overflow: hidden;
            transition: all 0.4s ease;
            text-decoration: none;
            display: inline-flex;
            align-items: center;
            gap: 10px;
        }
        .btn-primary::before {
            content: '';
            position: absolute;
            inset: 0;
            background: linear-gradient(135deg, transparent, rgba(255,255,255,0.2), transparent);
            transform: translateX(-100%);
            transition: transform 0.6s ease;
        }
        .btn-primary:hover::before {
            transform: translateX(100%);
        }
        .btn-primary:hover {
            box-shadow: 0 0 40px var(--primary-glow), 0 0 80px rgba(56, 189, 248, 0.15);
            transform: translateY(-2px);
        }
        .btn-secondary {
            padding: 16px 40px;
            background: transparent;
            color: var(--text-primary);
            font-family: 'Inter', sans-serif;
            font-size: 14px;
            font-weight: 600;
            letter-spacing: 1px;
            text-transform: uppercase;
            border: 1px solid var(--border);
            cursor: pointer;
            transition: all 0.4s ease;
            text-decoration: none;
            display: inline-flex;
            align-items: center;
            gap: 10px;
        }
        .btn-secondary:hover {
            border-color: var(--primary);
            color: var(--primary);
            box-shadow: 0 0 20px rgba(56, 189, 248, 0.1);
        }

        /* Hero 3D Floating Element */
        .hero-3d-container {
            position: absolute;
            right: 5%;
            top: 50%;
            transform: translateY(-50%);
            width: 450px;
            height: 450px;
            perspective: 1000px;
            z-index: 1;
        }
        .hero-3d-object {
            width: 100%;
            height: 100%;
            position: relative;
            transform-style: preserve-3d;
            animation: float3D 8s ease-in-out infinite;
        }
        @keyframes float3D {
            0%, 100% { transform: rotateX(15deg) rotateY(-15deg) translateY(0); }
            25% { transform: rotateX(20deg) rotateY(-10deg) translateY(-20px); }
            50% { transform: rotateX(15deg) rotateY(-20deg) translateY(0); }
            75% { transform: rotateX(10deg) rotateY(-15deg) translateY(-15px); }
        }
        .glass-card-3d {
            position: absolute;
            background: var(--bg-card);
            backdrop-filter: blur(20px);
            border: 1px solid var(--border);
            border-radius: 16px;
            padding: 25px;
            transform-style: preserve-3d;
        }
        .glass-card-3d.card-1 {
            width: 280px;
            top: 0;
            left: 50%;
            transform: translateX(-50%) rotateY(10deg);
            animation: cardFloat1 6s ease-in-out infinite;
        }
        .glass-card-3d.card-2 {
            width: 240px;
            bottom: 40px;
            left: 0;
            transform: rotateY(-15deg) rotateX(10deg);
            animation: cardFloat2 7s ease-in-out infinite;
        }
        .glass-card-3d.card-3 {
            width: 200px;
            bottom: 60px;
            right: 0;
            transform: rotateY(20deg) rotateX(-5deg);
            animation: cardFloat3 5s ease-in-out infinite;
        }
        @keyframes cardFloat1 {
            0%, 100% { transform: translateX(-50%) rotateY(10deg) translateY(0); }
            50% { transform: translateX(-50%) rotateY(10deg) translateY(-15px); }
        }
        @keyframes cardFloat2 {
            0%, 100% { transform: rotateY(-15deg) rotateX(10deg) translateY(0); }
            50% { transform: rotateY(-15deg) rotateX(10deg) translateY(-20px); }
        }
        @keyframes cardFloat3 {
            0%, 100% { transform: rotateY(20deg) rotateX(-5deg) translateY(0); }
            50% { transform: rotateY(20deg) rotateX(-5deg) translateY(-12px); }
        }
        .card-header {
            display: flex;
            align-items: center;
            gap: 10px;
            margin-bottom: 15px;
        }
        .card-dot {
            width: 10px;
            height: 10px;
            border-radius: 50%;
        }
        .card-dot.red { background: #EF4444; }
        .card-dot.yellow { background: #F59E0B; }
        .card-dot.green { background: #22C55E; }
        .card-code {
            font-family: 'JetBrains Mono', monospace;
            font-size: 12px;
            line-height: 1.8;
            color: var(--text-secondary);
        }
        .card-code .keyword { color: var(--accent-purple); }
        .card-code .function { color: var(--primary); }
        .card-code .string { color: var(--accent-green); }
        .card-code .comment { color: var(--text-muted); }
        .card-code .number { color: var(--accent-orange); }

        .card-stats {
            display: flex;
            flex-direction: column;
            gap: 12px;
        }
        .stat-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .stat-label {
            font-size: 12px;
            color: var(--text-muted);
        }
        .stat-value {
            font-family: 'JetBrains Mono', monospace;
            font-size: 14px;
            font-weight: 600;
            color: var(--primary);
        }
        .stat-bar {
            width: 100%;
            height: 4px;
            background: rgba(56, 189, 248, 0.1);
            border-radius: 2px;
            overflow: hidden;
            margin-top: 5px;
        }
        .stat-bar-fill {
            height: 100%;
            border-radius: 2px;
            background: linear-gradient(90deg, var(--primary), var(--accent-purple));
            transition: width 1.5s ease;
        }

        .card-tech {
            display: flex;
            flex-wrap: wrap;
            gap: 8px;
        }
        .tech-tag {
            padding: 6px 12px;
            background: rgba(56, 189, 248, 0.1);
            border: 1px solid rgba(56, 189, 248, 0.2);
            border-radius: 6px;
            font-family: 'JetBrains Mono', monospace;
            font-size: 11px;
            color: var(--primary);
        }

        /* Scroll Indicator */
        .scroll-indicator {
            position: absolute;
            bottom: 40px;
            left: 50%;
            transform: translateX(-50%);
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 10px;
        }
        .scroll-indicator span {
            font-size: 11px;
            letter-spacing: 3px;
            text-transform: uppercase;
            color: var(--text-muted);
        }
        .scroll-line {
            width: 1px;
            height: 60px;
            background: linear-gradient(to bottom, var(--primary), transparent);
            animation: scrollPulse 2s ease-in-out infinite;
        }
        @keyframes scrollPulse {
            0%, 100% { opacity: 1; height: 60px; }
            50% { opacity: 0.3; height: 40px; }
        }

        /* ═══════════════════════════════════ */
        /* ABOUT SECTION */
        /* ═══════════════════════════════════ */
        .about {
            padding: 120px 0;
        }
        .about-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 80px;
            align-items: center;
        }
        .about-image-container {
            position: relative;
            perspective: 1000px;
        }
        .about-image-wrapper {
            position: relative;
            border-radius: 20px;
            overflow: hidden;
            transform: rotateY(-5deg) rotateX(5deg);
            transition: transform 0.6s ease;
        }
        .about-image-wrapper:hover {
            transform: rotateY(0) rotateX(0);
        }
        .about-image-wrapper img {
            width: 100%;
            height: 500px;
            object-fit: cover;
        }
        .about-image-overlay {
            position: absolute;
            inset: 0;
            background: linear-gradient(135deg, rgba(56, 189, 248, 0.2), rgba(167, 139, 250, 0.2));
            mix-blend-mode: overlay;
        }
        .about-image-border {
            position: absolute;
            inset: -2px;
            border: 2px solid var(--border);
            border-radius: 22px;
            z-index: -1;
        }
        .about-floating-card {
            position: absolute;
            bottom: -30px;
            right: -30px;
            background: var(--bg-card);
            backdrop-filter: blur(20px);
            border: 1px solid var(--border);
            border-radius: 16px;
            padding: 25px;
            animation: floatCard 4s ease-in-out infinite;
        }
        @keyframes floatCard {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-10px); }
        }
        .about-floating-card .years {
            font-size: 48px;
            font-weight: 900;
            color: var(--primary);
            line-height: 1;
        }
        .about-floating-card .years-text {
            font-size: 13px;
            color: var(--text-secondary);
            margin-top: 5px;
        }
        .about-text p {
            font-size: 16px;
            line-height: 1.8;
            color: var(--text-secondary);
            margin-bottom: 25px;
        }
        .about-quote {
            padding: 25px 30px;
            background: var(--bg-card);
            border-left: 3px solid var(--primary);
            border-radius: 0 12px 12px 0;
            margin: 30px 0;
            font-style: italic;
            color: var(--text-secondary);
        }
        .about-highlights {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
            margin-top: 30px;
        }
        .highlight-item {
            display: flex;
            align-items: center;
            gap: 12px;
            padding: 15px;
            background: var(--bg-card);
            border: 1px solid var(--border);
            border-radius: 12px;
            transition: all 0.3s ease;
        }
        .highlight-item:hover {
            border-color: var(--border-hover);
            transform: translateX(5px);
        }
        .highlight-icon {
            width: 40px;
            height: 40px;
            display: flex;
            align-items: center;
            justify-content: center;
            background: rgba(56, 189, 248, 0.1);
            border-radius: 10px;
            color: var(--primary);
            font-size: 16px;
        }
        .highlight-text {
            font-size: 13px;
            color: var(--text-secondary);
        }
        .highlight-text strong {
            color: var(--text-primary);
            display: block;
            margin-bottom: 2px;
        }

        /* ═══════════════════════════════════ */
        /* SKILLS SECTION */
        /* ═══════════════════════════════════ */
        .skills {
            padding: 120px 0;
        }
        .skills-grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 25px;
            margin-top: 60px;
        }
        .skill-category {
            background: var(--bg-card);
            border: 1px solid var(--border);
            border-radius: 20px;
            padding: 35px 30px;
            transition: all 0.4s ease;
            position: relative;
            overflow: hidden;
        }
        .skill-category::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 3px;
            background: linear-gradient(90deg, var(--primary), var(--accent-purple));
            transform: scaleX(0);
            transform-origin: left;
            transition: transform 0.4s ease;
        }
        .skill-category:hover::before {
            transform: scaleX(1);
        }
        .skill-category:hover {
            border-color: var(--border-hover);
            transform: translateY(-10px);
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
        }
        .skill-icon {
            width: 60px;
            height: 60px;
            display: flex;
            align-items: center;
            justify-content: center;
            background: rgba(56, 189, 248, 0.1);
            border-radius: 15px;
            font-size: 24px;
            color: var(--primary);
            margin-bottom: 25px;
        }
        .skill-category h3 {
            font-size: 18px;
            font-weight: 700;
            margin-bottom: 20px;
        }
        .skill-list {
            display: flex;
            flex-direction: column;
            gap: 12px;
        }
        .skill-item {
            display: flex;
            align-items: center;
            justify-content: space-between;
            font-size: 14px;
            color: var(--text-secondary);
        }
        .skill-item span:last-child {
            font-family: 'JetBrains Mono', monospace;
            color: var(--primary);
            font-size: 12px;
        }

        /* ═══════════════════════════════════ */
        /* PROJECTS SECTION */
        /* ═══════════════════════════════════ */
        .projects {
            padding: 120px 0;
        }
        .projects-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 30px;
            margin-top: 60px;
        }
        .project-card {
            background: var(--bg-card);
            border: 1px solid var(--border);
            border-radius: 20px;
            overflow: hidden;
            transition: all 0.5s ease;
            position: relative;
        }
        .project-card:hover {
            border-color: var(--border-hover);
            transform: translateY(-8px);
            box-shadow: 0 25px 50px rgba(0, 0, 0, 0.4);
        }
        .project-card.featured {
            grid-column: span 2;
        }
        .project-image {
            height: 250px;
            overflow: hidden;
            position: relative;
        }
        .project-card.featured .project-image {
            height: 350px;
        }
        .project-image img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            transition: transform 0.6s ease;
        }
        .project-card:hover .project-image img {
            transform: scale(1.05);
        }
        .project-image-overlay {
            position: absolute;
            inset: 0;
            background: linear-gradient(to top, var(--bg-deep), transparent);
        }
        .project-featured-badge {
            position: absolute;
            top: 20px;
            left: 20px;
            padding: 6px 15px;
            background: linear-gradient(135deg, var(--accent-orange), #F97316);
            color: white;
            font-size: 11px;
            font-weight: 700;
            letter-spacing: 1px;
            text-transform: uppercase;
            border-radius: 6px;
        }
        .project-content {
            padding: 30px;
        }
        .project-title {
            font-size: 22px;
            font-weight: 700;
            margin-bottom: 12px;
            display: flex;
            align-items: center;
            gap: 12px;
        }
        .project-title i {
            font-size: 18px;
            color: var(--primary);
        }
        .project-desc {
            font-size: 14px;
            color: var(--text-secondary);
            line-height: 1.7;
            margin-bottom: 20px;
        }
        .project-tech {
            display: flex;
            flex-wrap: wrap;
            gap: 8px;
            margin-bottom: 25px;
        }
        .project-tech span {
            padding: 5px 12px;
            background: rgba(56, 189, 248, 0.08);
            border: 1px solid rgba(56, 189, 248, 0.15);
            border-radius: 6px;
            font-family: 'JetBrains Mono', monospace;
            font-size: 11px;
            color: var(--primary);
        }
        .project-links {
            display: flex;
            gap: 15px;
        }
        .project-link {
            display: inline-flex;
            align-items: center;
            gap: 8px;
            padding: 10px 20px;
            font-size: 13px;
            font-weight: 600;
            border-radius: 8px;
            text-decoration: none;
            transition: all 0.3s ease;
        }
        .project-link.primary {
            background: var(--primary);
            color: var(--bg-deep);
        }
        .project-link.primary:hover {
            box-shadow: 0 0 20px var(--primary-glow);
        }
        .project-link.secondary {
            background: transparent;
            border: 1px solid var(--border);
            color: var(--text-secondary);
        }
        .project-link.secondary:hover {
            border-color: var(--primary);
            color: var(--primary);
        }

        /* ═══════════════════════════════════ */
        /* LEETCODE SECTION */
        /* ═══════════════════════════════════ */
        .leetcode {
            padding: 120px 0;
        }
        .leetcode-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 40px;
            margin-top: 60px;
        }
        .leetcode-card {
            background: var(--bg-card);
            border: 1px solid var(--border);
            border-radius: 20px;
            padding: 40px;
            text-align: center;
            transition: all 0.4s ease;
        }
        .leetcode-card:hover {
            border-color: var(--border-hover);
            transform: translateY(-5px);
        }
        .leetcode-card img {
            max-width: 100%;
            border-radius: 12px;
        }
        .leetcode-stats-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 20px;
            margin-top: 40px;
        }
        .leetcode-stat {
            background: var(--bg-card);
            border: 1px solid var(--border);
            border-radius: 16px;
            padding: 30px 20px;
            text-align: center;
            transition: all 0.3s ease;
        }
        .leetcode-stat:hover {
            border-color: var(--border-hover);
            transform: scale(1.05);
        }
        .leetcode-stat .number {
            font-size: 36px;
            font-weight: 900;
            margin-bottom: 5px;
        }
        .leetcode-stat.easy .number { color: var(--accent-green); }
        .leetcode-stat.medium .number { color: var(--accent-orange); }
        .leetcode-stat.hard .number { color: #EF4444; }
        .leetcode-stat .label {
            font-size: 13px;
            color: var(--text-muted);
            text-transform: uppercase;
            letter-spacing: 1px;
        }
        .leetcode-cta {
            text-align: center;
            margin-top: 40px;
        }

        /* ═══════════════════════════════════ */
        /* CONTACT SECTION */
        /* ═══════════════════════════════════ */
        .contact {
            padding: 120px 0;
        }
        .contact-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 80px;
            margin-top: 60px;
        }
        .contact-info {
            display: flex;
            flex-direction: column;
            gap: 30px;
        }
        .contact-item {
            display: flex;
            align-items: flex-start;
            gap: 20px;
            padding: 25px;
            background: var(--bg-card);
            border: 1px solid var(--border);
            border-radius: 16px;
            transition: all 0.3s ease;
        }
        .contact-item:hover {
            border-color: var(--border-hover);
            transform: translateX(10px);
        }
        .contact-icon {
            width: 50px;
            height: 50px;
            display: flex;
            align-items: center;
            justify-content: center;
            background: rgba(56, 189, 248, 0.1);
            border-radius: 12px;
            color: var(--primary);
            font-size: 20px;
            flex-shrink: 0;
        }
        .contact-item h4 {
            font-size: 16px;
            margin-bottom: 5px;
        }
        .contact-item p {
            font-size: 14px;
            color: var(--text-secondary);
        }
        .contact-item a {
            color: var(--primary);
            text-decoration: none;
        }
        .contact-form {
            display: flex;
            flex-direction: column;
            gap: 20px;
        }
        .form-group {
            position: relative;
        }
        .form-group input,
        .form-group textarea {
            width: 100%;
            padding: 18px 20px;
            background: var(--bg-card);
            border: 1px solid var(--border);
            border-radius: 12px;
            color: var(--text-primary);
            font-family: 'Inter', sans-serif;
            font-size: 15px;
            transition: all 0.3s ease;
            outline: none;
        }
        .form-group input:focus,
        .form-group textarea:focus {
            border-color: var(--primary);
            box-shadow: 0 0 20px rgba(56, 189, 248, 0.1);
        }
        .form-group input::placeholder,
        .form-group textarea::placeholder {
            color: var(--text-muted);
        }
        .form-group textarea {
            min-height: 150px;
            resize: vertical;
        }
        .form-submit {
            padding: 18px 40px;
            background: linear-gradient(135deg, var(--primary), var(--primary-dim));
            color: var(--bg-deep);
            font-family: 'Inter', sans-serif;
            font-size: 15px;
            font-weight: 700;
            letter-spacing: 1px;
            text-transform: uppercase;
            border: none;
            cursor: pointer;
            transition: all 0.4s ease;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
        }
        .form-submit:hover {
            box-shadow: 0 0 40px var(--primary-glow);
            transform: translateY(-3px);
        }

        /* ═══════════════════════════════════ */
        /* FOOTER */
        /* ═══════════════════════════════════ */
        .footer {
            padding: 60px 0;
            border-top: 1px solid var(--border);
        }
        .footer-content {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .footer-text {
            font-size: 14px;
            color: var(--text-muted);
        }
        .footer-text span {
            color: var(--primary);
        }
        .footer-socials {
            display: flex;
            gap: 15px;
        }
        .footer-social {
            width: 45px;
            height: 45px;
            display: flex;
            align-items: center;
            justify-content: center;
            background: var(--bg-card);
            border: 1px solid var(--border);
            border-radius: 12px;
            color: var(--text-secondary);
            text-decoration: none;
            transition: all 0.3s ease;
        }
        .footer-social:hover {
            border-color: var(--primary);
            color: var(--primary);
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
        }

        /* ═══════════════════════════════════ */
        /* ANIMATIONS */
        /* ═══════════════════════════════════ */
        .reveal {
            opacity: 0;
            transform: translateY(40px);
            transition: all 0.8s cubic-bezier(0.16, 1, 0.3, 1);
        }
        .reveal.active {
            opacity: 1;
            transform: translateY(0);
        }
        .reveal-left {
            opacity: 0;
            transform: translateX(-40px);
            transition: all 0.8s cubic-bezier(0.16, 1, 0.3, 1);
        }
        .reveal-left.active {
            opacity: 1;
            transform: translateX(0);
        }
        .reveal-right {
            opacity: 0;
            transform: translateX(40px);
            transition: all 0.8s cubic-bezier(0.16, 1, 0.3, 1);
        }
        .reveal-right.active {
            opacity: 1;
            transform: translateX(0);
        }
        .reveal-scale {
            opacity: 0;
            transform: scale(0.9);
            transition: all 0.8s cubic-bezier(0.16, 1, 0.3, 1);
        }
        .reveal-scale.active {
            opacity: 1;
            transform: scale(1);
        }

        /* ═══════════════════════════════════ */
        /* RESPONSIVE */
        /* ═══════════════════════════════════ */
        @media (max-width: 1024px) {
            .hero-3d-container {
                display: none;
            }
            .skills-grid {
                grid-template-columns: repeat(2, 1fr);
            }
        }
        @media (max-width: 768px) {
            .nav {
                padding: 15px 25px;
            }
            .nav-links {
                display: none;
            }
            .menu-toggle {
                display: flex;
            }
            .section-container {
                padding: 0 25px;
            }
            .hero-title {
                font-size: clamp(36px, 8vw, 60px);
            }
            .about-grid,
            .contact-grid,
            .leetcode-container {
                grid-template-columns: 1fr;
                gap: 40px;
            }
            .skills-grid {
                grid-template-columns: 1fr;
            }
            .projects-grid {
                grid-template-columns: 1fr;
            }
            .project-card.featured {
                grid-column: span 1;
            }
            .leetcode-stats-grid {
                grid-template-columns: repeat(3, 1fr);
                gap: 10px;
            }
            .about-highlights {
                grid-template-columns: 1fr;
            }
            .footer-content {
                flex-direction: column;
                gap: 25px;
                text-align: center;
            }
            .cursor-dot, .cursor-ring {
                display: none;
            }
        }
    </style>
</head>
<body>

    <!-- Loader -->
    <div id="loader">
        <div class="loader-3d">
            <div class="loader-cube">
                <div class="face"></div>
                <div class="face"></div>
                <div class="face"></div>
                <div class="face"></div>
                <div class="face"></div>
                <div class="face"></div>
            </div>
        </div>
        <div class="loader-text">INITIALIZING</div>
        <div class="loader-progress">
            <div class="loader-progress-bar" id="progressBar"></div>
        </div>
    </div>

    <!-- Custom Cursor -->
    <div class="cursor-dot" id="cursorDot"></div>
    <div class="cursor-ring" id="cursorRing"></div>

    <!-- 3D Background Canvas -->
    <canvas id="bg-canvas"></canvas>

    <!-- Navigation -->
    <nav class="nav" id="nav">
        <a href="#" class="nav-logo">
            <span class="logo-bracket">{</span>NAREN<span class="logo-bracket">}</span>
        </a>
        <ul class="nav-links">
            <li><a href="#about">About</a></li>
            <li><a href="#skills">Skills</a></li>
            <li><a href="#projects">Projects</a></li>
            <li><a href="#leetcode">LeetCode</a></li>
            <li><a href="#contact">Contact</a></li>
        </ul>
        <a href="#contact" class="nav-cta">Let's Talk</a>
        <div class="menu-toggle" id="menuToggle">
            <span></span>
            <span></span>
            <span></span>
        </div>
    </nav>

    <!-- Hero Section -->
    <section class="hero" id="hero">
        <div class="section-container">
            <div class="hero-content">
                <div class="hero-tag reveal">
                    <span class="pulse"></span>
                    Available for opportunities
                </div>
                <h1 class="hero-title">
                    <span class="line reveal">Narendaran</span>
                    <span class="line line-2 reveal">Full-Stack Engineer</span>
                </h1>
                <p class="hero-subtitle reveal">
                    I deeply understand a problem before writing a single line — then ship something that holds up in production. Architecting resilient systems with clean code.
                </p>
                <div class="hero-buttons reveal">
                    <a href="#projects" class="btn-primary">
                        <i class="fas fa-rocket"></i> View Projects
                    </a>
                    <a href="#contact" class="btn-secondary">
                        <i class="fas fa-envelope"></i> Get in Touch
                    </a>
                </div>
            </div>
        </div>

        <!-- 3D Floating Cards -->
        <div class="hero-3d-container">
            <div class="hero-3d-object">
                <div class="glass-card-3d card-1">
                    <div class="card-header">
                        <div class="card-dot red"></div>
                        <div class="card-dot yellow"></div>
                        <div class="card-dot green"></div>
                    </div>
                    <div class="card-code">
                        <span class="keyword">async</span> <span class="function">solveProblem</span>() {<br>
                        &nbsp;&nbsp;<span class="keyword">const</span> solution = <span class="keyword">await</span><br>
                        &nbsp;&nbsp;&nbsp;&nbsp;<span class="function">deepAnalyze</span>(problem);<br>
                        &nbsp;&nbsp;<span class="keyword">return</span> <span class="function">ship</span>(solution);<br>
                        }
                    </div>
                </div>
                <div class="glass-card-3d card-2">
                    <div class="card-stats">
                        <div class="stat-item">
                            <span class="stat-label">Easy</span>
                            <span class="stat-value">222</span>
                        </div>
                        <div class="stat-bar"><div class="stat-bar-fill" style="width: 75%"></div></div>
                        <div class="stat-item">
                            <span class="stat-label">Medium</span>
                            <span class="stat-value">85</span>
                        </div>
                        <div class="stat-bar"><div class="stat-bar-fill" style="width: 45%"></div></div>
                        <div class="stat-item">
                            <span class="stat-label">Hard</span>
                            <span class="stat-value">8</span>
                        </div>
                        <div class="stat-bar"><div class="stat-bar-fill" style="width: 15%"></div></div>
                    </div>
                </div>
                <div class="glass-card-3d card-3">
                    <div class="card-tech">
                        <span class="tech-tag">React</span>
                        <span class="tech-tag">Node.js</span>
                        <span class="tech-tag">Python</span>
                        <span class="tech-tag">Flutter</span>
                    </div>
                </div>
            </div>
        </div>

        <div class="scroll-indicator">
            <span>Scroll</span>
            <div class="scroll-line"></div>
        </div>
    </section>

    <div class="section-divider"></div>

    <!-- About Section -->
    <section class="about" id="about">
        <div class="section-container">
            <div class="about-grid">
                <div class="about-image-container reveal-left">
                    <div class="about-image-wrapper">
                        <img src="https://picsum.photos/seed/naren-dev/600/500.jpg" alt="Narendaran M">
                        <div class="about-image-overlay"></div>
                    </div>
                    <div class="about-image-border"></div>
                    <div class="about-floating-card">
                        <div class="years">30+</div>
                        <div class="years-text">Projects Completed</div>
                    </div>
                </div>
                <div class="about-text reveal-right">
                    <div class="section-label">About Me</div>
                    <h2 class="section-title">Building <span class="highlight">resilient</span> systems</h2>
                    <p>
                        I'm a full-stack engineer who deeply understands a problem before writing a single line — then ships something that holds up in production. My work spans web platforms, mobile apps, applied cryptography, and lightweight AI tooling.
                    </p>
                    <div class="about-quote">
                        "I'd rather rebuild it from scratch than patch it."
                    </div>
                    <p>
                        Currently building an AI-assisted incident management platform and deepening my expertise in applied cryptography, NLP, and system design.
                    </p>
                    <div class="about-highlights">
                        <div class="highlight-item">
                            <div class="highlight-icon"><i class="fas fa-code"></i></div>
                            <div class="highlight-text">
                                <strong>Clean Code</strong>
                                Production-grade standards
                            </div>
                        </div>
                        <div class="highlight-item">
                            <div class="highlight-icon"><i class="fas fa-shield-halved"></i></div>
                            <div class="highlight-text">
                                <strong>Security</strong>
                                Cryptography & Auth
                            </div>
                        </div>
                        <div class="highlight-item">
                            <div class="highlight-icon"><i class="fas fa-brain"></i></div>
                            <div class="highlight-text">
                                <strong>AI/ML</strong>
                                NLP & Applied AI
                            </div>
                        </div>
                        <div class="highlight-item">
                            <div class="highlight-icon"><i class="fas fa-server"></i></div>
                            <div class="highlight-text">
                                <strong>Systems</strong>
                                Scalable Architecture
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <div class="section-divider"></div>

    <!-- Skills Section -->
    <section class="skills" id="skills">
        <div class="section-container">
            <div class="section-label reveal">Tech Arsenal</div>
            <h2 class="section-title reveal">Technologies I <span class="highlight">master</span></h2>
            
            <div class="skills-grid">
                <div class="skill-category reveal">
                    <div class="skill-icon"><i class="fab fa-react"></i></div>
                    <h3>Frontend</h3>
                    <div class="skill-list">
                        <div class="skill-item"><span>React / Next.js</span><span>Expert</span></div>
                        <div class="skill-item"><span>Flutter</span><span>Advanced</span></div>
                        <div class="skill-item"><span>Tailwind CSS</span><span>Expert</span></div>
                        <div class="skill-item"><span>Redux</span><span>Advanced</span></div>
                        <div class="skill-item"><span>Socket.io</span><span>Advanced</span></div>
                    </div>
                </div>
                <div class="skill-category reveal">
                    <div class="skill-icon"><i class="fab fa-node-js"></i></div>
                    <h3>Backend</h3>
                    <div class="skill-list">
                        <div class="skill-item"><span>Node.js / Express</span><span>Expert</span></div>
                        <div class="skill-item"><span>Python / Flask</span><span>Expert</span></div>
                        <div class="skill-item"><span>Django / FastAPI</span><span>Advanced</span></div>
                        <div class="skill-item"><span>REST APIs</span><span>Expert</span></div>
                        <div class="skill-item"><span>GraphQL</span><span>Intermediate</span></div>
                    </div>
                </div>
                <div class="skill-category reveal">
                    <div class="skill-icon"><i class="fas fa-database"></i></div>
                    <h3>Data & Infra</h3>
                    <div class="skill-list">
                        <div class="skill-item"><span>MongoDB</span><span>Expert</span></div>
                        <div class="skill-item"><span>PostgreSQL</span><span>Advanced</span></div>
                        <div class="skill-item"><span>Redis</span><span>Intermediate</span></div>
                        <div class="skill-item"><span>Docker</span><span>Advanced</span></div>
                        <div class="skill-item"><span>GCP / Vercel</span><span>Advanced</span></div>
                    </div>
                </div>
                <div class="skill-category reveal">
                    <div class="skill-icon"><i class="fas fa-lock"></i></div>
                    <h3>Specialized</h3>
                    <div class="skill-list">
                        <div class="skill-item"><span>JWT / OAuth 2.0</span><span>Expert</span></div>
                        <div class="skill-item"><span>Cryptography</span><span>Advanced</span></div>
                        <div class="skill-item"><span>NLP</span><span>Advanced</span></div>
                        <div class="skill-item"><span>scikit-learn</span><span>Intermediate</span></div>
                        <div class="skill-item"><span>Git / CI/CD</span><span>Expert</span></div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <div class="section-divider"></div>

    <!-- Projects Section -->
    <section class="projects" id="projects">
        <div class="section-container">
            <div class="section-label reveal">Featured Work</div>
            <h2 class="section-title reveal">Projects I've <span class="highlight">built</span></h2>
            
            <div class="projects-grid">
                <div class="project-card featured reveal-scale">
                    <div class="project-image">
                        <img src="https://picsum.photos/seed/ai-devops/1200/400.jpg" alt="AI DevOps Incident Management">
                        <div class="project-image-overlay"></div>
                        <div class="project-featured-badge">🔥 Featured</div>
                    </div>
                    <div class="project-content">
                        <h3 class="project-title">
                            <i class="fas fa-robot"></i>
                            AI DevOps Incident Management
                        </h3>
                        <p class="project-desc">
                            Full-stack incident management platform with AI-assisted severity classification, live dashboards, and complete lifecycle tracking. Deployed and live in production.
                        </p>
                        <div class="project-tech">
                            <span>React</span>
                            <span>Flask</span>
                            <span>PostgreSQL</span>
                            <span>JWT</span>
                            <span>AI/NLP</span>
                        </div>
                        <div class="project-links">
                            <a href="https://github.com/NAREN-105/AI-DevOps-Incident-Management" class="project-link primary" target="_blank">
                                <i class="fab fa-github"></i> Source Code
                            </a>
                            <a href="https://ai-dev-ops-incident-management.vercel.app" class="project-link secondary" target="_blank">
                                <i class="fas fa-external-link-alt"></i> Live Demo
                            </a>
                        </div>
                    </div>
                </div>
                
                <div class="project-card reveal-scale">
                    <div class="project-image">
                        <img src="https://picsum.photos/seed/chatbot-nlp/600/300.jpg" alt="Final Review Chatbot">
                        <div class="project-image-overlay"></div>
                    </div>
                    <div class="project-content">
                        <h3 class="project-title">
                            <i class="fas fa-comments"></i>
                            Final Review Chatbot
                        </h3>
                        <p class="project-desc">
                            Document Q&A chatbot with custom NLP pipeline — zero ML models, zero external APIs, 91% accuracy. Auto-generates presentation slides.
                        </p>
                        <div class="project-tech">
                            <span>Python</span>
                            <span>NLP</span>
                            <span>Tkinter</span>
                        </div>
                        <div class="project-links">
                            <a href="https://github.com/NAREN-105/FINAL_REVIEW_CHATBOT" class="project-link primary" target="_blank">
                                <i class="fab fa-github"></i> View Repo
                            </a>
                        </div>
                    </div>
                </div>
                
                <div class="project-card reveal-scale">
                    <div class="project-image">
                        <img src="https://picsum.photos/seed/crypto-api/600/300.jpg" alt="Shamir's Secret Sharing API">
                        <div class="project-image-overlay"></div>
                    </div>
                    <div class="project-content">
                        <h3 class="project-title">
                            <i class="fas fa-key"></i>
                            Shamir's Secret Sharing API
                        </h3>
                        <p class="project-desc">
                            Production-style API implementing Shamir's Secret Sharing with mathematical reconstruction via Lagrange interpolation.
                        </p>
                        <div class="project-tech">
                            <span>JavaScript</span>
                            <span>Cryptography</span>
                            <span>REST API</span>
                        </div>
                        <div class="project-links">
                            <a href="https://github.com/NAREN-105/REST_API_USING_SSS" class="project-link primary" target="_blank">
                                <i class="fab fa-github"></i> View Repo
                            </a>
                        </div>
                    </div>
                </div>
            </div>
            
            <div style="text-align: center; margin-top: 50px;" class="reveal">
                <a href="https://github.com/NAREN-105?tab=repositories" class="btn-secondary" target="_blank">
                    <i class="fab fa-github"></i> View All Repositories
                </a>
            </div>
        </div>
    </section>

    <div class="section-divider"></div>

    <!-- LeetCode Section -->
    <section class="leetcode" id="leetcode">
        <div class="section-container">
            <div class="section-label reveal">Problem Solving</div>
            <h2 class="section-title reveal">LeetCode <span class="highlight">Journey</span></h2>
            
            <div class="leetcode-container reveal">
                <div class="leetcode-card">
                    <img src="https://leetcode-stats.vercel.app/api?username=NARENDARAN_M&theme=dark&border_radius=12&hide_rank=true" alt="LeetCode Stats">
                </div>
                <div class="leetcode-card">
                    <img src="https://leetcard.jacoblin.cool/NARENDARAN_M?theme=dark&font=roboto&border_radius=12" alt="LeetCode Card">
                </div>
            </div>
            
            <div class="leetcode-stats-grid reveal">
                <div class="leetcode-stat easy">
                    <div class="number">222</div>
                    <div class="label">Easy Solved</div>
                </div>
                <div class="leetcode-stat medium">
                    <div class="number">85</div>
                    <div class="label">Medium Solved</div>
                </div>
                <div class="leetcode-stat hard">
                    <div class="number">8</div>
                    <div class="label">Hard Solved</div>
                </div>
            </div>
            
            <div class="leetcode-cta reveal">
                <a href="https://leetcode.com/u/NARENDARAN_M/" class="btn-primary" target="_blank" style="background: #FFA116; color: #0F172A;">
                    <i class="fas fa-trophy"></i> View LeetCode Profile
                </a>
            </div>
        </div>
    </section>

    <div class="section-divider"></div>

    <!-- Contact Section -->
    <section class="contact" id="contact">
        <div class="section-container">
            <div class="section-label reveal">Get in Touch</div>
            <h2 class="section-title reveal">Let's <span class="highlight">connect</span></h2>
            
            <div class="contact-grid">
                <div class="contact-info reveal-left">
                    <div class="contact-item">
                        <div class="contact-icon"><i class="fas fa-envelope"></i></div>
                        <div>
                            <h4>Email</h4>
                            <p><a href="mailto:narenrdkn@gmail.com">narenrdkn@gmail.com</a></p>
                        </div>
                    </div>
                    <div class="contact-item">
                        <div class="contact-icon"><i class="fab fa-linkedin"></i></div>
                        <div>
                            <h4>LinkedIn</h4>
                            <p><a href="https://www.linkedin.com/in/narendaran-m-rdknnkdr" target="_blank">Connect with me</a></p>
                        </div>
                    </div>
                    <div class="contact-item">
                        <div class="contact-icon"><i class="fas fa-globe"></i></div>
                        <div>
                            <h4>Portfolio</h4>
                            <p><a href="https://naren-105.github.io" target="_blank">naren-105.github.io</a></p>
                        </div>
                    </div>
                    <div class="contact-item">
                        <div class="contact-icon"><i class="fab fa-dev"></i></div>
                        <div>
                            <h4>Dev.to</h4>
                            <p><a href="https://dev.to/narendaran_m" target="_blank">Read my blogs</a></p>
                        </div>
                    </div>
                </div>
                <form class="contact-form reveal-right" id="contactForm">
                    <div class="form-group">
                        <input type="text" placeholder="Your Name" required>
                    </div>
                    <div class="form-group">
                        <input type="email" placeholder="Your Email" required>
                    </div>
                    <div class="form-group">
                        <input type="text" placeholder="Subject">
                    </div>
                    <div class="form-group">
                        <textarea placeholder="Your Message" required></textarea>
                    </div>
                    <button type="submit" class="form-submit">
                        <i class="fas fa-paper-plane"></i> Send Message
                    </button>
                </form>
            </div>
        </div>
    </section>

    <!-- Footer -->
    <footer class="footer">
        <div class="section-container">
            <div class="footer-content">
                <div class="footer-text">
                    © 2024 <span>Narendaran M</span>. Built with passion & clean code.
                </div>
                <div class="footer-socials">
                    <a href="https://github.com/NAREN-105" class="footer-social" target="_blank"><i class="fab fa-github"></i></a>
                    <a href="https://www.linkedin.com/in/narendaran-m-rdknnkdr" class="footer-social" target="_blank"><i class="fab fa-linkedin"></i></a>
                    <a href="https://leetcode.com/u/NARENDARAN_M/" class="footer-social" target="_blank"><i class="fas fa-code"></i></a>
                    <a href="https://dev.to/narendaran_m" class="footer-social" target="_blank"><i class="fab fa-dev"></i></a>
                    <a href="https://www.instagram.com/__naren_03" class="footer-social" target="_blank"><i class="fab fa-instagram"></i></a>
                </div>
            </div>
        </div>
    </footer>

    <script>
        // ═══════════════════════════════════════
        // LOADER
        // ═══════════════════════════════════════
        const progressBar = document.getElementById('progressBar');
        let progress = 0;
        const progressInterval = setInterval(() => {
            progress += Math.random() * 15 + 5;
            if (progress >= 100) {
                progress = 100;
                clearInterval(progressInterval);
                setTimeout(() => {
                    document.getElementById('loader').classList.add('hidden');
                }, 500);
            }
            progressBar.style.width = progress + '%';
        }, 200);

        // ═══════════════════════════════════════
        // CUSTOM CURSOR
        // ═══════════════════════════════════════
        const cursorDot = document.getElementById('cursorDot');
        const cursorRing = document.getElementById('cursorRing');
        
        document.addEventListener('mousemove', (e) => {
            cursorDot.style.left = e.clientX - 4 + 'px';
            cursorDot.style.top = e.clientY - 4 + 'px';
            cursorRing.style.left = e.clientX - 20 + 'px';
            cursorRing.style.top = e.clientY - 20 + 'px';
        });

        document.querySelectorAll('a, button, .skill-category, .project-card, .contact-item').forEach(el => {
            el.addEventListener('mouseenter', () => cursorRing.classList.add('hover'));
            el.addEventListener('mouseleave', () => cursorRing.classList.remove('hover'));
        });

        // ═══════════════════════════════════════
        // NAVIGATION
        // ═══════════════════════════════════════
        const nav = document.getElementById('nav');
        window.addEventListener('scroll', () => {
            nav.classList.toggle('scrolled', window.scrollY > 50);
        });

        const menuToggle = document.getElementById('menuToggle');
        menuToggle.addEventListener('click', () => {
            menuToggle.classList.toggle('active');
            // Add mobile menu toggle logic here
        });

        // ═══════════════════════════════════════
        // SCROLL REVEAL
        // ═══════════════════════════════════════
        const revealElements = document.querySelectorAll('.reveal, .reveal-left, .reveal-right, .reveal-scale');
        
        const revealObserver = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    entry.target.classList.add('active');
                }
            });
        }, { threshold: 0.1 });

        revealElements.forEach(el => revealObserver.observe(el));

        // ═══════════════════════════════════════
        // THREE.JS 3D BACKGROUND
        // ═══════════════════════════════════════
        const canvas = document.getElementById('bg-canvas');
        const scene = new THREE.Scene();
        const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
        const renderer = new THREE.WebGLRenderer({ canvas, alpha: true, antialias: true });
        renderer.setSize(window.innerWidth, window.innerHeight);
        renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));

        // Particles
        const particlesGeometry = new THREE.BufferGeometry();
        const particlesCount = 2000;
        const posArray = new Float32Array(particlesCount * 3);
        
        for (let i = 0; i < particlesCount * 3; i++) {
            posArray[i] = (Math.random() - 0.5) * 15;
        }
        
        particlesGeometry.setAttribute('position', new THREE.BufferAttribute(posArray, 3));
        
        const particlesMaterial = new THREE.PointsMaterial({
            size: 0.008,
            color: 0x38BDF8,
            transparent: true,
            opacity: 0.8,
            blending: THREE.AdditiveBlending
        });
        
        const particlesMesh = new THREE.Points(particlesGeometry, particlesMaterial);
        scene.add(particlesMesh);

        // Floating Geometries
        const geometries = [];
        const materials = [
            new THREE.MeshBasicMaterial({ color: 0x38BDF8, wireframe: true, transparent: true, opacity: 0.15 }),
            new THREE.MeshBasicMaterial({ color: 0xA78BFA, wireframe: true, transparent: true, opacity: 0.12 }),
            new THREE.MeshBasicMaterial({ color: 0xFB923C, wireframe: true, transparent: true, opacity: 0.1 })
        ];

        // Icosahedron
        const ico = new THREE.Mesh(new THREE.IcosahedronGeometry(1.5, 1), materials[0]);
        ico.position.set(4, 2, -3);
        scene.add(ico);
        geometries.push(ico);

        // Octahedron
        const octa = new THREE.Mesh(new THREE.OctahedronGeometry(1, 0), materials[1]);
        octa.position.set(-4, -2, -2);
        scene.add(octa);
        geometries.push(octa);

        // Torus
        const torus = new THREE.Mesh(new THREE.TorusGeometry(1.2, 0.3, 8, 16), materials[2]);
        torus.position.set(0, 4, -4);
        scene.add(torus);
        geometries.push(torus);

        // Dodecahedron
        const dodeca = new THREE.Mesh(new THREE.DodecahedronGeometry(0.8, 0), materials[0]);
        dodeca.position.set(-3, 3, -3);
        scene.add(dodeca);
        geometries.push(dodeca);

        camera.position.z = 5;

        // Mouse interaction
        let mouseX = 0, mouseY = 0;
        document.addEventListener('mousemove', (e) => {
            mouseX = (e.clientX / window.innerWidth) * 2 - 1;
            mouseY = -(e.clientY / window.innerHeight) * 2 + 1;
        });

        // Animation Loop
        function animate() {
            requestAnimationFrame(animate);
            
            const time = Date.now() * 0.001;
            
            // Rotate particles
            particlesMesh.rotation.x += 0.0003;
            particlesMesh.rotation.y += 0.0005;
            
            // Animate geometries
            ico.rotation.x = time * 0.3;
            ico.rotation.y = time * 0.2;
            ico.position.y = 2 + Math.sin(time * 0.5) * 0.5;
            
            octa.rotation.x = time * 0.4;
            octa.rotation.z = time * 0.3;
            octa.position.y = -2 + Math.sin(time * 0.7) * 0.4;
            
            torus.rotation.x = time * 0.2;
            torus.rotation.y = time * 0.5;
            torus.position.x = Math.sin(time * 0.3) * 2;
            
            dodeca.rotation.x = time * 0.5;
            dodeca.rotation.y = time * 0.3;
            dodeca.position.y = 3 + Math.cos(time * 0.4) * 0.6;
            
            // Camera follow mouse
            camera.position.x += (mouseX * 0.5 - camera.position.x) * 0.02;
            camera.position.y += (mouseY * 0.3 - camera.position.y) * 0.02;
            camera.lookAt(scene.position);
            
            renderer.render(scene, camera);
        }
        animate();

        // Resize handler
        window.addEventListener('resize', () => {
            camera.aspect = window.innerWidth / window.innerHeight;
            camera.updateProjectionMatrix();
            renderer.setSize(window.innerWidth, window.innerHeight);
        });

        // ═══════════════════════════════════════
        // CONTACT FORM
        // ═══════════════════════════════════════
        document.getElementById('contactForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const btn = e.target.querySelector('.form-submit');
            const originalHTML = btn.innerHTML;
            btn.innerHTML = '<i class="fas fa-check"></i> Message Sent!';
            btn.style.background = 'linear-gradient(135deg, #22C55E, #16A34A)';
            setTimeout(() => {
                btn.innerHTML = originalHTML;
                btn.style.background = '';
                e.target.reset();
            }, 3000);
        });

        // ═══════════════════════════════════════
        // SMOOTH SCROLL
        // ═══════════════════════════════════════
        document.querySelectorAll('a[href^="#"]').forEach(anchor => {
            anchor.addEventListener('click', function(e) {
                e.preventDefault();
                const target = document.querySelector(this.getAttribute('href'));
                if (target) {
                    target.scrollIntoView({ behavior: 'smooth', block: 'start' });
                }
            });
        });

        // ═══════════════════════════════════════
        // TYPING EFFECT FOR HERO
        // ═══════════════════════════════════════
        const roles = ['Full-Stack Engineer', 'System Designer', 'Problem Solver', 'Security Enthusiast'];
        let roleIndex = 0;
        let charIndex = 0;
        let isDeleting = false;
        const heroTitle = document.querySelector('.hero-title .line-2');
        
        function typeRole() {
            const currentRole = roles[roleIndex];
            
            if (isDeleting) {
                heroTitle.textContent = currentRole.substring(0, charIndex - 1);
                charIndex--;
            } else {
                heroTitle.textContent = currentRole.substring(0, charIndex + 1);
                charIndex++;
            }
            
            let typeSpeed = isDeleting ? 50 : 100;
            
            if (!isDeleting && charIndex === currentRole.length) {
                typeSpeed = 2000;
                isDeleting = true;
            } else if (isDeleting && charIndex === 0) {
                isDeleting = false;
                roleIndex = (roleIndex + 1) % roles.length;
                typeSpeed = 500;
            }
            
            setTimeout(typeRole, typeSpeed);
        }
        
        // Start typing after loader
        setTimeout(typeRole, 2500);
    </script>
</body>
</html>
