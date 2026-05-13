<!DOCTYPE html>
<html lang="ja" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tetsuya Goto | Graphic Designer Portfolio</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts: Inter & Noto Sans JP -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;800&family=Noto+Sans+JP:wght@300;400;500;700&display=swap" rel="stylesheet">
    
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Inter', 'Noto Sans JP', 'sans-serif'],
                    },
                    colors: {
                        primary: '#2C3E50', // ダークブルー
                        accent: '#E74C3C',  // レッド
                        lightBg: '#ECF0F1', // ライトグレー
                        darkBg: '#1a252f',  // ダークモード用背景
                        darkCard: '#2c3e50',// ダークモード用カード背景
                    },
                    animation: {
                        'fade-in-up': 'fadeInUp 0.8s ease-out forwards',
                        'slide-in-right': 'slideInRight 0.8s ease-out forwards',
                        'pulse-slow': 'pulse 3s cubic-bezier(0.4, 0, 0.6, 1) infinite',
                    },
                    keyframes: {
                        fadeInUp: {
                            '0%': { opacity: '0', transform: 'translateY(30px)' },
                            '100%': { opacity: '1', transform: 'translateY(0)' },
                        },
                        slideInRight: {
                            '0%': { opacity: '0', transform: 'translateX(30px)' },
                            '100%': { opacity: '1', transform: 'translateX(0)' },
                        }
                    }
                }
            }
        }
    </script>

    <style>
        body {
            transition: background-color 0.3s ease, color 0.3s ease;
        }
        
        .glass-nav {
            backdrop-filter: blur(10px);
            -webkit-backdrop-filter: blur(10px);
        }

        /* スクロールアニメーション用のクラス */
        .reveal {
            opacity: 0;
            transform: translateY(30px);
            transition: all 0.8s ease-out;
        }
        .reveal.active {
            opacity: 1;
            transform: translateY(0);
        }

        /* ヒーローセクションの背景グラデーション */
        .hero-bg-light {
            background: linear-gradient(135deg, rgba(236, 240, 241, 0.9) 0%, rgba(255, 255, 255, 0.9) 100%), url('https://images.unsplash.com/photo-1626785774573-4b799315345d?ixlib=rb-4.0.3&auto=format&fit=crop&w=2071&q=80') center/cover;
        }
        .dark .hero-bg-dark {
            background: linear-gradient(135deg, rgba(26, 37, 47, 0.95) 0%, rgba(44, 62, 80, 0.9) 100%), url('https://images.unsplash.com/photo-1626785774573-4b799315345d?ixlib=rb-4.0.3&auto=format&fit=crop&w=2071&q=80') center/cover;
        }

        /* ポートフォリオカードのホバーエフェクト */
        .portfolio-card {
            overflow: hidden;
        }
        .portfolio-card img {
            transition: transform 0.5s ease;
        }
        .portfolio-card:hover img {
            transform: scale(1.05);
        }
        .portfolio-overlay {
            background: linear-gradient(to top, rgba(44, 62, 80, 0.9), transparent);
            opacity: 0;
            transition: opacity 0.3s ease;
        }
        .portfolio-card:hover .portfolio-overlay {
            opacity: 1;
        }
    </style>
