<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gamers Place — Your Gaming Hub</title>
    <style>
        /* ========== THEME ROOT VARIABLES ========== */
        :root {
            --primary-accent: #00ffc8;
            --primary-glow: #00ffc8aa;
            --primary-gradient: linear-gradient(90deg, #00ffc8, #00d4ff);
            --secondary-accent: #ff3d8b;
            --secondary-glow: rgba(255, 61, 139, 0.4);
            --secondary-gradient: linear-gradient(90deg, #ff3d8b, #d400ff);
        }

        /* --- THEME VARIATION OVERRIDES --- */
        [data-theme="pink"] {
            --primary-accent: #ff3d8b;
            --primary-glow: #ff3d8baa;
            --primary-gradient: linear-gradient(90deg, #ff3d8b, #ff7bb0);
            --secondary-accent: #00ffc8;
            --secondary-glow: rgba(0, 255, 200, 0.4);
            --secondary-gradient: linear-gradient(90deg, #00ffc8, #00d4ff);
        }

        [data-theme="cyan"] {
            --primary-accent: #00d4ff;
            --primary-glow: #00d4ffaa;
            --primary-gradient: linear-gradient(90deg, #00d4ff, #0077ff);
            --secondary-accent: #ffb700;
            --secondary-glow: rgba(255, 183, 0, 0.4);
            --secondary-gradient: linear-gradient(90deg, #ffb700, #ff5500);
        }

        /* ========== RESET & BASE ========== */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        html {
            scroll-behavior: smooth;
        }
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: #0a0a14;
            color: #e0e0ff;
            line-height: 1.6;
            overflow-x: hidden;
            transition: background 0.3s ease;
        }
        a {
            text-decoration: none;
            color: inherit;
        }
        ul {
            list-style: none;
        }

        /* ========== NEON TEXT & GLOW ========== */
        .neon {
            color: var(--primary-accent);
            text-shadow: 0 0 10px var(--primary-accent), 0 0 20px var(--primary-glow);
            transition: color 0.3s ease, text-shadow 0.3s ease;
        }
        .accent {
            color: var(--secondary-accent);
            transition: color 0.3s ease;
        }

        /* ========== NAVBAR ========== */
        nav {
            position: fixed;
            top: 0;
            width: 100%;
            z-index: 100;
            background: rgba(10, 10, 20, 0.95);
            backdrop-filter: blur(10px);
            border-bottom: 1px solid #222244;
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px 5%;
        }
        .nav-left-group {
            display: flex;
            align-items: center;
            gap: 20px;
        }
        .logo-text {
            font-size: 1.5rem;
            font-weight: 800;
            letter-spacing: 1px;
            text-transform: uppercase;
            cursor: pointer;
            z-index: 102;
        }
        
        .control-matrix {
            display: flex;
            align-items: center;
            gap: 15px;
            background: rgba(20, 20, 40, 0.6);
            padding: 6px 14px;
            border-radius: 20px;
            border: 1px solid #222244;
        }
        .theme-selector-wrapper {
            display: flex;
            gap: 8px;
        }
        .theme-dot {
            width: 14px;
            height: 14px;
            border-radius: 50%;
            cursor: pointer;
            border: 1px solid rgba(255,255,255,0.2);
            transition: transform 0.2s, border-color 0.2s;
        }
        .theme-dot:hover { transform: scale(1.2); }
        .theme-dot.dot-green { background: #00ffc8; }
        .theme-dot.dot-pink { background: #ff3d8b; }
        .theme-dot.dot-cyan { background: #00d4ff; }
        .theme-dot.active { border-color: #ffffff; box-shadow: 0 0 8px currentColor; }

        .audio-toggle-btn {
            background: none;
            border: none;
            color: #666688;
            cursor: pointer;
            font-size: 0.9rem;
            display: flex;
            align-items: center;
            transition: color 0.2s;
            padding-left: 10px;
            border-left: 1px solid #222244;
        }
        .audio-toggle-btn.muted { color: #ff3d8b; }
        .audio-toggle-btn:not(.muted) { color: #00ffc8; }

        .nav-links {
            display: flex;
            gap: 30px;
            align-items: center;
        }
        .nav-links li a {
            font-weight: 500;
            transition: color 0.3s;
        }
        .nav-links li a:hover {
            color: var(--primary-accent);
        }
        .nav-cta {
            background: var(--primary-gradient);
            color: #0a0a14;
            font-weight: 700;
            padding: 8px 20px;
            border-radius: 30px;
            transition: transform 0.2s, background 0.3s;
            border: none;
            cursor: pointer;
        }
        .nav-cta:hover {
            transform: scale(1.05);
        }

        /* Hamburger Icon Structure */
        .hamburger {
            display: none;
            flex-direction: column;
            gap: 6px;
            cursor: pointer;
            z-index: 102;
            padding: 5px;
        }
        .hamburger span {
            display: block;
            width: 28px;
            height: 3px;
            background-color: var(--primary-accent);
            border-radius: 2px;
            transition: all 0.3s cubic-bezier(0.075, 0.82, 0.165, 1);
        }

        /* Hamburger Active Animations */
        .hamburger.active span:nth-child(1) { transform: translateY(9px) rotate(45deg); }
        .hamburger.active span:nth-child(2) { opacity: 0; transform: translateX(-20px); }
        .hamburger.active span:nth-child(3) { transform: translateY(-9px) rotate(-45deg); }

        /* ========== HERO ========== */
        .hero {
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
            padding: 120px 5% 60px;
            background: radial-gradient(circle at 20% 20%, #1a1a3a 0%, transparent 50%), radial-gradient(circle at 80% 80%, #3a1030 0%, transparent 50%), #0a0a14;
            position: relative;
            overflow: hidden;
        }
        .hero::before {
            content: "";
            position: absolute;
            inset: 0;
            background: linear-gradient(90deg, transparent 49.8%, rgba(0, 255, 200, 0.08) 50%, transparent 50.2%), linear-gradient(0deg, transparent 49.8%, rgba(0, 255, 200, 0.08) 50%, transparent 50.2%);
            background-size: 60px 60px;
            animation: gridMove 15s linear infinite;
            opacity: 0.5;
        }
        @keyframes gridMove {
            from { transform: translateY(0); }
            to { transform: translateY(60px); }
        }
        .hero h1 {
            font-size: clamp(2.2rem, 6vw, 4rem);
            font-weight: 900;
            letter-spacing: 2px;
            margin-bottom: 20px;
            position: relative;
            text-transform: uppercase;
        }
        .hero p {
            font-size: clamp(1rem, 2vw, 1.2rem);
            color: #a3a3c2;
            max-width: 600px;
            margin-bottom: 40px;
            position: relative;
            z-index: 2;
        }

        /* ========== BUTTONS ========== */
        .btn-container {
            display: flex;
            gap: 20px;
            justify-content: center;
            position: relative;
            z-index: 2;
        }
        .btn {
            padding: 14px 32px;
            border-radius: 30px;
            font-weight: 700;
            font-size: 1rem;
            transition: all 0.3s ease;
            cursor: pointer;
            text-transform: uppercase;
        }
        .btn-primary {
            background: var(--primary-gradient);
            color: #0a0a14;
            border: none;
            box-shadow: 0 4px 15px var(--primary-glow);
        }
        .btn-primary:hover {
            transform: translateY(-3px);
            box-shadow: 0 6px 20px var(--primary-accent);
        }
        .btn-secondary {
            background: transparent;
            color: var(--primary-accent);
            border: 2px solid var(--primary-accent);
        }
        .btn-secondary:hover {
            background: rgba(0, 255, 200, 0.1);
            transform: translateY(-3px);
        }

        /* ========== SHARED SECTION CLASS ========== */
        .section-padding {
            padding: 100px 5%;
        }
        .section-container {
            max-width: 1200px;
            margin: 0 auto;
        }
        .section-title {
            font-size: 2.5rem;
            text-align: center;
            text-transform: uppercase;
            letter-spacing: 1px;
            margin-bottom: 10px;
        }
        .section-subtitle {
            text-align: center;
            color: #a3a3c2;
            margin-bottom: 50px;
            font-size: 1.1rem;
        }

        /* ========== LEADERBOARD SECTION ========== */
        .leaderboard-section {
            background: #0d0d1f;
        }

        /* ========== SEARCH BAR ========== */
        .search-container {
            max-width: 400px;
            margin: 0 auto 30px;
            position: relative;
        }
        .search-container input {
            width: 100%;
            padding: 12px 20px;
            background: rgba(20, 20, 40, 0.8);
            border: 1px solid #222244;
            border-radius: 30px;
            color: #ffffff;
            font-size: 1rem;
            font-family: inherit;
