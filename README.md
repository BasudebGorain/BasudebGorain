<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Background Environment</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link
        href="https://fonts.googleapis.com/css2?family=Aldrich&family=Montserrat:wght@900&family=Oswald:wght@500;700&family=Outfit:wght@300;400&family=Rajdhani:wght@300;400;500;600;700&family=Syncopate:wght@400;700&family=Syne:wght@400;700;800&display=swap"
        rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://unpkg.com/@studio-freight/lenis@1.0.42/dist/lenis.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/opentype.js/1.3.4/opentype.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>

    <style>
        :root {
            --font-aldrich: 'Aldrich', sans-serif;
            --font-rajdhani: 'Rajdhani', sans-serif;
            --font-syne: 'Syne', sans-serif;
            --font-oswald: 'Oswald', sans-serif;
            --font-syncopate: 'Syncopate', sans-serif;
            --font-montserrat: 'Montserrat', sans-serif;
            --font-outfit: 'Outfit', sans-serif;
            --font-consolas: 'Consolas', monospace;

            --neon-green: #00ff88;
            --neon-cyan: #00f3ff;
            --bg-color: #02050a;

            --card-height: 55vh;
            --card-width: 22vw;
            --glass-bg: rgba(255, 255, 255, 0.08);
            --glass-border: rgba(255, 255, 255, 0.15);
            --solid-white: #ffffff;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            cursor: none !important;
        }

        html.lenis {
            height: auto;
        }

        .latest-release-container {
            display: flex;
            gap: 30px;
            align-items: center;
            flex-wrap: wrap;
            pointer-events: auto;
        }

        #latest-release-btn {
            position: relative;
        }

        #latest-release-btn .main_back {
            position: absolute;
            top: 0;
            left: 10%;
            width: 80%;
            height: 100%;
            border-radius: 10px;
            background: transparent;
            z-index: 1;
            border: 1px solid rgba(255, 255, 255, 0.2);
            transition: opacity 0.1s ease;
            pointer-events: none;
        }

        #latest-release-btn .main {
            display: flex;
            flex-wrap: wrap;
            width: 14em;
            align-items: center;
            justify-content: center;
            z-index: 1;
            position: relative;
            border-radius: 10px;
        }

        #latest-release-btn .card {
            display: flex;
            align-items: center;
            justify-content: center;
            width: 60px;
            height: 60px;
            border-top-left-radius: 10px;
            background: rgba(10, 20, 40, 0.3);
            transition: 0.3s ease-in-out;
            backdrop-filter: blur(5px);
            border: 1px solid transparent;
            -webkit-backdrop-filter: blur(5px);
            color: transparent;
            font-size: 10px;
            font-weight: 500;
            text-align: center;
            text-decoration: none;
            overflow: hidden;
            white-space: nowrap;
        }

        #latest-release-btn .card:hover {
            background: rgba(255, 255, 255, 0.1);
            border-color: rgba(255, 255, 255, 0.3);
            box-shadow: 0 0 10px rgba(3, 169, 244, 0.2);
            color: white;
            cursor: pointer;
        }

        #latest-release-btn .card:nth-child(2),
        #latest-release-btn .card:nth-child(4),
        #latest-release-btn .card:nth-child(5),
        #latest-release-btn .card:nth-child(6),
        #latest-release-btn .card:nth-child(8) {
            border-radius: 0px;
        }

        #latest-release-btn .card:nth-child(3) {
            border-top-right-radius: 10px;
            border-top-left-radius: 0px;
        }

        #latest-release-btn .card:nth-child(7) {
            border-bottom-left-radius: 10px;
            border-top-left-radius: 0px;
        }

        #latest-release-btn .card:nth-child(9) {
            border-bottom-right-radius: 10px;
            border-top-left-radius: 0px;
        }


        #latest-release-btn .main:hover {
            width: 14em;
            cursor: pointer;
        }

        #latest-release-btn .main:hover .main_back {
            opacity: 0;
        }

        #latest-release-btn .main:hover .card {
            margin: 0.2em;
            border-radius: 10px;
            box-shadow: 0 4px 30px rgba(0, 0, 0, 0.1);
            border: 1px solid rgba(255, 255, 255, 0.3);
            color: rgba(255, 255, 255, 0.8);
        }

        #latest-release-btn .main:hover .text {
            opacity: 0;
            z-index: -3;
        }

        #latest-release-btn .text {
            position: absolute;
            font-size: 0.7em;
            transition: 0.4s ease-in-out;
            color: #03a9f4;
            text-align: center;
            font-weight: bold;
            letter-spacing: 0.33em;
            z-index: 3;
            text-shadow: 0 0 5px #03a9f4, 0 0 10px #03a9f4, 0 0 20px #03a9f4;
        }

        .main-subtext {
            opacity: 0;
            transition: opacity 1s ease-in-out;
        }

        .main-subtext.visible {
            opacity: 1;
        }

        body {
            width: 100vw;
            min-height: 100vh;
            overflow: hidden;
            background-color: var(--bg-color);
            position: relative;
            font-family: 'Aldrich', sans-serif;
            color: white;
            touch-action: none;
        }

        .layer {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100vh;
            overflow: visible;
            display: flex;
            justify-content: center;
            align-items: center;
            pointer-events: none;
        }

        .gradient-container {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -10;
            filter: blur(80px);
            opacity: 0.6;
            transition: transform 0.2s ease-out;
        }

        .orb {
            position: absolute;
            border-radius: 50%;
            opacity: 0.6;
            animation: float 20s infinite alternate ease-in-out;
            mix-blend-mode: screen;
        }

        .orb-1 {
            width: 70vw;
            height: 70vw;
            background: radial-gradient(circle, #1a44c9 0%, transparent 70%);
            top: -20%;
            left: -10%;
            animation-duration: 25s;
        }

        .orb-2 {
            width: 60vw;
            height: 60vw;
            background: radial-gradient(circle, #001c40 0%, transparent 70%);
            bottom: -10%;
            right: -10%;
            animation-duration: 30s;
            animation-delay: -5s;
        }

        .orb-3 {
            width: 50vw;
            height: 50vw;
            background: radial-gradient(circle, #00509d 0%, transparent 70%);
            top: 40%;
            left: 40%;
            opacity: 0.4;
            animation-duration: 22s;
            animation-delay: -2s;
        }

        @keyframes float {
            0% {
                transform: translate(0, 0);
            }

            50% {
                transform: translate(30px, 50px);
            }

            100% {
                transform: translate(-20px, 20px);
            }
        }

        #particles-container {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -2;
            pointer-events: none;
        }

        .particle-bokeh {
            position: absolute;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.9);
            box-shadow: 0 0 10px rgba(255, 255, 255, 0.1);
            opacity: 0;
            will-change: transform, opacity;
        }

        @keyframes floatUp {
            0% {
                opacity: 0;
                transform: translateY(0) scale(0.8);
            }

            20% {
                opacity: var(--target-opacity);
                transform: translateY(-20px) scale(1);
            }

            80% {
                opacity: var(--target-opacity);
                transform: translateY(-100px) scale(0.9);
            }

            100% {
                opacity: 0;
                transform: translateY(-150px) scale(0.8);
            }
        }

        canvas.bg-canvas {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
        }

        #dna-canvas {
            z-index: -5;
            opacity: 1;
        }

        #network-canvas {
            z-index: -1;
        }

        .noise {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noiseFilter'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.7' numOctaves='3' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noiseFilter)' opacity='0.04'/%3E%3C/svg%3E");
            pointer-events: none;
            z-index: 15;
        }

        /* --- TEXT REVEAL LAYERS --- */
        #scene {
            z-index: 0;
            transition: transform 0.5s cubic-bezier(0.25, 0.46, 0.45, 0.94), opacity 0.5s ease;
        }

        #scene.hidden-layer {
            transform: translateY(-100px);
            opacity: 0;
        }

        .electric-layer {
            z-index: 1;
        }

        .stroke-static {
            fill: none;
            /* stroke: #333333; */
            stroke: rgba(200, 200, 200, 0.2);
            stroke-width: 2px;
            stroke-linecap: round;
            stroke-linejoin: round;
        }

        .stroke-running {
            fill: none;
            stroke: #ffffff;
            stroke-width: 2px;
            stroke-linecap: round;
            stroke-linejoin: round;
        }

        .solid-layer {
            z-index: 2;
            pointer-events: auto;
            --mask-size: 100px;
            --mask-x: 50%;
            --mask-y: 50%;
            -webkit-mask-image: radial-gradient(circle var(--mask-size) at var(--mask-x) var(--mask-y), transparent 99%, black 100%);
            mask-image: radial-gradient(circle var(--mask-size) at var(--mask-x) var(--mask-y), transparent 99%, black 100%);
            will-change: mask-image, -webkit-mask-image;
        }

        /* --- ANIMATION: CODEGEN TEXT REVEAL --- */
        @keyframes fadeInSimple {
            to {
                opacity: 1;
            }
        }

        #stroke-group,
        #static-stroke-group {
            opacity: 0;
            animation: fadeInSimple 0.3s ease-out forwards 0.6s;
        }

        #solid-group {
            opacity: 0;
            animation: fadeInSimple 0.7s ease-out forwards 1.0s;
        }

        .cursor-main {
            position: fixed;
            top: 0;
            left: 0;
            width: 24px;
            height: 24px;
            background-color: rgba(0, 243, 255, 0.3);
            border-radius: 50%;
            filter: blur(4px);
            pointer-events: none;
            z-index: 10000;
            transform: translate(-50%, -50%);
        }

        .cursor-glow {
            position: fixed;
            top: 0;
            left: 0;
            width: 160px;
            height: 160px;
            background: radial-gradient(circle, rgba(0, 243, 255, 0.15) 0%, transparent 70%);
            border-radius: 50%;
            filter: blur(30px);
            pointer-events: none;
            z-index: 9999;
            transform: translate(-50%, -50%);
        }

        .cursor-mask-circle {
            position: fixed;
            top: 0;
            left: 0;
            width: 200px;
            height: 200px;
            border: 2px solid rgba(255, 255, 255, 0.0);
            border-radius: 50%;
            pointer-events: none;
            z-index: 9999;
            margin-left: -100px;
            margin-top: -100px;
            will-change: transform;
            mix-blend-mode: difference;
        }

        .scroll-hint {
            position: fixed;
            bottom: 30px;
            left: 50%;
            transform: translateX(-50%);
            color: rgba(255, 255, 255, 0.5);
            font-family: 'Syncopate', sans-serif;
            font-size: 0.6rem;
            letter-spacing: 2px;
            z-index: 1000;
            pointer-events: none;
            transition: opacity 0.5s ease;
            opacity: 1;
        }

        .scroll-hint.hidden-hint {
            opacity: 0;
        }

        @media (max-width: 768px) {
            .solid-layer {
                --mask-size: 80px;
            }

            .cursor-mask-circle {
                width: 160px;
                height: 160px;
                margin-left: -80px;
                margin-top: -80px;
            }
        }

        .glass-ribbon {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 80px;
            background: rgba(10, 20, 40, 0.3);
            backdrop-filter: blur(6px);
            -webkit-backdrop-filter: blur(6px);
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
            z-index: 500;
            display: flex;
            align-items: center;
            padding-left: 50px;
            transition: transform 0.5s cubic-bezier(0.25, 0.46, 0.45, 0.94);
        }

        .glass-ribbon.hidden-ribbon {
            transform: translateY(-100%);
        }

        .status-container {
            display: flex;
            align-items: center;
            font-size: 0.9rem;
            letter-spacing: 2px;
            color: #888;
        }

        .status-dot {
            width: 8px;
            height: 8px;
            background-color: var(--neon-green);
            border-radius: 50%;
            margin-right: 12px;
            box-shadow: 0 0 10px var(--neon-green);
            animation: blink 2s infinite;
        }

        @keyframes blink {

            0%,
            100% {
                opacity: 1;
                transform: scale(1);
            }

            50% {
                opacity: 0.5;
                transform: scale(0.8);
            }
        }

        #canvas-back {
            z-index: 1;
        }

        #canvas-front {
            z-index: 9;
            mix-blend-mode: screen;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
        }

        .glass-container {
            position: relative;
            z-index: 5;
            pointer-events: all;
            display: flex;
            flex-direction: column;
            padding: 120vh 0 60vh 0;
            gap: 60vh;
            width: 100%;
            max-width: 1200px;
            margin: 0 auto;
        }

        .card-wrapper {
            position: relative;
            width: 100%;
            height: 40vh;
            display: flex;
            align-items: center;
            perspective: 1000px;
        }

        .glass-card {
            width: 35vh;
            max-width: 80vw;
            padding: 4.5vh;
            opacity: 0;
            background: rgba(10, 20, 40, 0.3);
            backdrop-filter: blur(15px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 12px;
            box-shadow: 0 10px 30px rgba(0, 243, 255, 0.1);
            color: white;
            text-align: center;
            will-change: transform, opacity;
            pointer-events: auto;
            transition: border-color 0.3s, background 0.3s;
        }

        .glass-card.activate-glitch {
            animation: hard-flicker 0.9s cubic-bezier(0.22, 0.5, 0.16, 0.8) forwards;
            opacity: 1 !important;
        }

        .glass-card:hover {
            border-color: rgba(255, 255, 255, 0.3);
            background: rgba(255, 255, 255, 0.12);
        }

        .glass-card h1 {
            margin: 0 0 1.5vh 0;
            font-size: 3.2vh;
            letter-spacing: 0.2vh;
            text-transform: uppercase;
            background: linear-gradient(to right, #b3e0ff, #ffffff);
            -webkit-background-clip: text;
            background-clip: text;
            -webkit-text-fill-color: transparent;
            text-shadow: 0 0 1.5vh rgba(136, 204, 255, 0.4);
        }

        .glass-card p {
            font-size: 1.8vh;
            line-height: 1.6;
            opacity: 0.85;
            margin-bottom: 4vh;
        }

        .btn {
            background: rgba(255, 255, 255, 0.1);
            border: 1px solid rgba(255, 255, 255, 0.2);
            color: white;
            padding: 1.5vh 3.5vh;
            border-radius: 4vh;
            cursor: pointer;
            transition: all 0.2s;
            text-decoration: none;
            display: inline-block;
            font-weight: 500;
            font-size: 1.8vh;
        }

        .btn:hover {
            background: white;
            color: black;
            box-shadow: 0 0 2vh rgba(255, 255, 255, 0.4);
        }

        @keyframes hard-flicker {
            0% {
                opacity: 1;
            }

            1% {
                background: var(--solid-white);
                box-shadow: 0 0 10vh rgba(255, 255, 255, 0.8);
            }

            3% {
                opacity: 0;
            }

            10% {
                opacity: 0;
            }

            11% {
                opacity: 1;
                background: var(--glass-bg);
                box-shadow: none;
            }

            15% {
                background: var(--solid-white);
                box-shadow: 0 0 10vh rgba(255, 255, 255, 1);
            }

            20% {
                background: var(--glass-bg);
            }

            40% {
                background: var(--glass-bg);
            }

            41% {
                background: var(--solid-white);
                box-shadow: 0 0 5vh rgba(255, 255, 255, 0.8);
            }

            45% {
                background: var(--glass-bg);
                box-shadow: 0 1vh 4vh 0 rgba(0, 0, 0, 0.5);
            }

            100% {
                opacity: 1;
                background: var(--glass-bg);
            }
        }

        .projects-section {
            position: relative;
            z-index: 10;
            width: 100%;
            padding: 0 50px 100px 50px;
            pointer-events: none;
        }

        .section-title {
            font-size: 1rem;
            letter-spacing: 4px;
            color: var(--neon-green);
            margin-bottom: 50px;
            border-left: 2px solid var(--neon-green);
            padding-left: 20px;
            margin-top: 50px;
        }

        .grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 30px;
            pointer-events: auto;
        }

        .project-card,
        .about-card {
            background: rgba(10, 20, 40, 0.3);
            backdrop-filter: blur(15px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 12px;
            padding: 30px;
            transition: all 0.3s cubic-bezier(0.25, 0.46, 0.45, 0.94);
            position: relative;
            overflow: hidden;
            text-decoration: none;
            display: block;
        }

        .project-card:hover {
            transform: translateY(-10px);
            border-color: var(--neon-cyan);
            box-shadow: 0 10px 30px rgba(0, 243, 255, 0.1);
        }

        #latest-repo-card {
            height: 180px;
            display: flex;
            flex-direction: column;
        }

        #latest-repo-desc {
            overflow: hidden;
            display: -webkit-box;
            -webkit-line-clamp: 2;
            line-clamp: 2;
            -webkit-box-orient: vertical;
            text-overflow: ellipsis;
            margin-bottom: auto;
        }

        .p-title {
            font-size: 1.5rem;
            color: white;
            margin-bottom: 10px;
            font-weight: bold;
        }

        .p-desc {
            font-size: 0.9rem;
            color: #aaa;
            line-height: 1.6;
            margin-bottom: 20px;
        }

        .tech-tags {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
        }

        .tag {
            font-size: 0.7rem;
            color: var(--neon-cyan);
            border: 1px solid rgba(0, 243, 255, 0.3);
            padding: 4px 10px;
            border-radius: 20px;
        }

        .about-card {
            cursor: default;
        }

        .repo-stack {
            display: flex;
            justify-content: center;
            gap: 15px;
            height: 450px;
            pointer-events: auto;
        }

        .stack-card {
            position: relative;
            flex: 1;
            height: 100%;
            background: rgba(10, 20, 40, 0.3);
            backdrop-filter: blur(15px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 20px;
            transition: flex 0.5s cubic-bezier(0.25, 0.46, 0.45, 0.94), background 0.3s;
            overflow: hidden;
            cursor: pointer;
            display: flex;
            flex-direction: column;
            justify-content: flex-end;
            padding: 30px;
            text-decoration: none;
        }

        .stack-card:hover {
            flex: 4;
            background: rgba(10, 20, 40, 0.5);
            border-color: var(--neon-cyan);
            box-shadow: 0 0 30px rgba(0, 243, 255, 0.1);
        }

        .stack-content {
            opacity: 0;
            transform: translateY(20px);
            transition: all 0.4s ease;
            min-width: 300px;
        }

        .stack-card:hover .stack-content {
            opacity: 1;
            transform: translateY(0);
            transition-delay: 0.2s;
        }

        .stack-title-vertical {
            position: absolute;
            bottom: 60px;
            left: 50%;
            transform: translateX(-50%) rotate(-90deg);
            white-space: nowrap;
            font-weight: bold;
            font-size: 1.2rem;
            color: rgba(255, 255, 255, 0.6);
            letter-spacing: 3px;
            transition: opacity 0.2s;
            pointer-events: none;
        }

        .stack-card:hover .stack-title-vertical {
            opacity: 0;
        }

        .scroll-stack-section {
            position: relative;
            z-index: 10;
            height: 800vh;
            margin-bottom: 50px;
        }

        .scroll-stack-wrapper {
            position: sticky;
            top: 0;
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding-left: 0;
            pointer-events: none;
        }

        .scroll-card {
            position: absolute;
            width: var(--card-width);
            height: var(--card-height);
            background: rgba(10, 20, 40, 0.8);
            backdrop-filter: blur(20px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 1.5vw;
            padding: 3vw 3vw 5vw 3vw;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            color: white;
            box-shadow: 0 10px 40px rgba(0, 0, 0, 0.5);
            transform-origin: top center;
            transition: box-shadow 0.3s, border-color 0.3s, opacity 0.3s, filter 0.3s;
            pointer-events: auto;
        }

        .scroll-card:hover {
            border-color: var(--neon-cyan);
            box-shadow: 0 0 40px rgba(0, 243, 255, 0.2);
        }

        .sc-num {
            font-size: 7vw;
            font-weight: 900;
            color: #ffffff;
            -webkit-text-stroke: 3px #ffffff;
            opacity: 0.05;
            line-height: 0.8;
            margin-left: -1vw;
            margin-bottom: -0.5vw;
        }

        .sc-title {
            font-size: 1.5vw;
            font-weight: bold;
            color: var(--neon-cyan);
            margin-bottom: 1vw;
        }

        .sc-desc {
            font-size: 0.9vw;
            color: #ccc;
            line-height: 1.6;
        }

        .card-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
            padding-bottom: 1vw;
            margin-bottom: 1vw;
            width: 100%;
        }

        .card-header h2 {
            font-size: 1.5vw;
            color: var(--neon-cyan);
            margin: 0;
            font-family: 'Aldrich', sans-serif;
            letter-spacing: 0.1vw;
        }

        .card-header i {
            color: var(--neon-green);
            font-size: 1.2vw;
        }

        .card-body {
            flex-grow: 1;
            color: #ccc;
            font-size: 0.9vw;
            line-height: 1.6;
            font-family: 'Arial', sans-serif;
            display: flex;
            flex-direction: column;
            justify-content: center;
        }

        .card-footer {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-top: 1.5vw;
            font-size: 0.8vw;
            color: #888;
            width: 100%;
            border-top: 1px solid rgba(255, 255, 255, 0.05);
            padding-top: 1vw;
        }

        .social-bar {
            position: fixed;
            left: 50px;
            bottom: 50px;
            z-index: 20;
            display: flex;
            flex-direction: column;
            gap: 15px;
            pointer-events: auto;
        }

        .social-link {
            position: relative;
            width: 45px;
            height: 45px;
            display: flex;
            align-items: center;
            justify-content: flex-start;
            padding-left: 12px;
            gap: 12px;
            color: rgba(255, 255, 255, 0.5);
            font-size: 1.2rem;
            text-decoration: none;
            border-radius: 12px;
            overflow: hidden;
            transition: all 0.4s cubic-bezier(0.25, 0.46, 0.45, 0.94);
            background: transparent;
            border: 1px solid transparent;
        }

        .social-text {
            font-family: 'Aldrich', sans-serif;
            font-size: 0.85rem;
            color: white;
            white-space: nowrap;
            opacity: 0;
            transform: translateX(-10px);
            transition: all 0.3s ease;
            transition-delay: 0.1s;
        }

        .social-link:hover {
            width: 140px;
            color: var(--neon-cyan);
            transform: translateX(5px);
            text-shadow: 0 0 10px var(--neon-cyan);
            background: rgba(10, 20, 40, 0.4);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-left: 1px solid rgba(255, 255, 255, 0.3);
            box-shadow: 0 0 20px rgba(0, 243, 255, 0.1);
        }

        .social-link:hover .social-text {
            opacity: 1;
            transform: translateX(0);
        }
    </style>
</head>

<body>

    <div style="font-family: 'Rajdhani'; font-weight: 900; opacity: 0; position: fixed; pointer-events: none;">.</div>

    <div class="gradient-container" id="bg-orbs">
        <div class="orb orb-1"></div>
        <div class="orb orb-2"></div>
        <div class="orb orb-3"></div>
    </div>
    <div id="particles-container"></div>
    <canvas id="dna-canvas" class="bg-canvas"></canvas>
    <canvas id="network-canvas" class="bg-canvas"></canvas>
    <div class="noise"></div>

    <div id="top-ribbon" class="glass-ribbon">
        <div class="status-container">
            <div class="status-dot"></div>
            AVAILABLE FOR WORK
        </div>
    </div>

    <div class="social-bar">
        <a href="https://github.com/BasudebGorain" class="social-link" target="_blank"><i
                class="fab fa-github"></i><span class="social-text">GitHub</span></a>
        <a href="#" class="social-link"><i class="fab fa-youtube"></i><span class="social-text">YouTube</span></a>
        <a href="#" class="social-link"><i class="fab fa-linkedin-in"></i><span class="social-text">LinkedIn</span></a>
        <a href="mailto:your-email@gmail.com" class="social-link"><i class="fas fa-envelope"></i><span
                class="social-text">Email</span></a>
    </div>


    <canvas id="canvas-back" class="layer"
        style="position: fixed; top: 0; left: 0; width: 100%; height: 100%; pointer-events: none;"></canvas>


    <div class="glass-container">
        <div class="card-wrapper" style="justify-content: center; padding-right: 25%;">
            <div class="glass-card" id="card1" data-drift-x="-1500" data-start-z="-8000">
                <h1>Nexus</h1>
                <p>Exploring the intersection of neural networks and celestial patterns.</p>
                <a href="#" class="btn">Initialize</a>
            </div>
        </div>


        <div class="card-wrapper" style="justify-content: flex-end; padding-right: 10%;">
            <div class="glass-card" id="card2" data-drift-x="-1500">
                <h1>Synapse</h1>
                <p>Bridging the gap between organic chaos and structured algorithms.</p>
                <a href="#" class="btn">Connect</a>
            </div>
        </div>


        <div class="card-wrapper" style="justify-content: flex-start; padding-left: 10%;">
            <div class="glass-card" id="card3" data-drift-x="0">
                <h1>Orbit</h1>
                <p>Gravitational simulations visualized through the lens of glassmorphism.</p>
                <a href="#" class="btn">Launch</a>
            </div>
        </div>


        <div class="card-wrapper" style="justify-content: flex-end; padding-right: 10%;">
            <div class="glass-card" id="card4" data-drift-x="0">
                <h1>Pulse</h1>
                <p>Capturing the rhythmic heartbeat of digital data streams in the void.</p>
                <a href="#" class="btn">Detect</a>
            </div>
        </div>
    </div>


    <div class="projects-section">
        <div class="section-title">/// LATEST RELEASE</div>
        <div class="latest-release-container">
            <a href="#" id="latest-repo-card" class="project-card" style="flex: 1; min-width: 300px;">
                <div class="p-title" id="latest-repo-title">Loading...</div>
                <div class="p-desc" id="latest-repo-desc">Fetching latest repository from GitHub...</div>
                <div class="tech-tags" id="latest-repo-tags">
                    <span class="tag">Loading...</span>
                </div>
            </a>


            <div id="latest-release-btn">
                <div class="main">
                    <div class="card">Project 1</div>
                    <div class="card">Project 2</div>
                    <div class="card">Project 3</div>
                    <div class="card">Project 4</div>
                    <div class="card">Project 5</div>
                    <div class="card">Project 6</div>
                    <div class="card">Project 7</div>
                    <div class="card">Project 8</div>
                    <div class="card">Project 9</div>
                    <p class="text">HOVER<br /><br />TO<br /><br />EXPLORE</p>
                    <div class="main_back"></div>
                </div>
            </div>
        </div>
    </div>

    <div class="projects-section">
        <div class="section-title">/// POPULAR REPOSITORIES</div>
        <div class="repo-stack">
            <a href="#" class="stack-card">
                <div class="stack-title-vertical">NEURAL NET</div>
                <div class="stack-content">
                    <div class="p-title">Neural Net UI</div>
                    <div class="p-desc">Deep learning visualization dashboard. Simulates neural pathways using dynamic
                        SVG strokes.</div>
                    <div class="tech-tags">
                        <span class="tag">Python</span> <span class="tag">React</span> <span class="tag">D3.js</span>
                    </div>
                </div>
            </a>
            <a href="#" class="stack-card">
                <div class="stack-title-vertical">CRYPTO CORE</div>
                <div class="stack-content">
                    <div class="p-title">Crypto Core</div>
                    <div class="p-desc">Decentralized exchange aggregator with real-time websocket updates and
                        neon-glassmorphism aesthetic.</div>
                    <div class="tech-tags">
                        <span class="tag">Solidity</span> <span class="tag">Web3.js</span>
                    </div>
                </div>
            </a>
            <a href="#" class="stack-card">
                <div class="stack-title-vertical">DATA FORGE</div>
                <div class="stack-content">
                    <div class="p-title">Data Forge</div>
                    <div class="p-desc">High-performance data processing pipeline for real-time analytics using WASM.
                    </div>
                    <div class="tech-tags">
                        <span class="tag">Rust</span> <span class="tag">WASM</span>
                    </div>
                </div>
            </a>
        </div>
    </div>
    <div class="scroll-stack-section">
        <div class="scroll-stack-wrapper">
            <div class="scroll-card" id="sc1">
                <div class="sc-num">01</div>
                <div class="card-header">
                    <h2>Architecture</h2>
                    <i class="fas fa-cube"></i>
                </div>
                <div class="card-body">
                    <p>Designing scalable systems with microservices and event-driven architecture. Focusing on
                        robustness and high availability.</p>
                </div>
                <div class="card-footer"><span>Phase 01</span><span>2024</span></div>
            </div>
            <div class="scroll-card" id="sc2">
                <div class="sc-num">02</div>
                <div class="card-header">
                    <h2>Frontend</h2>
                    <i class="fas fa-code"></i>
                </div>
                <div class="card-body">
                    <p>Crafting immersive user experiences using modern frameworks like React, Three.js, and WebGL for
                        high-performance interfaces.</p>
                </div>
                <div class="card-footer"><span>Phase 02</span><span>2024</span></div>
            </div>
            <div class="scroll-card" id="sc3">
                <div class="sc-num">03</div>
                <div class="card-header">
                    <h2>Backend</h2>
                    <i class="fas fa-server"></i>
                </div>
                <div class="card-body">
                    <p>Building secure and efficient APIs. managing databases, and ensuring seamless data flow across
                        the entire stack.</p>
                </div>
                <div class="card-footer"><span>Phase 03</span><span>2025</span></div>
            </div>
            <div class="scroll-card" id="sc4">
                <div class="sc-num">04</div>
                <div class="card-header">
                    <h2>Deployment</h2>
                    <i class="fas fa-rocket"></i>
                </div>
                <div class="card-body">
                    <p>Automated CI/CD pipelines, containerization with Docker, and orchestration using Kubernetes for
                        reliable production releases.</p>
                </div>
                <div class="card-footer"><span>Phase 04</span><span>2025</span></div>
            </div>
        </div>
    </div>

    <div class="projects-section">
        <div class="section-title">/// ABOUT ME</div>
        <div class="about-card">
            <div class="p-desc">Based in West Bengal, I bridge the gap between heavy engineering and fluid design.</div>
            <div style="margin-top: 30px;">
                <div class="p-title" style="font-size: 1rem; color: var(--neon-cyan);">CORE STACK</div>
                <div class="tech-tags"><span class="tag">JavaScript</span><span class="tag">Python</span><span
                        class="tag">Java</span><span class="tag">React</span><span class="tag">Three.js</span></div>
            </div>
        </div>
    </div>
    <div class="projects-section">
        <div class="section-title">/// MISSION CONTROL</div>
        <div class="dashboard-card">
            <div class="mission-control-grid">
                <div class="control-module">
                    <div class="module-header">SIGNAL STRENGTH</div>
                    <div class="module-content">
                        <div class="big-stat neon-yellow">0</div>
                        <div class="stat-label">Current Streak</div>
                        <div class="stat-sub">Feb 8 - Present</div>
                    </div>
                </div>

                <div class="control-module main-module">
                    <div class="module-header">TOTAL OUTPUT</div>
                    <div class="module-content">
                        <div class="big-stat neon-pink">9</div>
                        <div class="stat-label">Total Contributions</div>
                        <div class="stat-sub">Aug 30, 2021 - Present</div>
                    </div>
                    <div class="graph-scroll">
                        <div class="bar" style="height: 30%"></div>
                        <div class="bar" style="height: 50%"></div>
                        <div class="bar" style="height: 20%"></div>
                        <div class="bar" style="height: 70%"></div>
                        <div class="bar" style="height: 40%"></div>
                        <div class="bar" style="height: 90%"></div>
                        <div class="bar" style="height: 60%"></div>
                        <div class="bar" style="height: 30%"></div>
                        <div class="bar" style="height: 80%"></div>
                        <div class="bar" style="height: 50%"></div>
                    </div>
                </div>


                <div class="control-module">
                    <div class="module-header">RECORD HIGH</div>
                    <div class="module-content">
                        <div class="big-stat neon-cyan">1</div>
                        <div class="stat-label">Longest Streak</div>
                        <div class="stat-sub">Aug 29, 2021</div>
                    </div>
                </div>
            </div>

            <div class="system-status">
                <span class="blink">●</span> SYSTEM ONLINE // MONITORING REPOSITORIES
            </div>
        </div>
    </div>

    <style>
        .dashboard-card {
            background: rgba(10, 20, 40, 0.7);
            backdrop-filter: blur(20px);
            -webkit-backdrop-filter: blur(20px);
            border: 1px solid rgba(0, 243, 255, 0.3);
            border-radius: 20px;
            padding: 2vw;
            width: 100%;
            max-width: 1200px;
            margin: 0 auto;
            box-shadow: 0 0 50px rgba(0, 243, 255, 0.15);
            position: relative;
            overflow: hidden;
            display: flex;
            flex-direction: column;
            gap: 2vw;
        }

        .dashboard-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 2px;
            background: linear-gradient(90deg, transparent, var(--neon-cyan), transparent);
            animation: scanline 4s linear infinite;
            z-index: 10;
            pointer-events: none;
        }

        @keyframes scanline {
            0% {
                transform: translateY(0) translateX(-100%);
            }

            50% {
                transform: translateY(0) translateX(100%);
            }

            50.001% {
                transform: translateY(100%) translateX(-100%);
            }

            100% {
                transform: translateY(100%) translateX(100%);
            }
        }

        .mission-control-grid {
            display: grid;
            grid-template-columns: 1fr 2fr 1fr;
            gap: 1.5vw;
        }

        .control-module {
            background: rgba(0, 0, 0, 0.3);
            border: 1px solid rgba(255, 255, 255, 0.05);
            border-radius: 12px;
            padding: 1.5vw;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            position: relative;
            transition: all 0.3s ease;
        }

        .control-module:hover {
            border-color: rgba(255, 255, 255, 0.2);
            box-shadow: 0 0 20px rgba(0, 243, 255, 0.1);
            background: rgba(0, 0, 0, 0.5);
        }

        .module-header {
            font-size: clamp(10px, 0.8vw, 14px);
            letter-spacing: 0.15vw;
            color: rgba(255, 255, 255, 0.5);
            margin-bottom: 1vw;
            font-family: 'Aldrich', sans-serif;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
            padding-bottom: 0.5vw;
        }

        .module-content {
            flex-grow: 1;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
        }

        .big-stat {
            font-family: 'Montserrat', sans-serif;
            font-weight: 900;
            font-size: clamp(2rem, 4vw, 4rem);
            line-height: 1;
            margin-bottom: 0.5vw;
        }

        .neon-yellow {
            color: #F8D847;
            text-shadow: 0 0 20px rgba(248, 216, 71, 0.3);
        }

        .neon-pink {
            color: #FE428E;
            text-shadow: 0 0 20px rgba(254, 66, 142, 0.3);
        }

        .neon-cyan {
            color: #00f3ff;
            text-shadow: 0 0 20px rgba(0, 243, 255, 0.3);
        }

        .stat-label {
            font-size: clamp(10px, 1vw, 16px);
            color: white;
            font-weight: bold;
            margin-bottom: 0.2vw;
        }

        .stat-sub {
            font-size: clamp(8px, 0.7vw, 12px);
            color: rgba(255, 255, 255, 0.5);
        }

        .graph-scroll {
            display: flex;
            align-items: flex-end;
            gap: 0.5vw;
            height: 3vw;
            margin-top: 1vw;
            overflow: hidden;
            mask-image: linear-gradient(90deg, transparent, white 20%, white 80%, transparent);
            -webkit-mask-image: linear-gradient(90deg, transparent, white 20%, white 80%, transparent);
        }

        .bar {
            width: 0.8vw;
            background: linear-gradient(to top, rgba(254, 66, 142, 0.2), rgba(254, 66, 142, 0.8));
            border-radius: 2px;
            animation: pulseBar 2s infinite ease-in-out alternate;
        }

        .bar:nth-child(even) {
            animation-duration: 2.5s;
        }

        .bar:nth-child(3n) {
            animation-duration: 1.8s;
        }

        @keyframes pulseBar {
            0% {
                opacity: 0.5;
                height: 30%;
            }

            100% {
                opacity: 1;
                height: 100%;
            }
        }

        .system-status {
            font-family: 'Consolas', monospace;
            font-size: clamp(10px, 0.8vw, 14px);
            color: var(--neon-green);
            border-top: 1px solid rgba(0, 255, 136, 0.2);
            padding-top: 1vw;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .blink {
            animation: blink 1s infinite;
        }

        @media (max-width: 600px) {
            .mission-control-grid {
                grid-template-columns: 1fr;
                gap: 20px;
            }

            .dashboard-card {
                padding: 20px;
            }

            .module-header {
                font-size: 12px;
                margin-bottom: 10px;
            }

            .big-stat {
                font-size: 3rem;
                margin-bottom: 5px;
            }

            .stat-label {
                font-size: 14px;
            }

            .stat-sub {
                font-size: 10px;
            }

            .graph-scroll {
                height: 40px;
                margin-top: 15px;
            }

            .bar {
                width: 4px;
            }

            .system-status {
                font-size: 10px;
                padding-top: 15px;
            }


        }
    </style>
    <style>
        .big-link {
            font-family: var(--font-syne);
            font-size: 6vw;
            color: white;
            text-decoration: none;
            transition: color 0.3s;
            text-transform: uppercase;
            font-weight: 800;
            line-height: 1;
            cursor: pointer;
        }

        .big-link:hover {
            color: var(--neon-cyan);
        }

        @media (max-width: 768px) {
            .big-link {
                font-size: 15vw;
            }
        }
    </style>

    <section id="contact"
        style="min-height: 60vh; display: flex; flex-direction: column; justify-content: center; align-items: center; position: relative; z-index: 10;">
        <p
            style="font-family: var(--font-aldrich); font-size: 0.9rem; letter-spacing: 4px; color: var(--neon-cyan); margin-bottom: 20px; text-transform: uppercase;">
            Come Join</p>
        <a href="mailto:your-email@example.com" class="big-link">Let's Build.</a>
    </section>

    <footer
        style="height: 20vh; display: flex; justify-content: center; align-items: center; background: #000; border-top: 1px solid rgba(255,255,255,0.1); position: relative; z-index: 10;">
        <p style="color: rgba(255, 255, 255, 0.5); font-family: var(--font-rajdhani); font-size: 0.9rem;">&copy;
            2026-2027
            Basudeb Gorain. All rights reserved.</p>
    </footer>


    <canvas id="scene" class="layer" style="position: fixed;"></canvas>
    <svg class="layer electric-layer" id="electric-svg">
        <g id="static-stroke-group" class="stroke-static"></g>
        <g id="stroke-group" class="stroke-running"></g>
    </svg>
    <svg class="layer solid-layer" id="solid-svg">
        <!-- <defs>
            <linearGradient id="mainGradient" x1="0%" y1="0%" x2="100%" y2="0%">
                <stop offset="0%" style="stop-color:#00f260; stop-opacity:1" />
                <stop offset="100%" style="stop-color:#0575e6; stop-opacity:1" />
            </linearGradient>
        </defs>
        <g id="solid-group" fill="url(#mainGradient)"></g> -->
        <g id="solid-group" fill="white"></g>
    </svg>


    <canvas id="canvas-front"></canvas>


    <div class="cursor-mask-circle" id="cursor-mask"></div>
    <div class="cursor-glow" id="cursor-glow"></div>
    <div class="cursor-main" id="cursor-main"></div>
    <div class="main-subtext" id="main-subtext"></div>
    <div class="scroll-hint" id="scroll-hint">SCROLL TO EXPLORE</div>

    <script>
        const MAIN_TEXT_STRING = "Hey! Nice to see you.";
        const MAIN_TEXT_CONFIG = {
            fontSizeMultiplier: 0.063,
            centered: false,
            staticX: 100,
            staticY: 290,
            offsetY: 0
        };
        const MAIN_FONT_URL = 'https://raw.githubusercontent.com/google/fonts/main/ofl/rajdhani/Rajdhani-Bold.ttf';

        const SUB_TEXT_STRING = "I'm Auro aka Basudeb. Welcome to my page! This is the place where I opensource stuff. I hope you find something useful here. I'm a full stack developer who is passionate about making open source more accessible, creating technology to elevate people and building community. I build digital experiences that blend creativity with code. Let's create something extraordinary together.";
        const SUB_TEXT_CONFIG = {
            fontSize: 14,
            color: 'rgba(255, 255, 255, 0.5)',
            maxWidth: 500,
            offsetY: 40,
            lineHeight: 1.4
        };

        const PARTICLE_CONFIG = {
            text: "WELCOME",
            fontFamily: "Aldrich",
            fontWeight: "900",
            sizeMultiplier: 0.00,//0.06
            fixedFontSize: 0, //50, Fixed size relative to 1920px width
            offsetX: 100,
            offsetY: 0,


            enableFixedPosition: true,
            fixedX: 50,   // Matches ribbon padding-left
            fixedY: 180, // Below the 80px ribbon

            color: 'gradient',


            gradientStart: { r: 0, g: 255, b: 180 },//{ r: 0, g: 120, b: 255 }
            gradientEnd: { r: 0, g: 100, b: 200 },
            pageOffset: 0
        };

        const PARTICLE_CONFIG_SUB = {
            text: "AIMSTECH CODELAB",
            fontFamily: "Aldrich",
            fontWeight: "400",
            sizeMultiplier: 0.07,
            fixedFontSize: 80,
            offsetX: 0,
            offsetY: 0,


            enableFixedPosition: false,

            color: 'gradient',
            gradientStart: { r: 0, g: 200, b: 200 }, // Cyan
            gradientEnd: { r: 0, g: 255, b: 255 },  // White
            pageOffset: 0,
            sticky: true,
            stickySelector: '.glass-container',
            stickyStartOffsetVh: 1.2
        };

        const TEXT_EFFECT_CONFIG = {
            segments: 2,
            dash: 80,
            innerScale: 20,
            speed: 20,
            strokeWidth: 2
        };

        const FIBERS_PER_STRAND = 20;
        const HELIX_RADIUS = 160;

        // Elements
        const canvasParticles = document.getElementById('scene');
        const ctxParticles = canvasParticles.getContext('2d', { willReadFrequently: true });
        const canvasNetwork = document.getElementById('network-canvas');
        const ctxNetwork = canvasNetwork.getContext('2d');
        const canvasDNA = document.getElementById('dna-canvas');
        const ctxDNA = canvasDNA.getContext('2d');

        const electricSvg = document.getElementById('electric-svg');
        const staticStrokeGroup = document.getElementById('static-stroke-group');
        const strokeGroup = document.getElementById('stroke-group');
        const solidSvg = document.getElementById('solid-svg');
        const solidGroup = document.getElementById('solid-group');

        const cursorMaskEl = document.getElementById('cursor-mask');
        const cursorMain = document.getElementById('cursor-main');
        const cursorGlow = document.getElementById('cursor-glow');
        const ribbon = document.getElementById('top-ribbon');
        const bgOrbs = document.getElementById('bg-orbs');
        const domParticlesContainer = document.getElementById('particles-container');
        const scrollHint = document.getElementById('scroll-hint');
        const mainSubtext = document.getElementById('main-subtext');

        let width, height, scrollY = 0;
        let isScrolling = false, scrollTimeout, lastScrollY = 0;
        let particles = [], networkNodes = [], globePoints = [], fibers = [], dnaCloudParticles = [], domParticles = [];
        let mouse = { x: -1000, y: -1000, radius: 150 };
        let normMouse = { x: 0, y: 0 };
        let targetX = 0, targetY = 0;
        let cursorSpring = { x: -100, y: -100, vx: 0, vy: 0, targetX: -100, targetY: -100 };
        const springStiffness = 0.54, springDamping = 0.4;
        let isRightMouseDown = false, globeOpacity = 0, cachedFont = null;
        let lenis, time = 0;


        const PERSPECTIVE = 1000;
        const DEFAULT_MIN_Z = -4000;
        const MAX_Z = 0;
        const cardStates = {
            card1: { triggered: false },
            card2: { triggered: false },
            card3: { triggered: false },
            card4: { triggered: false }
        };


        const HEAD_VERTEX = `
            varying vec2 vUv;
            void main() {
                vUv = uv;
                vec4 mvPosition = modelViewMatrix * vec4(0.0, 0.0, 0.0, 1.0);
                float scaleX = length(modelViewMatrix[0].xyz);
                float scaleY = length(modelViewMatrix[1].xyz);
                mvPosition.x += position.x * scaleX;
                mvPosition.y += position.y * scaleY;
                gl_Position = projectionMatrix * mvPosition;
            }
        `;

        const ELECTRIC_FRAGMENT = `
            uniform float time;
            uniform float uStatic;
            varying vec2 vUv;
            float hash(float n) { return fract(sin(n) * 43758.5453123); }
            void main() {
                vec2 p = vUv - 0.5;
                float r = length(p) * 2.0;
                float noise = hash(time * 60.0);
                float activeFlicker = 0.85 + sin(time * 6.5) * 0.25 + (noise - 0.5) * 3.15;
                float flicker = mix(activeFlicker, 0.95, uStatic);
                float glowAlpha = clamp(0.25 + flicker * 0.05, 0.0, 1.0);
                float glowShape = max(0.0, 1.0 - r);
                vec3 glowColor = vec3(0.55, 0.75, 1.0);
                float coreAlpha = clamp(flicker + 0.2, 0.0, 1.0);
                float coreShape = 1.0 - smoothstep(0.25, 0.35, r);
                vec3 coreColor = vec3(0.9, 0.96, 1.0);
                vec4 glowLayer = vec4(glowColor, glowShape * glowAlpha);
                vec4 coreLayer = vec4(coreColor, coreShape * coreAlpha);
                vec3 finalRgb = mix(glowLayer.rgb, coreLayer.rgb, coreLayer.a);
                float finalAlpha = max(glowLayer.a, coreLayer.a);
                gl_FragColor = vec4(finalRgb, finalAlpha);
            }
        `;

        const LINE_VERTEX = `
            attribute float aSize;
            attribute float aAlpha;
            attribute float aProgress;
            attribute float aColorVar;
            varying float vAlpha;
            varying float vProgress;
            varying float vColorVar;
            uniform float uScreenHeight;
            void main() {
                vAlpha = aAlpha;
                vProgress = aProgress;
                vColorVar = aColorVar;
                vec4 mvPosition = modelViewMatrix * vec4(position, 1.0);
                gl_PointSize = aSize * (uScreenHeight / -mvPosition.z);
                gl_Position = projectionMatrix * mvPosition;
            }
        `;

        const SHEEN_FRAGMENT = `
            varying float vAlpha;
            varying float vProgress;
            uniform float uTime;
            uniform float uSpeed;
            void main() {
                vec2 coord = gl_PointCoord - vec2(0.5);
                float r = length(coord) * 1.5;
                if (r > 1.0) discard;
                float shape = 1.0 - smoothstep(0.1, 0.9, r); 
                float sheen = 0.35 + sin(vProgress * 18.0 - uTime * uSpeed) * 0.25;
                vec3 waveColor = vec3(0.9, 0.96, 1.0); 
                gl_FragColor = vec4(waveColor * sheen, shape * vAlpha * 2.0);
            }
        `;

        class Node {
            constructor(parentGroup, pos) {
                this.position = pos.clone();
                const geo = new THREE.CircleGeometry(0.062, 32);//circle(head) size and segments(resolution)
                const isStatic = Math.random() > 0.2 ? 1.0 : 0.0;
                this.mat = new THREE.ShaderMaterial({
                    transparent: true, depthWrite: false, blending: THREE.NormalBlending,
                    uniforms: { time: { value: 0 }, uStatic: { value: isStatic } },
                    vertexShader: HEAD_VERTEX, fragmentShader: ELECTRIC_FRAGMENT
                });
                this.mesh = new THREE.Mesh(geo, this.mat);
                this.mesh.position.copy(this.position);
                this.mesh.renderOrder = 2;
                parentGroup.add(this.mesh);
            }
            update(time) { this.mat.uniforms.time.value = time; }
        }

        class Connection {
            constructor(parentGroup, start, end, config = {}) {
                const defaults = { baseSize: 0.009, sheenSpeed: 3.5 };//Controls speed of the lines and thickness
                this.config = { ...defaults, ...config };
                const dist = start.distanceTo(end);
                const count = Math.max(5, Math.floor(dist * 160));//number of segments(160-circles in line)
                const geo = new THREE.BufferGeometry();
                const positions = [], sizes = [], alphas = [], progress = [], colorVars = [];
                for (let i = 0; i < count; i++) {
                    const t = i / (count - 1);
                    positions.push(THREE.MathUtils.lerp(start.x, end.x, t), THREE.MathUtils.lerp(start.y, end.y, t), THREE.MathUtils.lerp(start.z, end.z, t));
                    sizes.push(this.config.baseSize);
                    alphas.push(0.2 + Math.random() * 0.3);
                    progress.push(t);
                    colorVars.push(Math.random());
                }
                geo.setAttribute('position', new THREE.Float32BufferAttribute(positions, 3));
                geo.setAttribute('aSize', new THREE.Float32BufferAttribute(sizes, 1));
                geo.setAttribute('aAlpha', new THREE.Float32BufferAttribute(alphas, 1));
                geo.setAttribute('aProgress', new THREE.Float32BufferAttribute(progress, 1));
                geo.setAttribute('aColorVar', new THREE.Float32BufferAttribute(colorVars, 1));
                this.mat = new THREE.ShaderMaterial({
                    transparent: true, depthWrite: false, blending: THREE.AdditiveBlending,
                    uniforms: { uScreenHeight: { value: window.innerHeight }, uTime: { value: 0 }, uSpeed: { value: this.config.sheenSpeed } },
                    vertexShader: LINE_VERTEX, fragmentShader: SHEEN_FRAGMENT
                });
                this.mesh = new THREE.Points(geo, this.mat);
                this.mesh.renderOrder = 1;
                parentGroup.add(this.mesh);
            }
            update(time) { this.mat.uniforms.uTime.value = time; }
            resize(height) { this.mat.uniforms.uScreenHeight.value = height; }
        }

        class ElectricConstellation {
            constructor(scene, options = {}) {
                this.group = new THREE.Group();
                if (options.position) this.group.position.copy(options.position);
                if (options.scale) this.group.scale.setScalar(options.scale);
                if (options.rotation) this.group.rotation.copy(options.rotation);
                scene.add(this.group);
                this.nodes = [];
                this.connections = [];
                this.initClusters();
            }
            randomVec3(range) {
                return new THREE.Vector3((Math.random() - 0.5) * range.x, (Math.random() - 0.5) * range.y, (Math.random() - 0.5) * range.z);
            }
            createLink(n1, n2) {
                const c = new Connection(this.group, n1.position, n2.position, { sheenSpeed: 0.5 + Math.random() * 1.2 });
                this.connections.push(c);
            }
            createCluster(centerPos, type) {
                const clusterNodes = [];
                let count = type === 'triad' ? 3 : type === 'quad' ? 4 : 2;
                for (let i = 0; i < count; i++) {
                    const n = new Node(this.group, centerPos.clone().add(this.randomVec3({ x: 0.5, y: 0.5, z: 0.5 })));
                    clusterNodes.push(n);
                    this.nodes.push(n);
                }
                if (type === 'pair') this.createLink(clusterNodes[0], clusterNodes[1]);
                else if (type === 'triad') { this.createLink(clusterNodes[0], clusterNodes[1]); this.createLink(clusterNodes[1], clusterNodes[2]); }
                else if (type === 'quad') { this.createLink(clusterNodes[0], clusterNodes[1]); this.createLink(clusterNodes[2], clusterNodes[1]); this.createLink(clusterNodes[3], clusterNodes[1]); }
            }
            initClusters() {
                for (let i = 0; i < 4; i++) this.createCluster(this.randomVec3({ x: 0.8, y: 1.5, z: 0.3 }), 'quad');
                for (let i = 0; i < 5; i++) this.createCluster(this.randomVec3({ x: 0.8, y: 1.5, z: 0.3 }), 'triad');
                for (let i = 0; i < 4; i++) this.createCluster(this.randomVec3({ x: 0.8, y: 1.5, z: 0.3 }), 'pair');
                for (let i = 0; i < 4; i++) this.nodes.push(new Node(this.group, this.randomVec3({ x: 0.8, y: 1.5, z: 0.3 })));
            }
            update(time) {
                this.nodes.forEach(n => n.update(time));
                this.connections.forEach(c => c.update(time));
            }
            resize(height) { this.connections.forEach(c => c.resize(height)); }
        }

        class Engine {
            constructor(canvasId, cameraZ, scale, rotationSpeed, parallaxScale, numCards) {
                this.canvas = document.getElementById(canvasId);
                this.renderer = new THREE.WebGLRenderer({ canvas: this.canvas, alpha: true, antialias: true });
                this.renderer.setSize(window.innerWidth, window.innerHeight);
                this.renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
                this.scene = new THREE.Scene();
                this.camera = new THREE.PerspectiveCamera(45, window.innerWidth / window.innerHeight, 0.1, 100);
                this.camera.position.z = cameraZ;
                this.parallaxScale = parallaxScale || 0.3;
                this.rotationSpeed = rotationSpeed;


                this.constellations = [];
                for (let i = 0; i < numCards; i++) {
                    const c = new ElectricConstellation(this.scene, {
                        scale: scale,
                        rotation: new THREE.Euler(Math.random(), Math.random(), 0)
                    });
                    this.constellations.push({
                        instance: c,
                        baseRotationY: c.group.rotation.y
                    });
                }
            }


            updateCamera(deltaTime) {
                this.constellations.forEach(wrapper => {
                    const c = wrapper.instance;
                    wrapper.baseRotationY += this.rotationSpeed * (deltaTime * 60);
                    c.group.rotation.y = wrapper.baseRotationY + (normMouse.x * 0.2);
                    c.group.rotation.x = -normMouse.y * 0.2;
                });

                const targetX = -normMouse.x * this.parallaxScale;
                const targetY = normMouse.y * this.parallaxScale;

                this.camera.position.x += (targetX - this.camera.position.x) * 0.02;
                this.camera.position.y += (targetY - this.camera.position.y) * 0.02;
            }


            render(time) {
                this.constellations.forEach(wrapper => {
                    wrapper.instance.update(time);
                });
                this.renderer.render(this.scene, this.camera);
            }

            onResize() {
                this.camera.aspect = window.innerWidth / window.innerHeight;
                this.camera.updateProjectionMatrix();
                this.renderer.setSize(window.innerWidth, window.innerHeight);
                this.constellations.forEach(w => w.instance.resize(window.innerHeight));
            }
        }


        class Particle {
            constructor(x, y, color, pageOffset = 0, stickyConfig = null) {
                this.x = x;
                this.docY = y + pageOffset;
                this.baseX = x;
                this.stickyConfig = stickyConfig;
                this.size = 2;
                this.color = color;
                this.density = (Math.random() * 15) + 1;

                // Initialize position correctly based on scroll/sticky state
                let effectiveScroll = scrollY;
                if (this.stickyConfig) {
                    const { start, end } = this.stickyConfig;
                    if (scrollY > start && scrollY < end) {
                        effectiveScroll = start;
                    } else if (scrollY >= end) {
                        effectiveScroll = scrollY - (end - start);
                    }
                }
                this.baseY = this.docY - effectiveScroll;
                this.y = this.baseY; // Start at target position to avoid "falling"
            }
            draw() {
                ctxParticles.fillStyle = this.color;
                ctxParticles.beginPath(); ctxParticles.arc(this.x, this.y, this.size, 0, Math.PI * 2); ctxParticles.fill();
            }
            update() {
                let effectiveScroll = scrollY;

                if (this.stickyConfig) {
                    const { start, end } = this.stickyConfig;
                    if (scrollY > start && scrollY < end) {
                        effectiveScroll = start; // Freeze scroll effect
                        // Optional: Add some parallax or slight movement if desired
                    } else if (scrollY >= end) {
                        effectiveScroll = scrollY - (end - start); // Resume scrolling as if section was skipped
                    }
                }

                this.baseY = this.docY - effectiveScroll; // Update base Y based on scroll

                let dx = mouse.x - this.x; let dy = mouse.y - this.y;
                let distance = Math.sqrt(dx * dx + dy * dy);
                if (distance < mouse.radius && !isScrolling) {
                    let force = (mouse.radius - distance) / mouse.radius;
                    let dxForce = (dx / distance) * force * this.density * 1.5;
                    let dyForce = (dy / distance) * force * this.density * 1.5;
                    this.x -= dxForce; this.y -= dyForce;
                } else {
                    if (this.x !== this.baseX) this.x -= (this.x - this.baseX) / 10;
                    if (this.y !== this.baseY) this.y -= (this.y - this.baseY) / 10;
                }
            }
        }

        class DnaFiber {
            constructor(backboneId, fiberIndex, totalFibers) {
                this.backboneId = backboneId; this.fiberIndex = fiberIndex; this.totalFibers = totalFibers;
                this.phaseOffset = (fiberIndex / totalFibers) * Math.PI * 2;
                this.thickness = Math.random() * 0.8 + 0.2;
            }
        }

        class DnaCloudParticle {
            constructor() {
                this.tOffset = Math.random() * 30 - 10; this.backboneId = Math.random() > 0.5 ? 1 : 0;
                this.radialOffset = Math.random() * 20 + 5; this.thetaOffset = Math.random() * Math.PI * 2;
                this.size = Math.random() * 3 + 0.2; this.blinkSpeed = Math.random() * 0.02 + 0.005;
                this.blinkPhase = Math.random() * Math.PI * 2;
            }
        }

        class NetworkNode {
            constructor() {
                this.x = Math.random() * width; this.y = Math.random() * height;
                this.vx = (Math.random() - 0.5) * 0.5; this.vy = (Math.random() - 0.5) * 0.5;
                this.size = Math.random() > 0.8 ? Math.random() * 3 + 2 : Math.random() * 1.5 + 0.5;
                this.color = Math.random() > 0.9 ? '#ffffff' : '#00f3ff';
                this.pulseFactor = Math.random() * 0.05 + 0.02; this.pulseOffset = Math.random() * Math.PI * 2;
            }
            update() {
                this.x += this.vx; this.y += this.vy;
                if (this.x < 0 || this.x > width) this.vx *= -1;
                if (this.y < 0 || this.y > height) this.vy *= -1;
            }
            draw(ctx, time, mouseX, mouseY) {
                const dx = this.x - mouseX; const dy = this.y - mouseY;
                const dist = Math.sqrt(dx * dx + dy * dy);
                if (dist > 300) return;
                const visibility = 1 - (dist / 300);
                const pulse = Math.sin(time * this.pulseFactor + this.pulseOffset);
                ctx.beginPath(); ctx.arc(this.x, this.y, Math.max(0, this.size + pulse), 0, Math.PI * 2);
                ctx.fillStyle = this.color; ctx.globalAlpha = 0.5 * (visibility * visibility); ctx.fill();
            }
        }


        function init() {
            width = window.innerWidth;
            height = window.innerHeight;

            if (width <= 0 || height <= 0) { setTimeout(init, 100); return; }


            canvasParticles.width = canvasNetwork.width = canvasDNA.width = width;
            canvasParticles.height = canvasNetwork.height = canvasDNA.height = height;


            electricSvg.setAttribute('viewBox', `0 0 ${width} ${height}`);
            solidSvg.setAttribute('viewBox', `0 0 ${width} ${height}`);


            mouse.radius = (width < 768) ? 80 : 100;
            initNetwork(); initGlobe(); initDNA(); initDomParticles();

            if (!engineBack) initEngines();
            updateScrollDepth();

            if (engineBack) engineBack.onResize();
            if (engineFront) engineFront.onResize();

            if (cachedFont) {
                generateAllLayers(cachedFont);
                updateSubText();
                setTimeout(() => {
                    if (mainSubtext) mainSubtext.classList.add('visible');
                }, 1000);
            } else {
                opentype.load(MAIN_FONT_URL, (err, font) => {
                    if (!err) {
                        cachedFont = font;
                        generateAllLayers(font);
                        updateSubText();
                        setTimeout(() => {
                            if (mainSubtext) mainSubtext.classList.add('visible');
                        }, 1000);
                    }
                });
            }
        }

        function updateSubText() {
            if (!mainSubtext) return;
            mainSubtext.innerHTML = SUB_TEXT_STRING;
            mainSubtext.style.position = 'absolute';
            mainSubtext.style.color = SUB_TEXT_CONFIG.color;
            mainSubtext.style.fontSize = `${SUB_TEXT_CONFIG.fontSize}px`;
            mainSubtext.style.fontFamily = "'Outfit', sans-serif";
            mainSubtext.style.fontWeight = "300";
            mainSubtext.style.maxWidth = `${SUB_TEXT_CONFIG.maxWidth}px`;
            mainSubtext.style.lineHeight = SUB_TEXT_CONFIG.lineHeight;
            mainSubtext.style.zIndex = '4';
            mainSubtext.style.pointerEvents = 'none';
            // mainSubtext.style.textShadow = '0 0 10px rgba(0, 243, 255, 0.3)';

            // Calculate position based on MAIN_TEXT_CONFIG
            let x, y;
            if (MAIN_TEXT_CONFIG.centered) {
                x = (width / 2) - (SUB_TEXT_CONFIG.maxWidth / 2);
                y = (height / 2) + MAIN_TEXT_CONFIG.offsetY + SUB_TEXT_CONFIG.offsetY;
                mainSubtext.style.textAlign = 'center';
            } else {
                x = MAIN_TEXT_CONFIG.staticX;
                y = MAIN_TEXT_CONFIG.staticY + SUB_TEXT_CONFIG.offsetY;
                mainSubtext.style.textAlign = 'left';
            }

            mainSubtext.style.left = `${x}px`;
            mainSubtext.style.top = `${y}px`;
        }

        function generateAllLayers(font) {
            const scaleFactor = width / 1440;
            // const scaledStrokeWidth = Math.max(1, TEXT_EFFECT_CONFIG.strokeWidth * scaleFactor);
            const fontSize = width * MAIN_TEXT_CONFIG.fontSizeMultiplier;
            const path = getTextPath(font, MAIN_TEXT_STRING, fontSize);
            const pathData = path.toPathData(2);


            solidGroup.innerHTML = '';
            const solidPath = document.createElementNS("http://www.w3.org/2000/svg", "path");
            solidPath.setAttribute("d", pathData);
            // solidPath.setAttribute("stroke", "url(#mainGradient)");
            solidPath.setAttribute("stroke", "white");
            solidPath.setAttribute("stroke-width", "3");
            solidPath.setAttribute("stroke-linejoin", "round");
            solidPath.setAttribute("stroke-linecap", "round");
            solidGroup.appendChild(solidPath);


            staticStrokeGroup.innerHTML = '';
            const staticPath = document.createElementNS("http://www.w3.org/2000/svg", "path");
            staticPath.setAttribute("d", pathData);
            staticStrokeGroup.appendChild(staticPath);


            strokeGroup.innerHTML = '';
            // document.documentElement.style.setProperty('--stroke-width', `${TEXT_EFFECT_CONFIG.strokeWidth}px`);
            const contours = splitPathIntoContours(path.commands);
            const processed = analyzeContours(contours);
            processed.forEach(item => {
                const p = document.createElementNS("http://www.w3.org/2000/svg", "path");
                p.setAttribute("d", item.d);
                strokeGroup.appendChild(p);
                applyFixedCountAnimation(p, item.isInner, scaleFactor);
            });

            initParticleLayers();
        }

        async function initParticleLayers() {

            const particles1 = await createParticlesFromConfig(PARTICLE_CONFIG);
            const particles2 = await createParticlesFromConfig(PARTICLE_CONFIG_SUB);


            particles = [...particles1, ...particles2];
        }

        async function createParticlesFromConfig(config) {

            const tempCanvas = document.createElement('canvas');
            tempCanvas.width = width;
            tempCanvas.height = height;
            const tempCtx = tempCanvas.getContext('2d', { willReadFrequently: true });


            let pSize;
            if (config.fixedFontSize) {
                pSize = config.fixedFontSize;
            } else {
                pSize = Math.floor(width * config.sizeMultiplier);
            }
            const fontSpec = `${config.fontWeight} ${pSize}px "${config.fontFamily}"`;


            try {
                await document.fonts.load(fontSpec);
            } catch (e) {
                console.warn("Font loading check failed, attempting render anyway", e);
            }

            tempCtx.font = fontSpec;


            let xPos, yPos;
            if (config.enableFixedPosition) {
                xPos = config.fixedX;
                yPos = config.fixedY;
                tempCtx.textAlign = 'left';
            } else {
                xPos = (width / 2) + config.offsetX;
                yPos = (height / 2) + config.offsetY;
                tempCtx.textAlign = 'center';
            }

            tempCtx.textBaseline = 'middle';
            tempCtx.fillStyle = 'white';

            tempCtx.fillText(config.text, xPos, yPos);

            const textMetrics = tempCtx.measureText(config.text);
            const textWidth = textMetrics.width;
            let textStartX;

            if (config.enableFixedPosition) {
                textStartX = xPos;
            } else {
                textStartX = xPos - (textWidth / 2);
            }



            let stickyConfig = null;
            if (config.sticky && config.stickySelector) {
                const el = document.querySelector(config.stickySelector);
                if (el) {
                    const rect = el.getBoundingClientRect();
                    const scrollTop = window.scrollY || document.documentElement.scrollTop;
                    const start = rect.top + scrollTop - (height / 2) + config.offsetY;
                    // Adjust start to be when element is centered or as needed. 
                    // stickyConfig = { start: rect.top + scrollTop, end: rect.bottom + scrollTop - height };

                    let stickyStartOffset = 0;
                    if (config.stickyStartOffsetVh) {
                        stickyStartOffset = height * config.stickyStartOffsetVh;
                    }

                    stickyConfig = {
                        start: rect.top + scrollTop + stickyStartOffset,
                        end: rect.bottom + scrollTop - height
                    };


                }
            }


            const newParticles = [];
            const effectivePageOffset = stickyConfig ? stickyConfig.start : (config.pageOffset || 0);

            const gap = 4;
            try {
                const data = tempCtx.getImageData(0, 0, width, height);
                for (let y = 0; y < height; y += gap) {
                    for (let x = 0; x < width; x += gap) {

                        if (data.data[(y * 4 * width) + (x * 4) + 3] > 128) {
                            let pColor;

                            if (config.color === 'gradient') {

                                let normalizedX = (x - textStartX) / textWidth;
                                normalizedX = Math.max(0, Math.min(1, normalizedX));


                                const start = config.gradientStart;
                                const end = config.gradientEnd;

                                const r = Math.floor(start.r + (end.r - start.r) * normalizedX);
                                const g = Math.floor(start.g + (end.g - start.g) * normalizedX);
                                const b = Math.floor(start.b + (end.b - start.b) * normalizedX);

                                pColor = `rgb(${r},${g},${b})`;
                            } else {
                                pColor = config.color;
                            }

                            newParticles.push(new Particle(x, y, pColor, effectivePageOffset, stickyConfig));
                        }
                    }
                }
            } catch (error) {
                console.warn("Canvas data extraction failed:", error);
            }


            return newParticles;
        }


        function getTextPath(font, text, fontSize) {
            const temp = font.getPath(text, 0, 0, fontSize);
            const bbox = temp.getBoundingBox();

            let x, y;
            if (MAIN_TEXT_CONFIG.centered) {
                x = (width - (bbox.x2 - bbox.x1)) / 2 - bbox.x1;
                y = (height / 2) + ((bbox.y2 - bbox.y1) / 2) - bbox.y2;
            } else {
                x = MAIN_TEXT_CONFIG.staticX;
                y = MAIN_TEXT_CONFIG.staticY;
            }

            y += MAIN_TEXT_CONFIG.offsetY;

            return font.getPath(text, x, y, fontSize);
        }

        function splitPathIntoContours(commands) {
            let contours = [], current = [];
            commands.forEach(cmd => { if (cmd.type === 'M' && current.length) { contours.push(current); current = []; } current.push(cmd); });
            if (current.length) contours.push(current);
            return contours;
        }

        function analyzeContours(contours) {
            const meta = contours.map(cmds => ({ cmds, area: calculateSignedArea(cmds) }));
            const maxArea = Math.max(...meta.map(m => Math.abs(m.area)));
            const dominantSign = Math.sign(meta.find(m => Math.abs(m.area) === maxArea).area);
            return meta.map(m => {
                const path = new opentype.Path();
                m.cmds.forEach(c => {
                    if (c.type === 'M') path.moveTo(c.x, c.y);
                    else if (c.type === 'L') path.lineTo(c.x, c.y);
                    else if (c.type === 'Q') path.quadraticCurveTo(c.x1, c.y1, c.x, c.y);
                    else if (c.type === 'C') path.curveTo(c.x1, c.y1, c.x2, c.y2, c.x, c.y);
                    else if (c.type === 'Z') path.close();
                });
                return { d: path.toPathData(2), isInner: Math.sign(m.area) !== dominantSign };
            });
        }

        function calculateSignedArea(cmds) {
            let area = 0, x = 0, y = 0;
            cmds.forEach(c => {
                let nx = (c.type === 'Z') ? 0 : c.x, ny = (c.type === 'Z') ? 0 : c.y;
                area += (x * ny - nx * y); x = nx; y = ny;
            });
            return area / 2;
        }

        function applyFixedCountAnimation(el, isInner, scale) {
            const length = el.getTotalLength(); if (!length) return;
            let dash = TEXT_EFFECT_CONFIG.dash * scale;
            const seg = length / TEXT_EFFECT_CONFIG.segments;
            if (isInner) dash *= (TEXT_EFFECT_CONFIG.innerScale / 100);
            if (dash >= seg * 0.6) dash = seg * 0.6;
            el.style.strokeDasharray = `${dash} ${seg - dash}`;
            el.animate([{ strokeDashoffset: 0 }, { strokeDashoffset: -seg }], { duration: (seg / TEXT_EFFECT_CONFIG.speed) * 1000, iterations: Infinity, easing: 'linear' });
        }


        function initNetwork() { networkNodes = []; for (let i = 0; i < 100; i++) networkNodes.push(new NetworkNode()); }
        function initDNA() {
            fibers = []; dnaCloudParticles = [];
            for (let i = 0; i < FIBERS_PER_STRAND; i++) { fibers.push(new DnaFiber(0, i, FIBERS_PER_STRAND)); fibers.push(new DnaFiber(1, i, FIBERS_PER_STRAND)); }
            for (let i = 0; i < 800; i++) dnaCloudParticles.push(new DnaCloudParticle());
        }
        function initGlobe() {
            globePoints = [];
            for (let i = 0; i < 100; i++) {
                const u = Math.random(), v = Math.random();
                globePoints.push({
                    baseX: 60 * Math.sin(Math.acos(2 * v - 1)) * Math.cos(2 * Math.PI * u),
                    baseY: 60 * Math.sin(Math.acos(2 * v - 1)) * Math.sin(2 * Math.PI * u),
                    baseZ: 60 * (2 * v - 1),
                    size: Math.random() * 2 + 1,
                    blinkPhase: Math.random() * Math.PI * 2, blinkSpeed: Math.random() * 0.05 + 0.02,
                    wobbleSpeed: Math.random() * 0.02 + 0.01, wobbleRange: Math.random() * 2 + 0.5, wobbleOffset: Math.random() * 100
                });
            }
        }
        function initDomParticles() {
            domParticles = []; domParticlesContainer.innerHTML = '';
            for (let i = 0; i < 100; i++) {
                const p = document.createElement('div'); p.classList.add('particle-bokeh');
                const isBokeh = Math.random() > 0.4;
                const size = isBokeh ? Math.random() * 20 + 10 : Math.random() * 3 + 1;
                const opacity = isBokeh ? Math.random() * 0.15 + 0.05 : Math.random() * 0.5 + 0.3;
                p.style.width = `${size}px`; p.style.height = `${size}px`;
                p.style.left = `${Math.random() * 100}%`; p.style.top = `${Math.random() * 100}%`;
                p.style.setProperty('--target-opacity', opacity);
                p.style.filter = `blur(${isBokeh ? Math.random() * 6 + 4 : Math.random() * 1}px)`;
                p.style.animation = `floatUp ${Math.random() * 20 + 10}s ${Math.random() * 10}s infinite ease-in-out`;
                domParticles.push({ element: p, factor: Math.random() * 20 + 5 });
                domParticlesContainer.appendChild(p);
            }
        }


        function drawDNA(time, currentScroll = 0) {
            ctxDNA.clearRect(0, 0, width, height);
            ctxDNA.globalCompositeOperation = 'lighter';
            const cx = width / 2, cy = height / 2;
            const effectiveScroll = (window.scrollY || currentScroll);
            const phase = time * 0.2 + effectiveScroll * 0.003;
            const spin = time * 0.5, rotAngle = Math.PI / 4;

            function project(x, y, z) {
                let rx = x * Math.cos(rotAngle) - y * Math.sin(rotAngle), ry = x * Math.sin(rotAngle) + y * Math.cos(rotAngle);
                let sc = 1000 / (1000 + z); return { x: cx + rx * sc - 300, y: cy + ry * sc - 300 };
            }

            fibers.forEach(f => {
                ctxDNA.beginPath(); let started = false;
                for (let t = -8; t < 18; t += 0.1) {
                    let angle = (t + phase) + (f.backboneId * Math.PI) + spin;
                    let y = Math.sin(angle) * HELIX_RADIUS + Math.sin((t + phase) * 2 + f.phaseOffset) * 15;
                    let z = Math.cos(angle) * HELIX_RADIUS + Math.cos((t + phase) * 2 + f.phaseOffset) * 15;
                    let p = project(t * 150, y, z);
                    let dist = Math.sqrt((p.x - cx) ** 2 + (p.y - cy) ** 2);
                    let alpha = 1 - Math.pow(dist / (Math.sqrt((width / 2) ** 2 + (height / 2) ** 2) * 0.7), 2);
                    if (alpha > 0) { if (!started) { ctxDNA.moveTo(p.x, p.y); started = true; } else ctxDNA.lineTo(p.x, p.y); }
                    else if (started) { ctxDNA.stroke(); ctxDNA.beginPath(); started = false; }
                }
                if (started) ctxDNA.stroke();
                const grad = ctxDNA.createLinearGradient(0, 0, width, height);
                grad.addColorStop(0, "rgba(0,243,255,0)"); grad.addColorStop(0.2, "rgba(0,243,255,0)");
                grad.addColorStop(0.5, "rgba(0,243,255,0.3)"); grad.addColorStop(0.8, "rgba(0,243,255,0)");
                ctxDNA.strokeStyle = grad; ctxDNA.lineWidth = f.thickness; ctxDNA.stroke();
            });


            const RUNG_SPACING = 0.4;
            for (let s = Math.ceil((phase - 12) / RUNG_SPACING); s <= Math.floor((phase + 20) / RUNG_SPACING); s++) {
                let angle = (s * RUNG_SPACING) + spin, xBase = (s * RUNG_SPACING - phase) * 150;
                let y1 = Math.sin(angle) * HELIX_RADIUS, z1 = Math.cos(angle) * HELIX_RADIUS;
                let y2 = Math.sin(angle + Math.PI) * HELIX_RADIUS, z2 = Math.cos(angle + Math.PI) * HELIX_RADIUS;
                for (let k = 0; k < 12; k++) {
                    let seed = s * 100 + k;
                    let pS = project(xBase, y1 + Math.sin(seed) * 20, z1 + Math.cos(seed) * 20);
                    let pE = project(xBase, y2 + Math.sin(seed + 1) * 20, z2 + Math.cos(seed + 1) * 20);
                    let pC1 = project(xBase + Math.sin(seed * 0.15) * 40, (y1 + y2) / 2 + Math.sin(seed * 0.1) * 60, (z1 + z2) / 2 + Math.cos(seed * 0.12) * 60);
                    let pC2 = project(xBase + Math.cos(seed * 0.25) * 40, (y1 + y2) / 2 + Math.cos(seed * 0.2) * 60, (z1 + z2) / 2 + Math.sin(seed * 0.22) * 60);
                    let dist = Math.sqrt((pC1.x - cx) ** 2 + (pC1.y - cy) ** 2);
                    let alpha = 1 - Math.pow(dist / (Math.sqrt((width / 2) ** 2 + (height / 2) ** 2) * 0.7), 2);
                    if (alpha > 0) {
                        ctxDNA.beginPath(); ctxDNA.moveTo(pS.x, pS.y); ctxDNA.bezierCurveTo(pC1.x, pC1.y, pC2.x, pC2.y, pE.x, pE.y);
                        ctxDNA.strokeStyle = `rgba(0, 243, 255, ${alpha * 0.15})`; ctxDNA.stroke();
                        for (let m = 0; m < 2; m++) {
                            let fT = (time * (0.01 + (k % 3) * 0.005) + seed * 0.1 + m * 0.5) % 1, iT = 1 - fT;
                            let bx = iT ** 3 * pS.x + 3 * iT ** 2 * fT * pC1.x + 3 * iT * fT ** 2 * pC2.x + fT ** 3 * pE.x;
                            let by = iT ** 3 * pS.y + 3 * iT ** 2 * fT * pC1.y + 3 * iT * fT ** 2 * pC2.y + fT ** 3 * pE.y;
                            ctxDNA.beginPath(); ctxDNA.arc(bx, by, 0.8 + Math.abs(Math.sin(seed + m)), 0, Math.PI * 2); ctxDNA.fillStyle = `rgba(255,255,255,${alpha * 0.8})`; ctxDNA.fill();
                        }
                    }
                }
            }
            dnaCloudParticles.forEach(p => {
                let T = p.tOffset + phase;
                let proj = project(p.tOffset * 150, Math.sin(T + p.backboneId * Math.PI) * HELIX_RADIUS + Math.sin(p.thetaOffset) * p.radialOffset, Math.cos(T + p.backboneId * Math.PI) * HELIX_RADIUS + Math.cos(p.thetaOffset) * p.radialOffset);
                let alpha = 1 - Math.pow(Math.sqrt((proj.x - cx) ** 2 + (proj.y - cy) ** 2) / (Math.sqrt((width / 2) ** 2 + (height / 2) ** 2) * 0.7), 2);
                if (alpha > 0) {
                    ctxDNA.beginPath(); ctxDNA.arc(proj.x, proj.y, p.size * (1000 / (1000 + Math.cos(T + p.backboneId * Math.PI) * HELIX_RADIUS)), 0, Math.PI * 2);
                    ctxDNA.fillStyle = `rgba(0, 243, 255, ${alpha * (0.3 + (Math.sin(time * p.blinkSpeed + p.blinkPhase) + 1) * 0.35) * 0.8})`; ctxDNA.fill();
                }
            });
            ctxDNA.globalCompositeOperation = 'source-over';
        }

        function drawConnections(time, mx, my) {
            for (let a = 0; a < networkNodes.length; a++) {
                const nA = networkNodes[a]; const dA = Math.hypot(nA.x - mx, nA.y - my);
                if (dA > 300) continue;
                for (let b = a + 1; b < networkNodes.length; b++) {
                    const nB = networkNodes[b]; const dAB = Math.hypot(nA.x - nB.x, nA.y - nB.y);
                    if (dAB < 150) {
                        const alpha = (1 - dAB / 150) * (1 - dA / 300) * 0.4;
                        ctxNetwork.strokeStyle = `rgba(0, 243, 255, ${alpha})`; ctxNetwork.lineWidth = 1; ctxNetwork.beginPath(); ctxNetwork.moveTo(nA.x, nA.y); ctxNetwork.lineTo(nB.x, nB.y); ctxNetwork.stroke();
                    }
                }
            }
        }


        function updateScrollStack(scroll) {
            const stackSection = document.querySelector('.scroll-stack-section');
            const scrollCards = document.querySelectorAll('.scroll-card');

            if (!stackSection) return;
            const sectionTop = stackSection.offsetTop;
            const sectionH = stackSection.offsetHeight;
            const viewH = window.innerHeight;

            let progress = (scroll - sectionTop) / (sectionH - viewH);
            progress = Math.max(0, Math.min(1, progress));

            const totalCards = scrollCards.length;

            scrollCards.forEach((card, index) => {
                let t = (progress - ((index - 1) * 0.25)) / 0.25;
                if (index === 0) t = 1;
                t = Math.max(0, Math.min(1, t));
                let easeT = 1 - Math.pow(1 - t, 3);

                let startY = viewH;
                let endY = index * 40;
                let y = startY - (startY - endY) * easeT;


                let scale = 1;
                let opacity = 1;
                let blur = 0;
                let brightness = 1;
                let cardsOnTop = (progress * totalCards) - index;
                if (cardsOnTop > 0) {
                    scale = 1 - (cardsOnTop * 0.15);
                    scale = Math.max(0.4, scale);


                    opacity = 1 - (cardsOnTop * 0.3);
                    blur = cardsOnTop * 5;
                    brightness = 1 - (cardsOnTop * 0.2);
                }

                card.style.zIndex = index + 1;
                card.style.transform = `translateY(${y}px) scale(${scale})`;
                card.style.opacity = Math.max(0, opacity);
                card.style.filter = `blur(${blur}px) brightness(${brightness})`;
            });
        }


        function updateScrollDepth() {
            const viewportCenter = window.innerHeight / 2;
            const viewportHeight = window.innerHeight;

            const wrappers = document.querySelectorAll('.card-wrapper');
            wrappers.forEach(wrapper => {
                const rect = wrapper.getBoundingClientRect();
                const wrapperCenter = rect.top + rect.height / 2;
                const card = wrapper.querySelector('.glass-card');

                const dist = wrapperCenter - viewportCenter;
                let progress = 1 - (dist / (viewportHeight * 1.0));
                progress = Math.max(0, Math.min(1, progress));

                const localMinZ = parseFloat(card.dataset.startZ) || DEFAULT_MIN_Z;
                const currentZ = localMinZ + (MAX_Z - localMinZ) * progress;
                const startDrift = parseFloat(card.dataset.driftX || 0);
                const currentDrift = startDrift * (1 - progress);

                card.style.transform = `translate3d(${currentDrift}px, 0, ${currentZ}px)`;

                const id = card.id;
                if (cardStates[id].triggered) {
                    card.style.opacity = 1;
                } else {
                    if (progress > 0.90) {
                        card.classList.add('activate-glitch');
                        cardStates[id].triggered = true;
                        card.style.opacity = 1;
                    } else {
                        card.style.opacity = 0;
                    }
                }
                card.dataset.zDepth = currentZ;
            });
        }

        let engineBack, engineFront;
        function initEngines() {
            engineBack = new Engine('canvas-back', 6, 1.2, 0.0006, 0.4, 4);
            engineFront = new Engine('canvas-front', 3, 0.7, 0.0009, 0.8, 4);
        }

        function syncToElement(engine, constellationIndex, elementX, elementY) {
            const ndcX = (elementX / window.innerWidth) * 2 - 1;
            const ndcY = -(elementY / window.innerHeight) * 2 + 1;
            const vector = new THREE.Vector3(ndcX, ndcY, 0.5);
            vector.unproject(engine.camera);
            vector.sub(engine.camera.position).normalize();
            const distance = -engine.camera.position.z / vector.z;
            const pos = engine.camera.position.clone().add(vector.multiplyScalar(distance));

            engine.constellations[constellationIndex].instance.group.position.set(pos.x, pos.y, 0);
        }

        function animate(rafTime) {
            time++;
            if (lenis) {
                lenis.raf(rafTime);
                scrollY = lenis.scroll;
            } else {
                scrollY = window.scrollY;
            }

            if (Math.abs(scrollY - lastScrollY) > 0.5) {
                isScrolling = true;
                clearTimeout(scrollTimeout);
                scrollTimeout = setTimeout(() => { isScrolling = false; }, 100);
            }
            lastScrollY = scrollY;

            if (scrollY > 50) {
                ribbon.classList.add('hidden-ribbon');
                scrollHint.classList.add('hidden-hint');
            } else {
                ribbon.classList.remove('hidden-ribbon');
                scrollHint.classList.remove('hidden-hint');
            }

            updateScrollDepth();
            updateScrollStack(scrollY);

            const ax = (cursorSpring.targetX - cursorSpring.x) * springStiffness;
            const ay = (cursorSpring.targetY - cursorSpring.y) * springStiffness;
            cursorSpring.vx = (cursorSpring.vx + ax) * springDamping; cursorSpring.vy = (cursorSpring.vy + ay) * springDamping;
            cursorSpring.x += cursorSpring.vx; cursorSpring.y += cursorSpring.vy;

            cursorMain.style.transform = `translate(${cursorSpring.x}px, ${cursorSpring.y}px) translate(-50%, -50%)`;
            cursorGlow.style.transform = `translate(${cursorSpring.x}px, ${cursorSpring.y}px) translate(-50%, -50%)`;
            cursorMaskEl.style.transform = `translate3d(${mouse.x}px, ${mouse.y}px, 0)`;

            const rect = solidSvg.getBoundingClientRect();
            solidSvg.style.setProperty('--mask-x', (mouse.x - rect.left) + 'px');
            solidSvg.style.setProperty('--mask-y', (mouse.y - rect.top) + 'px');

            targetX += (normMouse.x - targetX) * 0.05; targetY += (normMouse.y - targetY) * 0.05;
            bgOrbs.style.transform = `translate(${targetX * -30}px, ${targetY * -30}px)`;
            domParticles.forEach(p => { p.element.style.marginLeft = `${targetX * p.factor}px`; p.element.style.marginTop = `${targetY * p.factor}px`; });

            ctxParticles.clearRect(0, 0, width, height);
            particles.forEach(p => { p.draw(); p.update(); });

            drawDNA(time * 0.02, scrollY);
            ctxNetwork.clearRect(0, 0, width, height);
            networkNodes.forEach(n => { n.update(); n.draw(ctxNetwork, time, cursorSpring.x, cursorSpring.y); });
            drawConnections(time, cursorSpring.x, cursorSpring.y);

            const t = rafTime * 0.001;
            const dt = 0.016;

            if (engineBack && engineFront) {
                engineBack.updateCamera(dt);
                engineFront.updateCamera(dt);
                const cards = document.querySelectorAll('.glass-card');
                cards.forEach((card, index) => {
                    const rect = card.getBoundingClientRect();


                    const targetX = rect.left;
                    const targetY = rect.top + rect.height / 2;


                    syncToElement(engineBack, index, targetX, targetY);
                    syncToElement(engineFront, index, targetX, targetY);

                    const zDepth = parseFloat(card.dataset.zDepth || DEFAULT_MIN_Z);


                    const scaleFactor = (PERSPECTIVE / (PERSPECTIVE - zDepth)) * 0.55;

                    engineBack.constellations[index].instance.group.scale.setScalar(scaleFactor);
                    engineFront.constellations[index].instance.group.scale.setScalar(scaleFactor);
                });

                engineBack.render(t);
                engineFront.render(t);
            }

            requestAnimationFrame(animate);
        }


        window.addEventListener('mousemove', e => {
            mouse.x = e.clientX; mouse.y = e.clientY;
            cursorSpring.targetX = e.clientX; cursorSpring.targetY = e.clientY;
            normMouse.x = (e.clientX / width) * 2 - 1; normMouse.y = (e.clientY / height) * 2 - 1;
        });
        window.addEventListener('touchmove', e => {
            e.preventDefault();
            mouse.x = e.touches[0].clientX; mouse.y = e.touches[0].clientY;
            cursorSpring.targetX = mouse.x; cursorSpring.targetY = mouse.y;
        }, { passive: false });

        // Disable inspect element and source view shortcuts
        document.addEventListener('contextmenu', e => e.preventDefault());
        document.addEventListener('keydown', e => {
            if (e.key === 'F12' || e.keyCode === 123) {
                e.preventDefault();
            }
            if (e.ctrlKey && e.shiftKey && ['I', 'i', 'C', 'c', 'J', 'j'].includes(e.key)) {
                e.preventDefault();
            }
            if (e.ctrlKey && ['U', 'u', 'S', 's', 'V', 'v'].includes(e.key)) {
                e.preventDefault();
            }
        });

        async function fetchLatestGitHubRepo() {
            try {
                const response = await fetch('https://api.github.com/users/BasudebGorain/repos?sort=updated&per_page=10');
                if (!response.ok) throw new Error('Failed to fetch repositories');

                const repos = await response.json();
                if (repos && repos.length > 0) {
                    const latestRepo = repos[0];

                    document.getElementById('latest-repo-card').href = latestRepo.html_url;
                    document.getElementById('latest-repo-title').textContent = latestRepo.name;
                    document.getElementById('latest-repo-desc').textContent = latestRepo.description || 'No description available for this repository.';

                    const tagsContainer = document.getElementById('latest-repo-tags');
                    tagsContainer.innerHTML = '';

                    if (latestRepo.language) {
                        const langTag = document.createElement('span');
                        langTag.className = 'tag';
                        langTag.textContent = latestRepo.language;
                        tagsContainer.appendChild(langTag);
                    }

                    if (latestRepo.topics && latestRepo.topics.length > 0) {
                        latestRepo.topics.slice(0, 3).forEach(topic => {
                            const topicTag = document.createElement('span');
                            topicTag.className = 'tag';
                            topicTag.textContent = topic;
                            tagsContainer.appendChild(topicTag);
                        });
                    }

                    // Update the 9 project cards on the right
                    const projectCards = document.querySelectorAll('#latest-release-btn .main .card');
                    for (let i = 0; i < projectCards.length; i++) {
                        if (repos[i + 1]) {
                            projectCards[i].textContent = repos[i + 1].name;
                            projectCards[i].onclick = () => window.open(repos[i + 1].html_url, '_blank');
                            projectCards[i].title = repos[i + 1].description || repos[i + 1].name;
                        } else {
                            projectCards[i].textContent = 'Coming Soon';
                            projectCards[i].onclick = null;
                            projectCards[i].title = '';
                        }
                    }
                }
            } catch (error) {
                console.error('Error fetching latest repo:', error);
                document.getElementById('latest-repo-title').textContent = 'Error Loading Repo';
                document.getElementById('latest-repo-desc').textContent = 'Failed to load latest repository from GitHub.';
            }
        }

        window.addEventListener('resize', init);
        window.onload = () => {
            if (typeof Lenis !== 'undefined') lenis = new Lenis({ lerp: 0.1, smoothWheel: true });
            init();
            animate();
            fetchLatestGitHubRepo();
        };
    </script>
</body>

</html>