</head>
<body class="bg-lightBg text-primary dark:bg-darkBg dark:text-gray-200 antialiased font-sans">

    <!-- Navigation -->
    <nav class="fixed w-full z-50 glass-nav bg-white/70 dark:bg-darkCard/80 border-b border-gray-200 dark:border-gray-700 transition-colors duration-300">
        <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex justify-between items-center h-16">
                <!-- Logo -->
                <div class="flex-shrink-0 flex items-center">
                    <a href="#" class="text-2xl font-bold tracking-tighter text-primary dark:text-white">
                        T.GOTO<span class="text-accent">.</span>
                    </a>
                </div>

                <!-- Desktop Menu -->
                <div class="hidden md:flex space-x-8 items-center">
                    <a href="#about" class="text-sm font-medium hover:text-accent transition-colors">About</a>
                    <a href="#skills" class="text-sm font-medium hover:text-accent transition-colors">Skills</a>
                    <a href="#portfolio" class="text-sm font-medium hover:text-accent transition-colors">Portfolio</a>
                    <a href="#contact" class="text-sm font-medium hover:text-accent transition-colors">Contact</a>
                    
                    <!-- Theme Toggle Button -->
                    <button id="theme-toggle" class="p-2 rounded-full hover:bg-gray-200 dark:hover:bg-gray-700 transition-colors focus:outline-none focus:ring-2 focus:ring-accent" aria-label="Toggle Dark Mode">
                        <i id="theme-icon" class="fas fa-moon text-lg"></i>
                    </button>
                </div>

                <!-- Mobile menu button -->
                <div class="md:hidden flex items-center space-x-4">
                    <button id="theme-toggle-mobile" class="p-2 rounded-full hover:bg-gray-200 dark:hover:bg-gray-700 transition-colors focus:outline-none" aria-label="Toggle Dark Mode">
                        <i id="theme-icon-mobile" class="fas fa-moon text-lg"></i>
                    </button>
                    <button id="mobile-menu-btn" class="text-primary dark:text-white focus:outline-none p-2" aria-label="Open Menu">
                        <i class="fas fa-bars text-2xl"></i>
                    </button>
                </div>
            </div>
        </div>

        <!-- Mobile Menu Panel -->
        <div id="mobile-menu" class="hidden md:hidden bg-white dark:bg-darkCard border-b border-gray-200 dark:border-gray-700">
            <div class="px-2 pt-2 pb-3 space-y-1 sm:px-3">
                <a href="#about" class="block px-3 py-2 rounded-md text-base font-medium hover:bg-gray-100 dark:hover:bg-gray-700 mobile-link">About</a>
                <a href="#skills" class="block px-3 py-2 rounded-md text-base font-medium hover:bg-gray-100 dark:hover:bg-gray-700 mobile-link">Skills</a>
                <a href="#portfolio" class="block px-3 py-2 rounded-md text-base font-medium hover:bg-gray-100 dark:hover:bg-gray-700 mobile-link">Portfolio</a>
                <a href="#contact" class="block px-3 py-2 rounded-md text-base font-medium hover:bg-gray-100 dark:hover:bg-gray-700 mobile-link">Contact</a>
            </div>
        </div>
    </nav>

    <!-- 1. Hero Section -->
    <section id="hero" class="relative pt-32 pb-20 md:pt-48 md:pb-32 flex items-center min-h-[90vh] hero-bg-light dark:hero-bg-dark transition-all duration-300">
        <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8 relative z-10 w-full">
            <div class="text-center md:text-left max-w-3xl">
                <span class="block text-accent font-semibold tracking-wider uppercase mb-4 animate-fade-in-up" style="animation-delay: 0.1s; opacity: 0;">Graphic Designer</span>
                <h1 class="text-5xl md:text-7xl font-extrabold tracking-tight mb-6 leading-tight animate-fade-in-up" style="animation-delay: 0.3s; opacity: 0;">
                    Colors Logic,<br/>
                    <span class="text-transparent bg-clip-text bg-gradient-to-r from-primary to-accent dark:from-blue-400 dark:to-accent">Design Magic.</span>
                </h1>
                <p class="mt-4 text-xl md:text-2xl text-gray-600 dark:text-gray-300 mb-10 animate-fade-in-up" style="animation-delay: 0.5s; opacity: 0;">
                    企業の想いを「伝わる」形に。
                </p>
                <div class="flex flex-col sm:flex-row gap-4 justify-center md:justify-start animate-fade-in-up" style="animation-delay: 0.7s; opacity: 0;">
                    <a href="#portfolio" class="px-8 py-4 bg-primary text-white rounded-full font-semibold hover:bg-opacity-90 transition-all shadow-lg hover:shadow-xl dark:bg-white dark:text-primary dark:hover:bg-gray-100 text-center">
                        View Portfolio
                    </a>
                    <a href="#contact" class="px-8 py-4 border-2 border-primary text-primary dark:border-white dark:text-white rounded-full font-semibold hover:bg-primary hover:text-white dark:hover:bg-white dark:hover:text-primary transition-all text-center">
                        Contact Me
                    </a>
                </div>
            </div>
        </div>
        
        <!-- Scroll indicator -->
        <div class="absolute bottom-10 left-1/2 transform -translate-x-1/2 animate-pulse-slow">
            <a href="#about" class="text-gray-400 hover:text-accent transition-colors" aria-label="Scroll down">
                <i class="fas fa-chevron-down text-2xl"></i>
            </a>
        </div>
    </section>

    <!-- 2. About Section -->
    <section id="about" class="py-20 md:py-32 bg-white dark:bg-darkCard transition-colors duration-300">
        <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex flex-col md:flex-row items-center gap-12">
                <!-- Image -->
                <div class="w-full md:w-1/3 flex justify-center reveal">
                    <div class="relative w-64 h-64 md:w-80 md:h-80 rounded-full p-2 border-4 border-lightBg dark:border-gray-700 shadow-xl overflow-hidden group">
                        <!-- Placeholder for illustration. Replaced with an Unsplash image of a male for mockup purposes -->
                        <img src="https://images.unsplash.com/photo-1507003211169-0a1dd7228f2d?ixlib=rb-4.0.3&auto=format&fit=crop&w=800&q=80" alt="Tetsuya Goto Portrait" class="w-full h-full object-cover rounded-full transition-transform duration-700 group-hover:scale-110">
                        <div class="absolute inset-0 rounded-full border-4 border-accent opacity-0 group-hover:opacity-100 group-hover:scale-105 transition-all duration-500 z-10"></div>
                    </div>
                </div>
                
                <!-- Text Content -->
                <div class="w-full md:w-2/3 reveal">
                    <h2 class="text-3xl md:text-4xl font-bold mb-2 flex items-center">
                        About Me
                        <span class="ml-4 h-1 w-20 bg-accent rounded-full inline-block"></span>
                    </h2>
                    <h3 class="text-xl text-gray-500 dark:text-gray-400 mb-6 font-medium">後藤 哲也 / Tetsuya Goto</h3>
                    
                    <div class="space-y-4 text-gray-700 dark:text-gray-300 leading-relaxed text-lg">
                        <p class="font-semibold text-xl text-primary dark:text-white">「初めまして、デザイナーの後藤哲也です。」</p>
                        <p>
                            近郊の制作会社で30年、ロゴ制作やグラフィックデザイン全般、カリグラフィなど多岐にわたるクリエイティブ業務に従事してきました。現在はその経験を活かし、フリーランスとして活動しています。
                        </p>
                        
                        <div class="mt-8 p-6 bg-lightBg dark:bg-gray-800 rounded-2xl border-l-4 border-accent shadow-sm">
                            <h4 class="font-bold text-primary dark:text-white mb-2 flex items-center">
                                <i class="fas fa-bullseye text-accent mr-2"></i> 強み (Strengths)
                            </h4>
                            <p class="text-base">
                                ただ美しいだけでなく、目的に合わせたビジネスの課題解決をサポートするデザインを提案します。長年の経験に基づく論理的アプローチ（Logic）と、人の心を動かす視覚的魅力（Magic）の融合が私の強みです。
                            </p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- 3. Skills Section -->
    <section id="skills" class="py-20 md:py-32 bg-lightBg dark:bg-darkBg transition-colors duration-300">
        <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="text-center mb-16 reveal">
                <h2 class="text-3xl md:text-4xl font-bold mb-4 inline-block relative">
                    My Skills
                    <span class="absolute -bottom-2 left-1/2 transform -translate-x-1/2 h-1 w-20 bg-accent rounded-full"></span>
                </h2>
                <p class="mt-4 text-gray-600 dark:text-gray-400">30年の経験で培った確かな技術力</p>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-2 gap-10">
                <!-- Software Skills -->
                <div class="bg-white dark:bg-darkCard p-8 rounded-3xl shadow-lg reveal">
                    <h3 class="text-2xl font-bold mb-6 flex items-center">
                        <i class="fas fa-laptop-code text-accent mr-3"></i> Software
                    </h3>
                    
                    <div class="space-y-6">
                        <!-- Illustrator -->
                        <div>
                            <div class="flex justify-between mb-1">
                                <span class="font-semibold text-gray-700 dark:text-gray-200">Adobe Illustrator</span>
                                <span class="text-sm text-gray-500 dark:text-gray-400">Expert</span>
                            </div>
                            <div class="w-full bg-gray-200 rounded-full h-2.5 dark:bg-gray-700">
                                <div class="bg-primary h-2.5 rounded-full" style="width: 95%"></div>
                            </div>
                        </div>
                        
                        <!-- Photoshop -->
                        <div>
                            <div class="flex justify-between mb-1">
                                <span class="font-semibold text-gray-700 dark:text-gray-200">Adobe Photoshop</span>
                                <span class="text-sm text-gray-500 dark:text-gray-400">Expert</span>
                            </div>
                            <div class="w-full bg-gray-200 rounded-full h-2.5 dark:bg-gray-700">
                                <div class="bg-primary h-2.5 rounded-full" style="width: 90%"></div>
                            </div>
                        </div>

                        <!-- InDesign -->
                        <div>
                            <div class="flex justify-between mb-1">
                                <span class="font-semibold text-gray-700 dark:text-gray-200">Adobe InDesign</span>
                                <span class="text-sm text-gray-500 dark:text-gray-400">Advanced</span>
                            </div>
                            <div class="w-full bg-gray-200 rounded-full h-2.5 dark:bg-gray-700">
                                <div class="bg-primary h-2.5 rounded-full" style="width: 85%"></div>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Design Expertise -->
                <div class="bg-white dark:bg-darkCard p-8 rounded-3xl shadow-lg reveal delay-100">
                    <h3 class="text-2xl font-bold mb-6 flex items-center">
                        <i class="fas fa-palette text-accent mr-3"></i> Expertise
                    </h3>
                    
                    <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                        <div class="flex items-start space-x-3 p-4 rounded-xl hover:bg-lightBg dark:hover:bg-gray-800 transition-colors">
                            <div class="mt-1 bg-accent/10 text-accent p-2 rounded-lg">
                                <i class="fas fa-pen-nib"></i>
                            </div>
                            <div>
                                <h4 class="font-bold text-gray-800 dark:text-gray-200">Logo Design</h4>
                                <p class="text-sm text-gray-500 mt-1">企業理念を象徴するロゴ制作</p>
                            </div>
                        </div>
                        
                        <div class="flex items-start space-x-3 p-4 rounded-xl hover:bg-lightBg dark:hover:bg-gray-800 transition-colors">
                            <div class="mt-1 bg-accent/10 text-accent p-2 rounded-lg">
                                <i class="fas fa-book-open"></i>
                            </div>
                            <div>
                                <h4 class="font-bold text-gray-800 dark:text-gray-200">Editorial Design</h4>
                                <p class="text-sm text-gray-500 mt-1">読みやすく美しい誌面構成</p>
                            </div>
                        </div>
                        
                        <div class="flex items-start space-x-3 p-4 rounded-xl hover:bg-lightBg dark:hover:bg-gray-800 transition-colors">
                            <div class="mt-1 bg-accent/10 text-accent p-2 rounded-lg">
                                <i class="fas fa-ad"></i>
                            </div>
                            <div>
                                <h4 class="font-bold text-gray-800 dark:text-gray-200">Advertising</h4>
                                <p class="text-sm text-gray-500 mt-1">反響を呼ぶポスター・チラシ</p>
                            </div>
                        </div>
                        
                        <div class="flex items-start space-x-3 p-4 rounded-xl hover:bg-lightBg dark:hover:bg-gray-800 transition-colors">
                            <div class="mt-1 bg-accent/10 text-accent p-2 rounded-lg">
                                <i class="fas fa-signature"></i>
                            </div>
                            <div>
                                <h4 class="font-bold text-gray-800 dark:text-gray-200">Calligraphy</h4>
                                <p class="text-sm text-gray-500 mt-1">手書き文字による表現</p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- 4. Portfolio Section -->
    <section id="portfolio" class="py-20 md:py-32 bg-white dark:bg-darkCard transition-colors duration-300">
        <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="text-center mb-16 reveal">
                <h2 class="text-3xl md:text-4xl font-bold mb-4 inline-block relative">
                    Portfolio Gallery
                    <span class="absolute -bottom-2 left-1/2 transform -translate-x-1/2 h-1 w-20 bg-accent rounded-full"></span>
                </h2>
                <p class="mt-4 text-gray-600 dark:text-gray-400">これまでの実績の一部をご紹介します</p>
            </div>

            <!-- Gallery Grid -->
            <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-8">
                
                <!-- Project 1 -->
                <div class="portfolio-card relative rounded-2xl shadow-lg bg-lightBg dark:bg-gray-800 cursor-pointer reveal">
                    <div class="aspect-w-4 aspect-h-3 h-64">
                        <img src="https://images.unsplash.com/photo-1626785774625-ddcddc3445e9?ixlib=rb-4.0.3&auto=format&fit=crop&w=800&q=80" alt="Corporate Brand Identity" class="w-full h-full object-cover">
                    </div>
                    <div class="portfolio-overlay absolute inset-0 flex flex-col justify-end p-6 text-white">
                        <span class="text-accent font-semibold text-sm mb-1">Branding</span>
                        <h3 class="text-xl font-bold mb-2">Corporate Identity</h3>
                        <p class="text-sm text-gray-300 opacity-0 transform translate-y-4 transition-all duration-300 group-hover:opacity-100 group-hover:translate-y-0">テクノロジー企業のCI刷新プロジェクト</p>
                    </div>
                </div>

                <!-- Project 2 -->
                <div class="portfolio-card relative rounded-2xl shadow-lg bg-lightBg dark:bg-gray-800 cursor-pointer reveal delay-100">
                    <div class="aspect-w-4 aspect-h-3 h-64">
                        <img src="https://images.unsplash.com/photo-1600880292203-757bb62b4baf?ixlib=rb-4.0.3&auto=format&fit=crop&w=800&q=80" alt="Packaging Design" class="w-full h-full object-cover">
                    </div>
                    <div class="portfolio-overlay absolute inset-0 flex flex-col justify-end p-6 text-white">
                        <span class="text-accent font-semibold text-sm mb-1">Packaging</span>
                        <h3 class="text-xl font-bold mb-2">Organic Product Package</h3>
                        <p class="text-sm text-gray-300">オーガニックコスメのパッケージデザイン</p>
                    </div>
                </div>

                <!-- Project 3 -->
                <div class="portfolio-card relative rounded-2xl shadow-lg bg-lightBg dark:bg-gray-800 cursor-pointer reveal delay-200">
                    <div class="aspect-w-4 aspect-h-3 h-64">
                        <img src="https://images.unsplash.com/photo-1541462608143-67571c6738dd?ixlib=rb-4.0.3&auto=format&fit=crop&w=800&q=80" alt="Editorial Design" class="w-full h-full object-cover">
                    </div>
                    <div class="portfolio-overlay absolute inset-0 flex flex-col justify-end p-6 text-white">
                        <span class="text-accent font-semibold text-sm mb-1">Editorial</span>
                        <h3 class="text-xl font-bold mb-2">Lifestyle Magazine</h3>
                        <p class="text-sm text-gray-300">創刊号のエディトリアルデザイン一式</p>
                    </div>
                </div>

                <!-- Project 4 -->
                <div class="portfolio-card relative rounded-2xl shadow-lg bg-lightBg dark:bg-gray-800 cursor-pointer reveal">
                    <div class="aspect-w-4 aspect-h-3 h-64">
                        <img src="https://images.unsplash.com/photo-1629752187687-3d3c7ea3a21b?ixlib=rb-4.0.3&auto=format&fit=crop&w=800&q=80" alt="Poster Design" class="w-full h-full object-cover">
                    </div>
                    <div class="portfolio-overlay absolute inset-0 flex flex-col justify-end p-6 text-white">
                        <span class="text-accent font-semibold text-sm mb-1">Advertising</span>
                        <h3 class="text-xl font-bold mb-2">Exhibition Poster</h3>
                        <p class="text-sm text-gray-300">美術展のメインビジュアルおよびポスター</p>
                    </div>
                </div>

                <!-- Project 5 -->
                <div class="portfolio-card relative rounded-2xl shadow-lg bg-lightBg dark:bg-gray-800 cursor-pointer reveal delay-100">
                    <div class="aspect-w-4 aspect-h-3 h-64">
                        <img src="https://images.unsplash.com/photo-1586075010923-2dd4570fb338?ixlib=rb-4.0.3&auto=format&fit=crop&w=800&q=80" alt="Logo Design" class="w-full h-full object-cover">
                    </div>
                    <div class="portfolio-overlay absolute inset-0 flex flex-col justify-end p-6 text-white">
                        <span class="text-accent font-semibold text-sm mb-1">Logo</span>
                        <h3 class="text-xl font-bold mb-2">Cafe Brand Logo</h3>
                        <p class="text-sm text-gray-300">新規オープンカフェのロゴマーク</p>
                    </div>
                </div>

                <!-- Project 6 -->
                <div class="portfolio-card relative rounded-2xl shadow-lg bg-lightBg dark:bg-gray-800 cursor-pointer reveal delay-200">
                    <div class="aspect-w-4 aspect-h-3 h-64">
                        <img src="https://images.unsplash.com/photo-1563298723-dcfebaa392e3?ixlib=rb-4.0.3&auto=format&fit=crop&w=800&q=80" alt="Calligraphy Work" class="w-full h-full object-cover">
                    </div>
                    <div class="portfolio-overlay absolute inset-0 flex flex-col justify-end p-6 text-white">
                        <span class="text-accent font-semibold text-sm mb-1">Calligraphy</span>
                        <h3 class="text-xl font-bold mb-2">Japanese Sake Label</h3>
                        <p class="text-sm text-gray-300">筆文字を用いた日本酒ラベルデザイン</p>
                    </div>
                </div>

            </div>

            <div class="mt-12 text-center reveal">
                <a href="#" class="inline-flex items-center justify-center px-6 py-3 border border-transparent text-base font-medium rounded-full text-white bg-primary dark:bg-gray-700 hover:bg-opacity-90 dark:hover:bg-gray-600 transition-colors shadow-md">
                    もっと見る <i class="fas fa-arrow-right ml-2"></i>
                </a>
            </div>
        </div>
    </section>

    <!-- 5. Contact Section -->
    <section id="contact" class="py-20 md:py-32 bg-lightBg dark:bg-darkBg transition-colors duration-300 relative overflow-hidden">
        
        <!-- Decorative bg elements -->
        <div class="absolute top-0 right-0 -mr-20 -mt-20 w-64 h-64 rounded-full bg-accent opacity-5 blur-3xl pointer-events-none"></div>
        <div class="absolute bottom-0 left-0 -ml-20 -mb-20 w-80 h-80 rounded-full bg-primary opacity-5 blur-3xl pointer-events-none"></div>

        <div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 relative z-10">
            <div class="text-center mb-12 reveal">
                <h2 class="text-3xl md:text-4xl font-bold mb-4 inline-block relative">
                    Contact
                    <span class="absolute -bottom-2 left-1/2 transform -translate-x-1/2 h-1 w-20 bg-accent rounded-full"></span>
                </h2>
                <p class="mt-6 text-lg text-gray-700 dark:text-gray-300 font-medium">
                    制作のご依頼、お見積り、その他ご相談はお気軽にどうぞ。
                </p>
                <p class="mt-2 text-sm text-gray-500">※通常2営業日以内にご返信いたします。</p>
            </div>

            <div class="bg-white dark:bg-darkCard rounded-3xl shadow-xl p-8 md:p-12 reveal">
                <form id="contact-form" class="space-y-6" onsubmit="event.preventDefault(); showMessage();">
                    
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <!-- Name -->
                        <div>
                            <label for="name" class="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-1">お名前 <span class="text-accent">*</span></label>
                            <input type="text" id="name" name="name" required
                                class="w-full px-4 py-3 rounded-xl border border-gray-300 dark:border-gray-600 bg-lightBg dark:bg-gray-800 text-gray-900 dark:text-white focus:ring-2 focus:ring-accent focus:border-transparent outline-none transition-all placeholder-gray-400"
                                placeholder="山田 太郎">
                        </div>
                        
                        <!-- Email -->
                        <div>
                            <label for="email" class="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-1">メールアドレス <span class="text-accent">*</span></label>
                            <input type="email" id="email" name="email" required
                                class="w-full px-4 py-3 rounded-xl border border-gray-300 dark:border-gray-600 bg-lightBg dark:bg-gray-800 text-gray-900 dark:text-white focus:ring-2 focus:ring-accent focus:border-transparent outline-none transition-all placeholder-gray-400"
                                placeholder="yamada@example.com">
                        </div>
                    </div>

                    <!-- Subject (Optional addition for clarity) -->
                    <div>
                        <label for="subject" class="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-1">ご用件</label>
                        <select id="subject" name="subject" class="w-full px-4 py-3 rounded-xl border border-gray-300 dark:border-gray-600 bg-lightBg dark:bg-gray-800 text-gray-900 dark:text-white focus:ring-2 focus:ring-accent focus:border-transparent outline-none transition-all">
                            <option value="design">デザイン制作のご依頼</option>
                            <option value="estimate">お見積りのご相談</option>
                            <option value="other">その他のお問い合わせ</option>
                        </select>
                    </div>

                    <!-- Message -->
                    <div>
                        <label for="message" class="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-1">お問い合わせ内容 <span class="text-accent">*</span></label>
                        <textarea id="message" name="message" rows="5" required
                            class="w-full px-4 py-3 rounded-xl border border-gray-300 dark:border-gray-600 bg-lightBg dark:bg-gray-800 text-gray-900 dark:text-white focus:ring-2 focus:ring-accent focus:border-transparent outline-none transition-all resize-none placeholder-gray-400"
                            placeholder="具体的な内容をご記入ください。"></textarea>
                    </div>

                    <!-- Submit Button -->
                    <div class="text-center pt-4">
                        <button type="submit"
                            class="w-full md:w-auto px-10 py-4 bg-primary text-white font-bold rounded-full hover:bg-opacity-90 dark:bg-white dark:text-primary dark:hover:bg-gray-200 transition-all shadow-lg hover:shadow-xl focus:outline-none focus:ring-4 focus:ring-primary/30 flex justify-center items-center mx-auto">
                            <i class="fas fa-paper-plane mr-2"></i> 送信する
                        </button>
                    </div>
                </form>

                <!-- Custom Message Box (Replaces alert) -->
                <div id="success-message" class="hidden mt-6 p-4 bg-green-100 border border-green-400 text-green-700 rounded-xl text-center">
                    <i class="fas fa-check-circle mr-2"></i> メッセージを送信しました。ご連絡ありがとうございます。
                </div>
            </div>
        </div>
    </section>

    <!-- Footer -->
    <footer class="bg-primary dark:bg-gray-900 text-white py-12 border-t-4 border-accent">
        <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8 flex flex-col md:flex-row justify-between items-center">
            <div class="mb-6 md:mb-0 text-center md:text-left">
                <a href="#" class="text-2xl font-bold tracking-tighter">
                    T.GOTO<span class="text-accent">.</span>
                </a>
                <p class="mt-2 text-gray-400 text-sm">Graphic Designer Portfolio</p>
            </div>
            
            <div class="flex space-x-6 mb-6 md:mb-0">
                <a href="#" class="text-gray-400 hover:text-white transition-colors">
                    <i class="fab fa-behance text-xl"></i>
                </a>
                <a href="#" class="text-gray-400 hover:text-white transition-colors">
                    <i class="fab fa-dribbble text-xl"></i>
                </a>
                <a href="#" class="text-gray-400 hover:text-white transition-colors">
                    <i class="fab fa-instagram text-xl"></i>
                </a>
            </div>

            <div class="text-gray-400 text-sm">
                &copy; <span id="year"></span> Tetsuya Goto. All rights reserved.
            </div>
        </div>
    </footer>

    <!-- JavaScript -->
    <script>
        document.addEventListener('DOMContentLoaded', () => {
            
            // 1. Theme Toggle Logic (Dark/Light Mode)
            const themeToggleBtn = document.getElementById('theme-toggle');
            const themeToggleMobileBtn = document.getElementById('theme-toggle-mobile');
            const themeIcon = document.getElementById('theme-icon');
            const themeIconMobile = document.getElementById('theme-icon-mobile');
            const htmlElement = document.documentElement;

            // Check for saved user preference, if any, on load of the website
            if (localStorage.getItem('color-theme') === 'dark' || (!('color-theme' in localStorage) && window.matchMedia('(prefers-color-scheme: dark)').matches)) {
                htmlElement.classList.add('dark');
                setSunIcon();
            } else {
                htmlElement.classList.remove('dark');
                setMoonIcon();
            }

            function setSunIcon() {
                themeIcon.classList.remove('fa-moon');
                themeIcon.classList.add('fa-sun');
                themeIconMobile.classList.remove('fa-moon');
                themeIconMobile.classList.add('fa-sun');
            }

            function setMoonIcon() {
                themeIcon.classList.remove('fa-sun');
                themeIcon.classList.add('fa-moon');
                themeIconMobile.classList.remove('fa-sun');
                themeIconMobile.classList.add('fa-moon');
            }

            function toggleTheme() {
                if (htmlElement.classList.contains('dark')) {
                    htmlElement.classList.remove('dark');
                    localStorage.setItem('color-theme', 'light');
                    setMoonIcon();
                } else {
                    htmlElement.classList.add('dark');
                    localStorage.setItem('color-theme', 'dark');
                    setSunIcon();
                }
            }

            themeToggleBtn.addEventListener('click', toggleTheme);
            themeToggleMobileBtn.addEventListener('click', toggleTheme);

            // 2. Mobile Menu Toggle
            const mobileMenuBtn = document.getElementById('mobile-menu-btn');
            const mobileMenu = document.getElementById('mobile-menu');
            const mobileLinks = document.querySelectorAll('.mobile-link');

            mobileMenuBtn.addEventListener('click', () => {
                mobileMenu.classList.toggle('hidden');
                const icon = mobileMenuBtn.querySelector('i');
                if(mobileMenu.classList.contains('hidden')){
                    icon.classList.remove('fa-times');
                    icon.classList.add('fa-bars');
                } else {
                    icon.classList.remove('fa-bars');
                    icon.classList.add('fa-times');
                }
            });

            // Close mobile menu when a link is clicked
            mobileLinks.forEach(link => {
                link.addEventListener('click', () => {
                    mobileMenu.classList.add('hidden');
                    mobileMenuBtn.querySelector('i').classList.remove('fa-times');
                    mobileMenuBtn.querySelector('i').classList.add('fa-bars');
                });
            });

            // 3. Scroll Reveal Animation
            function reveal() {
                var reveals = document.querySelectorAll(".reveal");
                for (var i = 0; i < reveals.length; i++) {
                    var windowHeight = window.innerHeight;
                    var elementTop = reveals[i].getBoundingClientRect().top;
                    var elementVisible = 100; // 発火タイミング

                    if (elementTop < windowHeight - elementVisible) {
                        reveals[i].classList.add("active");
                    }
                }
            }
            window.addEventListener("scroll", reveal);
            reveal(); // Trigger on load

            // 4. Set current year in footer
            document.getElementById('year').textContent = new Date().getFullYear();
        });

        // 5. Form Submission Mockup (No alert)
        function showMessage() {
            const btn = document.querySelector('button[type="submit"]');
            const originalText = btn.innerHTML;
            
            // Change button state
            btn.innerHTML = '<i class="fas fa-spinner fa-spin mr-2"></i> 送信中...';
            btn.disabled = true;
            btn.classList.add('opacity-70');

            // Simulate network request
            setTimeout(() => {
                const form = document.getElementById('contact-form');
                const successMsg = document.getElementById('success-message');
                
                // Show success message
                successMsg.classList.remove('hidden');
                
                // Reset form and button
                form.reset();
                btn.innerHTML = originalText;
                btn.disabled = false;
                btn.classList.remove('opacity-70');

                // Hide message after 5 seconds
                setTimeout(() => {
                    successMsg.classList.add('hidden');
                }, 5000);
            }, 1500);
        }
    </script>
</body>
</html>
