<!DOCTYPE html>
<html lang="id" class="h-full scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SKI INTERAKTIF – Jelajah Sejarah Peradaban Islam</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Font Awesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts: Amiri (Arab) & Plus Jakarta Sans (Latin) -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Amiri:ital,wght@0,400;0,700;1,400&family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
    
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        emerald: {
                            950: '#022c22',
                            900: '#064e3b',
                            800: '#065f46',
                            700: '#047857',
                            600: '#059669',
                            500: '#10b981',
                        },
                        gold: {
                            100: '#fef9c3',
                            300: '#fde047',
                            400: '#facc15',
                            500: '#eab308',
                            600: '#ca8a04',
                            700: '#a16207',
                        }
                    },
                    fontFamily: {
                        sans: ['Plus Jakarta Sans', 'sans-serif'],
                        arabic: ['Amiri', 'serif'],
                    }
                }
            }
        }
    </script>

    <style>
        /* Custom Pattern and Scrollbar Styles */
        .bg-islamic-pattern {
            background-color: #064e3b;
            background-image: radial-gradient(#ca8a04 0.75px, transparent 0.75px), radial-gradient(#ca8a04 0.75px, #064e3b 0.75px);
            background-size: 30px 30px;
            background-position: 0 0, 15px 15px;
            background-opacity: 0.15;
        }
        
        .bg-pattern-light {
            background-color: #f8fafc;
            background-image: radial-gradient(#059669 0.5px, transparent 0.5px);
            background-size: 24px 24px;
        }

        /* Gold Gradient Effects */
        .gold-gradient-text {
            background: linear-gradient(135deg, #fef9c3 0%, #facc15 50%, #ca8a04 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .gold-border-gradient {
            border-image: linear-gradient(to right, #eab308, #fef9c3, #ca8a04) 1;
        }

        .glass-card {
            background: rgba(255, 255, 255, 0.92);
            backdrop-filter: blur(12px);
            border: 1px solid rgba(202, 138, 4, 0.2);
        }

        .glass-card-dark {
            background: rgba(6, 78, 59, 0.85);
            backdrop-filter: blur(12px);
            border: 1px solid rgba(234, 179, 8, 0.3);
        }

        /* Smooth page transition */
        .view-section {
            display: none;
            opacity: 0;
            transition: opacity 0.3s ease-in-out;
        }
        .view-section.active {
            display: block;
            opacity: 1;
        }

        /* Custom Drag & Drop styling */
        .draggable-item {
            cursor: grab;
            user-select: none;
        }
        .draggable-item:active {
            cursor: grabbing;
        }
        .drop-zone.hovered {
            border-color: #eab308;
            background-color: rgba(234, 179, 8, 0.1);
        }
    </style>
</head>
<body class="bg-slate-100 text-slate-800 font-sans min-h-full flex flex-col antialiased selection:bg-gold-500 selection:text-emerald-950">

    <!-- Header Controls & Navigation -->
    <header class="sticky top-0 z-50 bg-emerald-900 text-white shadow-lg border-b-2 border-gold-500/50">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between">
            <!-- App Identity -->
            <div class="flex items-center space-x-3 cursor-pointer" onclick="showSection('dashboard')">
                <div class="w-10 h-10 rounded-full bg-gradient-to-tr from-gold-600 to-gold-300 flex items-center justify-center text-emerald-950 font-bold shadow-md">
                    <i class="fa-solid me-0.5 fa-kaaba text-lg"></i>
                </div>
                <div>
                    <span class="font-extrabold tracking-wider text-base sm:text-lg text-white block leading-tight">SKI<span class="text-gold-400"> INTERAKTIF</span></span>
                    <span class="text-[10px] text-emerald-200 hidden sm:block">Kelas XII SMA/MA</span>
                </div>
            </div>

            <!-- Page Title Indicator in Header -->
            <div id="headerPageIndicator" class="hidden md:flex items-center text-xs font-medium bg-emerald-800/80 px-3 py-1.5 rounded-full border border-emerald-700 text-emerald-100">
                <i class="fa-solid fa-compass text-gold-400 mr-2"></i>
                <span id="currentPageText">Dashboard Utama</span>
            </div>

            <!-- Header Quick Actions -->
            <div class="flex items-center space-x-2 sm:space-x-3">
                <!-- Music Control Button -->
                <button id="musicBtn" onclick="toggleMusic()" class="p-2 sm:px-3 sm:py-1.5 rounded-lg bg-emerald-800 hover:bg-emerald-700 text-gold-300 transition text-xs sm:text-sm flex items-center gap-2 border border-emerald-700 shadow" title="Musik Islami Background">
                    <i class="fa-solid fa-music text-sm" id="musicIcon"></i>
                    <span class="hidden sm:inline font-semibold" id="musicText">Musik Off</span>
                </button>

                <button id="audioBtn" onclick="toggleAudio()" class="p-2 sm:px-3 sm:py-1.5 rounded-lg bg-emerald-800 hover:bg-emerald-700 text-gold-300 transition text-xs sm:text-sm flex items-center gap-2 border border-emerald-700" title="Suara Efek / SFX">
                    <i class="fa-solid fa-volume-high text-sm" id="audioIcon"></i>
                    <span class="hidden sm:inline font-semibold" id="audioText">SFX On</span>
                </button>

                <button onclick="toggleFullScreen()" class="p-2 sm:px-3 sm:py-1.5 rounded-lg bg-emerald-800 hover:bg-emerald-700 text-gold-300 transition text-xs sm:text-sm flex items-center gap-2 border border-emerald-700" title="Layar Penuh">
                    <i class="fa-solid fa-expand text-sm" id="fsIcon"></i>
                    <span class="hidden sm:inline font-semibold">Layar Penuh</span>
                </button>

                <button onclick="showSection('dashboard')" class="p-2 sm:px-3 sm:py-1.5 rounded-lg bg-gold-500 hover:bg-gold-400 text-emerald-950 transition text-xs sm:text-sm font-bold flex items-center gap-1.5 shadow">
                    <i class="fa-solid fa-house"></i>
                    <span class="hidden sm:inline">Menu Utama</span>
                </button>
            </div>
        </div>
    </header>

    <!-- Floating Audio/Music Controller Widget for easy volume/tune adjustment -->
    <div id="musicFloatingPlayer" class="fixed bottom-4 right-4 z-40 bg-emerald-900/95 text-white border-2 border-gold-400/60 p-3 rounded-2xl shadow-2xl backdrop-blur-md hidden sm:flex items-center gap-3 transition-all duration-300">
        <div class="w-10 h-10 rounded-full bg-gold-500 text-emerald-950 flex items-center justify-center font-bold animate-pulse">
            <i class="fa-solid fa-compact-disc text-xl"></i>
        </div>
        <div class="text-xs">
            <div class="font-bold text-gold-300">Musik Islami Relaksasi</div>
            <div class="text-[10px] text-emerald-200" id="musicStatusText">Instrumen Oud & Nay (Makam Hijaz)</div>
        </div>
        <button onclick="toggleMusic()" class="w-8 h-8 rounded-full bg-emerald-800 hover:bg-emerald-700 text-gold-300 flex items-center justify-center border border-emerald-600 transition ml-2">
            <i class="fa-solid fa-pause text-xs" id="floatingMusicIcon"></i>
        </button>
    </div>

    <main class="flex-grow flex flex-col">

        <!-- ================= DASHBOARD VIEW ================= -->
        <section id="dashboard" class="view-section active flex-grow bg-islamic-pattern text-white flex flex-col justify-center py-10 px-4">
            <div class="max-w-5xl mx-auto w-full text-center space-y-8">
                
                <!-- Hero Banner -->
                <div class="space-y-4">
                    <div class="inline-flex items-center gap-2 px-4 py-1.5 rounded-full bg-gold-500/20 border border-gold-400/40 text-gold-300 text-xs sm:text-sm font-semibold tracking-wide backdrop-blur-md">
                        <i class="fa-solid fa-star text-gold-400"></i>
                        <span>Media Pembelajaran Digital Resmi Kelas XII SMA / MA</span>
                        <i class="fa-solid fa-star text-gold-400"></i>
                    </div>

                    <h1 class="text-3xl sm:text-5xl lg:text-6xl font-extrabold tracking-tight gold-gradient-text leading-tight">
                        Sejarah Kebudayaan Islam
                    </h1>
                    
                    <p class="text-base sm:text-xl text-emerald-100 max-w-2xl mx-auto font-light leading-relaxed">
                        Jelajahi perjalanan sejarah, tokoh, dan perkembangan peradaban Islam melalui pengalaman belajar dan bermain interaktif.
                    </p>
                </div>

                <!-- Islamic Decorative Hero Illustration -->
                <div class="relative max-w-md mx-auto py-6">
                    <div class="w-48 h-48 sm:w-56 sm:h-56 mx-auto rounded-full bg-gradient-to-tr from-emerald-800 to-emerald-600 border-4 border-gold-400 shadow-2xl flex items-center justify-center relative overflow-hidden group">
                        <div class="absolute inset-0 bg-[radial-gradient(#eab308_1px,transparent_1px)] [background-size:16px_16px] opacity-20"></div>
                        <i class="fa-solid fa-mosque text-7xl sm:text-8xl text-gold-400 transition-transform duration-500 group-hover:scale-110"></i>
                        <div class="absolute bottom-3 text-center w-full bg-emerald-950/80 py-1 text-xs text-gold-300 font-arabic tracking-widest">
                            الْحَضَارَةُ الإِسْلَامِيَّةُ
                        </div>
                    </div>
                </div>

                <!-- Main Action Buttons Grid -->
                <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4 max-w-4xl mx-auto pt-4">
                    <button onclick="showSection('materi')" class="group p-5 rounded-2xl glass-card-dark hover:bg-emerald-800/90 border border-gold-400/50 hover:border-gold-300 transition-all duration-300 shadow-xl flex flex-col items-center justify-center text-center transform hover:-translate-y-1">
                        <div class="w-14 h-14 rounded-xl bg-gold-500 text-emerald-950 flex items-center justify-center text-2xl font-bold mb-3 group-hover:scale-110 transition-transform shadow-md">
                            <i class="fa-solid fa-book-open-reader"></i>
                        </div>
                        <span class="text-xl font-bold text-white group-hover:text-gold-300">Ayo Belajar</span>
                        <span class="text-xs text-emerald-200 mt-1">Eksplorasi Ringkasan & Modul SKI</span>
                    </button>

                    <button onclick="showLoginModal()" class="group p-5 rounded-2xl glass-card-dark hover:bg-emerald-800/90 border border-gold-400/50 hover:border-gold-300 transition-all duration-300 shadow-xl flex flex-col items-center justify-center text-center transform hover:-translate-y-1">
                        <div class="w-14 h-14 rounded-xl bg-emerald-500 text-white flex items-center justify-center text-2xl font-bold mb-3 group-hover:scale-110 transition-transform shadow-md">
                            <i class="fa-solid fa-gamepad"></i>
                        </div>
                        <span class="text-xl font-bold text-white group-hover:text-gold-300">Ayo Bermain</span>
                        <span class="text-xs text-emerald-200 mt-1">Game Match & Drag-Drop</span>
                    </button>

                    <button onclick="showSection('skor')" class="group p-5 rounded-2xl glass-card-dark hover:bg-emerald-800/90 border border-gold-400/50 hover:border-gold-300 transition-all duration-300 shadow-xl flex flex-col items-center justify-center text-center transform hover:-translate-y-1">
                        <div class="w-14 h-14 rounded-xl bg-amber-600 text-white flex items-center justify-center text-2xl font-bold mb-3 group-hover:scale-110 transition-transform shadow-md">
                            <i class="fa-solid fa-trophy"></i>
                        </div>
                        <span class="text-xl font-bold text-white group-hover:text-gold-300">Skor & Nilai</span>
                        <span class="text-xs text-emerald-200 mt-1">Catatan Hasil Latihan Siswa</span>
                    </button>

                    <button onclick="showSection('pengembang')" class="group p-5 rounded-2xl glass-card-dark hover:bg-emerald-800/90 border border-gold-400/50 hover:border-gold-300 transition-all duration-300 shadow-xl flex flex-col items-center justify-center text-center transform hover:-translate-y-1">
                        <div class="w-14 h-14 rounded-xl bg-sky-600 text-white flex items-center justify-center text-2xl font-bold mb-3 group-hover:scale-110 transition-transform shadow-md">
                            <i class="fa-solid fa-user-gear"></i>
                        </div>
                        <span class="text-xl font-bold text-white group-hover:text-gold-300">Pengembang</span>
                        <span class="text-xs text-emerald-200 mt-1">Profil & Informasi Media</span>
                    </button>
                </div>

            </div>
        </section>

        <!-- ================= AYO BELAJAR (MATERI) VIEW ================= -->
        <section id="materi" class="view-section flex-grow bg-pattern-light py-8 px-4">
            <div class="max-w-7xl mx-auto space-y-6">
                
                <!-- Section Header & Progress Bar -->
                <div class="bg-white rounded-2xl p-6 shadow-md border border-slate-200 space-y-4">
                    <div class="flex flex-col md:flex-row md:items-center justify-between gap-4">
                        <div>
                            <div class="flex items-center gap-2 text-emerald-700 font-bold text-sm">
                                <i class="fa-solid fa-book"></i> Modul Pembelajaran Interaktif
                            </div>
                            <h2 class="text-2xl sm:text-3xl font-extrabold text-emerald-950">Materi SKI Kelas XII SMA/MA</h2>
                        </div>

                        <!-- Progress Bar Display -->
                        <div class="w-full md:w-72 bg-slate-100 p-3 rounded-xl border border-slate-200">
                            <div class="flex justify-between items-center text-xs font-bold text-slate-600 mb-1">
                                <span>Kemajuan Belajar</span>
                                <span id="progressPercent" class="text-emerald-700">20%</span>
                            </div>
                            <div class="w-full bg-slate-200 h-3 rounded-full overflow-hidden">
                                <div id="progressBar" class="bg-gradient-to-r from-emerald-600 to-gold-500 h-full w-1/5 transition-all duration-500"></div>
                            </div>
                        </div>
                    </div>

                    <!-- Navigation Tabs for Chapters -->
                    <div class="flex overflow-x-auto gap-2 pb-2 scrollbar-none border-t border-slate-100 pt-4" id="chapterTabs">
                        <!-- JS Dynamic Tabs Inserted Here -->
                    </div>
                </div>

                <!-- Main Content Display Area -->
                <div id="materiContentCard" class="bg-white rounded-2xl p-6 sm:p-8 shadow-xl border border-slate-200 space-y-8">
                    <!-- Dynamic Content Loaded by JS -->
                </div>

                <!-- Bottom Navigation Buttons -->
                <div class="flex items-center justify-between pt-2">
                    <button id="btnPrevMateri" onclick="navigateChapter(-1)" class="px-5 py-3 rounded-xl bg-slate-200 hover:bg-slate-300 text-slate-700 font-bold transition flex items-center gap-2">
                        <i class="fa-solid fa-arrow-left"></i>
                        <span>Materi Sebelumnya</span>
                    </button>
                    
                    <button id="btnNextMateri" onclick="navigateChapter(1)" class="px-5 py-3 rounded-xl bg-emerald-700 hover:bg-emerald-800 text-white font-bold transition flex items-center gap-2 shadow-md">
                        <span>Materi Berikutnya</span>
                        <i class="fa-solid fa-arrow-right"></i>
                    </button>
                </div>

            </div>
        </section>

        <!-- ================= LOGIN MODAL ================= -->
        <div id="loginModal" class="fixed inset-0 bg-emerald-950/80 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden">
            <div class="bg-white rounded-2xl max-w-md w-full p-6 sm:p-8 shadow-2xl border-2 border-gold-500 space-y-6 relative animate-fadeIn">
                <button onclick="closeLoginModal()" class="absolute top-4 right-4 text-slate-400 hover:text-slate-600 text-xl font-bold">
                    <i class="fa-solid fa-xmark"></i>
                </button>

                <div class="text-center space-y-2">
                    <div class="w-16 h-16 bg-emerald-100 text-emerald-800 rounded-full flex items-center justify-center mx-auto text-3xl">
                        <i class="fa-solid fa-user-graduate"></i>
                    </div>
                    <h3 class="text-2xl font-extrabold text-emerald-950">Identitas Siswa</h3>
                    <p class="text-xs text-slate-500">Masukkan nama & sekolah untuk mencatat hasil permainan</p>
                </div>

                <form id="loginForm" onsubmit="handleLogin(event)" class="space-y-4">
                    <div>
                        <label class="block text-xs font-bold text-slate-700 uppercase mb-1">Nama Lengkap Siswa *</label>
                        <input type="text" id="studentName" required placeholder="Contoh: Ahmad Raihan" class="w-full px-4 py-3 rounded-xl border border-slate-300 focus:outline-none focus:ring-2 focus:ring-emerald-600 text-sm">
                    </div>
                    
                    <div>
                        <label class="block text-xs font-bold text-slate-700 uppercase mb-1">Nama Sekolah / Madrasah *</label>
                        <input type="text" id="studentSchool" required placeholder="Contoh: MAN 1 Jakarta / SMA Negeri 2" class="w-full px-4 py-3 rounded-xl border border-slate-300 focus:outline-none focus:ring-2 focus:ring-emerald-600 text-sm">
                    </div>

                    <div id="loginError" class="text-red-500 text-xs hidden font-semibold">
                        * Harap isi nama dan sekolah terlebih dahulu.
                    </div>

                    <div class="pt-2 flex gap-3">
                        <button type="button" onclick="closeLoginModal()" class="w-1/2 py-3 rounded-xl bg-slate-100 hover:bg-slate-200 text-slate-700 font-bold transition text-sm">
                            Batal
                        </button>
                        <button type="submit" class="w-1/2 py-3 rounded-xl bg-emerald-700 hover:bg-emerald-800 text-white font-bold transition text-sm shadow-md">
                            Mulai Bermain
                        </button>
                    </div>
                </form>
            </div>
        </div>

        <!-- ================= AYO BERMAIN SELECTOR VIEW ================= -->
        <section id="gamesMenu" class="view-section flex-grow bg-pattern-light py-10 px-4">
            <div class="max-w-5xl mx-auto space-y-8">
                
                <div class="bg-gradient-to-r from-emerald-900 to-emerald-800 rounded-2xl p-6 sm:p-8 text-white shadow-xl flex flex-col md:flex-row items-center justify-between gap-6">
                    <div>
                        <div class="text-gold-400 font-semibold text-sm">Pusat Permainan Interaktif</div>
                        <h2 class="text-3xl font-extrabold mt-1">Pilih Permainan SKI</h2>
                        <p class="text-emerald-100 text-sm mt-2">Uji pemahaman sejarahmu melalui kuis dan simulasi interaktif.</p>
                    </div>
                    
                    <div id="studentBadge" class="bg-emerald-950/60 border border-gold-400/40 px-5 py-3 rounded-xl text-right">
                        <div class="text-xs text-gold-300">Pemain Aktif:</div>
                        <div id="badgeName" class="font-bold text-base text-white">Guest</div>
                        <div id="badgeSchool" class="text-xs text-emerald-200">Sekolah</div>
                    </div>
                </div>

                <!-- Games Cards -->
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <!-- Game 1 Card -->
                    <div class="bg-white rounded-2xl p-6 shadow-xl border border-slate-200 flex flex-col justify-between hover:border-gold-500 transition">
                        <div class="space-y-4">
                            <div class="w-12 h-12 rounded-xl bg-gold-100 text-gold-700 flex items-center justify-center text-2xl font-bold">
                                <i class="fa-solid fa-clone"></i>
                            </div>
                            <h3 class="text-xl font-bold text-emerald-950">Permainan 1: Mencocokkan Sejarah</h3>
                            <p class="text-slate-600 text-sm leading-relaxed">
                                Balik kartu dan cocokkan pasangan antara Tokoh dengan Perannya, Dinasti dengan Karakteristiknya, atau Peristiwa dengan Lokasi sejarahnya.
                            </p>
                        </div>
                        <div class="pt-6">
                            <button onclick="startMatchGame()" class="w-full py-3 rounded-xl bg-gold-500 hover:bg-gold-400 text-emerald-950 font-bold transition shadow text-sm">
                                Mainkan Matching Game
                            </button>
                        </div>
                    </div>

                    <!-- Game 2 Card -->
                    <div class="bg-white rounded-2xl p-6 shadow-xl border border-slate-200 flex flex-col justify-between hover:border-emerald-500 transition">
                        <div class="space-y-4">
                            <div class="w-12 h-12 rounded-xl bg-emerald-100 text-emerald-700 flex items-center justify-center text-2xl font-bold">
                                <i class="fa-solid fa-hand-back-fist"></i>
                            </div>
                            <h3 class="text-xl font-bold text-emerald-950">Permainan 2: Seret & Lepas (Drag & Drop)</h3>
                            <p class="text-slate-600 text-sm leading-relaxed">
                                Seret nama tokoh sejarah, ilmuwan, atau peristiwa penting ke dalam wadah kategori peradaban yang tepat.
                            </p>
                        </div>
                        <div class="pt-6">
                            <button onclick="startDragGame()" class="w-full py-3 rounded-xl bg-emerald-700 hover:bg-emerald-800 text-white font-bold transition shadow text-sm">
                                Mainkan Drag & Drop
                            </button>
                        </div>
                    </div>
                </div>

            </div>
        </section>

        <!-- ================= GAME 1: MATCHING CARDS VIEW ================= -->
        <section id="gameMatch" class="view-section flex-grow bg-pattern-light py-8 px-4">
            <div class="max-w-5xl mx-auto space-y-6">
                
                <!-- Game Controls Header -->
                <div class="bg-white rounded-2xl p-4 sm:p-6 shadow-md border border-slate-200 flex flex-wrap items-center justify-between gap-4">
                    <div>
                        <span class="text-xs font-bold text-gold-600 uppercase">Permainan 1</span>
                        <h2 class="text-2xl font-extrabold text-emerald-950">Mencocokkan Pasangan Sejarah</h2>
                    </div>

                    <div class="flex items-center gap-4">
                        <div class="bg-slate-100 px-4 py-2 rounded-xl text-center">
                            <span class="text-[10px] text-slate-500 block">Skor</span>
                            <span id="matchScore" class="font-extrabold text-emerald-700 text-lg">0</span>
                        </div>
                        <div class="bg-slate-100 px-4 py-2 rounded-xl text-center">
                            <span class="text-[10px] text-slate-500 block">Percobaan</span>
                            <span id="matchAttempts" class="font-extrabold text-slate-700 text-lg">0</span>
                        </div>
                        <button onclick="showSection('gamesMenu')" class="px-4 py-2.5 rounded-xl bg-slate-200 hover:bg-slate-300 text-slate-700 text-xs font-bold">
                            Keluar Game
                        </button>
                    </div>
                </div>

                <!-- Match Game Grid Container -->
                <div id="matchGrid" class="grid grid-cols-2 sm:grid-cols-3 lg:grid-cols-4 gap-4">
                    <!-- Dynamic Cards Inserted Here -->
                </div>

            </div>
        </section>

        <!-- ================= GAME 2: DRAG AND DROP VIEW ================= -->
        <section id="gameDrag" class="view-section flex-grow bg-pattern-light py-8 px-4">
            <div class="max-w-6xl mx-auto space-y-6">
                
                <!-- Game Controls Header -->
                <div class="bg-white rounded-2xl p-4 sm:p-6 shadow-md border border-slate-200 flex flex-wrap items-center justify-between gap-4">
                    <div>
                        <span class="text-xs font-bold text-emerald-600 uppercase">Permainan 2</span>
                        <h2 class="text-2xl font-extrabold text-emerald-950">Klasifikasi Tokoh & Kontribusi Sejarah</h2>
                    </div>

                    <div class="flex items-center gap-4">
                        <div class="bg-slate-100 px-4 py-2 rounded-xl text-center">
                            <span class="text-[10px] text-slate-500 block">Skor Drag & Drop</span>
                            <span id="dragScore" class="font-extrabold text-emerald-700 text-lg">0</span>
                        </div>
                        <button onclick="checkDragGameResult()" class="px-4 py-2.5 rounded-xl bg-emerald-700 hover:bg-emerald-800 text-white text-xs font-bold shadow">
                            Periksa Jawaban
                        </button>
                        <button onclick="showSection('gamesMenu')" class="px-4 py-2.5 rounded-xl bg-slate-200 hover:bg-slate-300 text-slate-700 text-xs font-bold">
                            Keluar Game
                        </button>
                    </div>
                </div>

                <!-- Items Pool to Drag -->
                <div class="bg-white rounded-2xl p-6 shadow-md border border-slate-200 space-y-3">
                    <h3 class="text-sm font-bold text-slate-700 flex items-center gap-2">
                        <i class="fa-solid fa-arrows-up-down-left-right text-gold-500"></i>
                        <span>Seret Item Berikut Ke Kategori yang Sesuai:</span>
                    </h3>
                    <div id="draggablePool" class="flex flex-wrap gap-3 p-4 bg-slate-50 rounded-xl border border-dashed border-slate-300 min-h-[80px]">
                        <!-- Dynamic Draggable Elements -->
                    </div>
                </div>

                <!-- Drop Target Zones -->
                <div id="dropZonesContainer" class="grid grid-cols-1 md:grid-cols-3 gap-6">
                    <!-- Dynamic Drop Target Categories -->
                </div>

            </div>
        </section>

        <!-- ================= SCORE / REKAP NILAI VIEW ================= -->
        <section id="skor" class="view-section flex-grow bg-pattern-light py-8 px-4">
            <div class="max-w-4xl mx-auto space-y-6">
                
                <div class="bg-white rounded-2xl p-6 shadow-xl border border-slate-200 space-y-6">
                    <div class="flex items-center justify-between border-b border-slate-100 pb-4">
                        <div>
                            <span class="text-xs font-bold text-amber-600 uppercase">Laporan Prestasi</span>
                            <h2 class="text-2xl font-extrabold text-emerald-950">Papan Skor & Catatan Belajar</h2>
                        </div>
                        <button onclick="clearScores()" class="text-xs text-red-600 hover:text-red-800 font-bold underline">
                            Reset Skor
                        </button>
                    </div>

                    <div class="overflow-x-auto">
                        <table class="w-full text-left text-sm">
                            <thead class="bg-slate-100 text-slate-700 font-bold uppercase text-xs">
                                <tr>
                                    <th class="p-3 rounded-l-lg">Tanggal</th>
                                    <th class="p-3">Nama Siswa</th>
                                    <th class="p-3">Sekolah</th>
                                    <th class="p-3">Jenis Permainan</th>
                                    <th class="p-3 rounded-r-lg text-right">Skor Akhir</th>
                                </tr>
                            </thead>
                            <tbody id="scoreTableBody" class="divide-y divide-slate-100">
                                <!-- Dynamic Score Rows -->
                            </tbody>
                        </table>
                    </div>
                </div>

            </div>
        </section>

        <!-- ================= PENGEMBANG VIEW ================= -->
        <section id="pengembang" class="view-section flex-grow bg-pattern-light py-8 px-4">
            <div class="max-w-4xl mx-auto space-y-6">
                
                <div class="bg-white rounded-2xl p-6 sm:p-8 shadow-xl border border-slate-200 space-y-6">
                    <div class="text-center space-y-2 border-b border-slate-100 pb-6">
                        <div class="w-20 h-20 bg-gradient-to-tr from-emerald-800 to-emerald-600 text-gold-400 rounded-full flex items-center justify-center mx-auto text-4xl shadow-lg border-2 border-gold-400">
                            <i class="fa-solid fa-graduation-cap"></i>
                        </div>
                        <h2 class="text-2xl font-extrabold text-emerald-950">Tim Pengembang Media</h2>
                        <p class="text-xs text-slate-500">Pengembang Media Pembelajaran Digital SKI Kelas XII SMA/MA</p>
                    </div>

                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6 text-sm">
                        <div class="bg-emerald-50 p-5 rounded-xl border border-emerald-100 space-y-3">
                            <h3 class="font-bold text-emerald-900 border-b border-emerald-200 pb-2 flex items-center gap-2">
                                <i class="fa-solid fa-laptop-code text-gold-600"></i> Informasi Aplikasi
                            </h3>
                            <ul class="space-y-2 text-slate-700">
                                <li><strong>Nama Media:</strong> SKI INTERAKTIF</li>
                                <li><strong>Sasaran:</strong> Siswa Kelas XII SMA / MA</li>
                                <li><strong>Mata Pelajaran:</strong> Sejarah Kebudayaan Islam</li>
                                <li><strong>Versi Aplikasi:</strong> 2.0 Web Single-File</li>
                                <li><strong>Teknologi:</strong> HTML5, Tailwind CSS, JavaScript ES6</li>
                            </ul>
                        </div>

                        <div class="bg-gold-50 p-5 rounded-xl border border-gold-200 space-y-3">
                            <h3 class="font-bold text-gold-900 border-b border-gold-200 pb-2 flex items-center gap-2">
                                <i class="fa-solid fa-book-bookmark text-emerald-700"></i> Rujukan Curriculum & Referensi
                            </h3>
                            <ul class="space-y-2 text-slate-700 text-xs leading-relaxed">
                                <li>• Buku Siswa SKI Kelas XII Kemenag RI Curriculum Standards.</li>
                                <li>• Badri Yatim, <em>Sejarah Peradaban Islam</em>, Rajawali Pers.</li>
                                <li>• Harun Nasution, <em>Islam Ditinjau dari Berbagai Aspeknya</em>.</li>
                                <li>• Ensiklopedia Peradaban Islam & Sejarah Islam Nusantara.</li>
                            </ul>
                        </div>
                    </div>

                    <div class="text-center pt-4">
                        <button onclick="showSection('dashboard')" class="px-6 py-2.5 rounded-xl bg-emerald-800 text-white font-bold text-sm hover:bg-emerald-700 transition">
                            Kembali ke Dashboard Utama
                        </button>
                    </div>
                </div>

            </div>
        </section>

    </main>

    <!-- Footer -->
    <footer class="bg-emerald-950 text-emerald-200 py-4 border-t border-gold-500/30 text-xs">
        <div class="max-w-7xl mx-auto px-4 text-center space-y-1">
            <p>&copy; 2026 <strong>SKI INTERAKTIF</strong> — Media Pembelajaran Digital Kebudayaan Islam Kelas XII.</p>
            <p class="text-[10px] text-emerald-400">Dirancang untuk Pembelajaran Interaktif Siswa SMA/MA Tanpa Instalasi External Backend.</p>
        </div>
    </footer>

    <!-- ================= JAVASCRIPT LOGIC ================= -->
    <script>
        /* -------------------------------------------------------------
           1. MATERI CURRICULUM DATA (SKI KELAS XII SMA/MA)
           ------------------------------------------------------------- */
        const MATERI_DATA = [
            {
                id: 'bab1',
                title: 'Pengantar Sejarah Kebudayaan Islam',
                purpose: 'Memahami hakikat sejarah, perbedaan kebudayaan dan peradaban Islam, serta tujuan dan manfaat mempelajari SKI bagi kehidupan modern.',
                content: `
                    <p class="text-slate-700 leading-relaxed">
                        <strong>Sejarah Kebudayaan Islam (SKI)</strong> merupakan catatan perkembangan hidup umat Islam dari masa ke masa dalam mewujudkan nilai-nilai ajaran Islam ke dalam bentuk hasil karya, cipta, dan rasa. Kebudayaan mencakup seluruh hasil pemikiran dan kebiasaan, sedangkan <strong>Peradaban Islam</strong> merefleksikan pencapaian wujud fisik, ilmu pengetahuan, seni, dan sistem pemerintahan yang tinggi.
                    </p>
                    <div class="bg-emerald-50 border-l-4 border-emerald-600 p-4 rounded-r-xl my-4">
                        <h4 class="font-bold text-emerald-900 mb-1">Tujuan Mempelajari SKI:</h4>
                        <ul class="list-disc list-inside text-sm text-slate-700 space-y-1">
                            <li>Mengenal dan mengambil <em>Ibrah</em> (pelajaran/hikmah) dari peristiwa masa lalu.</li>
                            <li>Meneladani akhlak mulia para Nabi, Sahabat, dan Tokoh Cendekiawan Muslim.</li>
                            <li>Menumbuhkan rasa bangga dan cinta terhadap warisan peradaban Islam.</li>
                        </ul>
                    </div>
                `,
                summary: [
                    'Sejarah adalah rekonstruksi peristiwa masa lalu yang memiliki dampak sistematis.',
                    'Peradaban Islam berpijak pada nilai tauhid dan Al-Qur\'an serta Al-Hadits.',
                    'Mempelajari SKI membentuk kesadaran sejarah dan daya kritis siswa.'
                ],
                figures: [
                    { name: 'Ibnu Khaldun', role: 'Bapak Sosiologi & Filsafat Sejarah Islam (Penulis Kitab Al-Muqaddimah)' }
                ],
                quiz: {
                    question: 'Apakah perbedaan utama antara "Kebudayaan" dan "Peradaban" dalam kajian sejarah Islam?',
                    options: [
                        'Kebudayaan bersifat materialistis, peradaban bersifat pemikiran saja',
                        'Kebudayaan mencakup wujud pemikiran/kebiasaan, peradaban adalah bentuk fisik & kemajuan halus yang kompleks',
                        'Tidak ada perbedaan sama sekali',
                        'Kebudayaan hanya berlaku di Arab, peradaban di Nusantara'
                    ],
                    correctIndex: 1,
                    explanation: 'Peradaban merupakan bagian kebudayaan yang telah mencapai tingkat kemajuan fisik, ilmu pengetahuan, dan tata sosial yang halus.'
                }
            },
            {
                id: 'bab2',
                title: 'Perkembangan Peradaban Islam: Khulafaur Rasyidin & Dinasti Besar',
                purpose: 'Menganalisis perkembangan peradaban pada masa Khulafaur Rasyidin, Dinasti Umayyah, dan Dinasti Abbasiyah.',
                content: `
                    <p class="text-slate-700 leading-relaxed mb-3">
                        Perkembangan peradaban Islam mengalami masa keemasan melalui tahap kepemimpinan Khulafaur Rasyidin yang dilanjutkan oleh Dinasti Umayyah di Damaskus dan Dinasti Abbasiyah di Baghdad.
                    </p>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4 my-4">
                        <div class="border border-slate-200 p-4 rounded-xl bg-slate-50">
                            <h4 class="font-bold text-emerald-800 text-sm mb-1">Dinasti Umayyah (Damaskus)</h4>
                            <p class="text-xs text-slate-600">Peluasan wilayah ke Semenanjung Iberia (Andalusia), kodifikasi Al-Qur'an & Hadits, serta standarisasi mata uang dinar-dirham Islam.</p>
                        </div>
                        <div class="border border-slate-200 p-4 rounded-xl bg-slate-50">
                            <h4 class="font-bold text-emerald-800 text-sm mb-1">Dinasti Abbasiyah (Baghdad)</h4>
                            <p class="text-xs text-slate-600">Puncak kejayaan ilmu pengetahuan (Golden Age) dengan pusat penerjemahan dan perpustakaan <strong>Bayt al-Hikmah</strong>.</p>
                        </div>
                    </div>
                `,
                summary: [
                    'Khulafaur Rasyidin meletakkan dasar musyawarah dan ekspansi dakwah awal.',
                    'Dinasti Umayyah memodernisasi administrasi pemerintahan dan bahasa Arab resmi.',
                    'Dinasti Abbasiyah melahirkan saintis besar seperti Al-Khawarizmi, Ibnu Sina, dan Al-Razi.'
                ],
                figures: [
                    { name: 'Harun al-Rasyid', role: 'Khalifah Abbasiyah yang mendirikan Bayt al-Hikmah' },
                    { name: 'Tariq bin Ziyad', role: 'Panglima penakluk Andalusia (Gibraltar/Jabal Tariq)' }
                ],
                quiz: {
                    question: 'Pusat penerjemahan dan akademi ilmu pengetahuan yang terkenal pada masa Dinasti Abbasiyah adalah...',
                    options: ['Al-Azhar', 'Bayt al-Hikmah', 'Cordoba Library', 'Darul Hikmah Cairo'],
                    correctIndex: 1,
                    explanation: 'Bayt al-Hikmah di Baghdad adalah pusat ilmu pengetahuan utama era Abbasiyah.'
                }
            },
            {
                id: 'bab3',
                title: 'Islam di Andalusia & Perkembangan Global',
                purpose: 'Memahami kejayaan peradaban Islam di Eropa (Andalusia/Spanyol) serta penyebaran Islam di Asia dan Afrika.',
                content: `
                    <p class="text-slate-700 leading-relaxed mb-3">
                        Andalusia (Spanyol) di bawah pemerintahan Umayyah II menjadi jembatan transfer ilmu pengetahuan Islam ke dunia Barat/Eropa. Kota Cordoba dan Granada menjadi pusat kemajuan arsitektur dan sains terdepan pada abad pertengahan.
                    </p>
                    <p class="text-slate-700 leading-relaxed">
                        Sementara itu, penyebaran Islam di Asia Tengah dan Afrika berlangsung melalui jalur perdagangan damai, akulturasi budaya, dan peran sufi wandering scholars.
                    </p>
                `,
                summary: [
                    'Cordoba memiliki perpustakaan besar berisikan ratusan ribu naskah ilmiah.',
                    'Istana Alhambra di Granada adalah simbol kejayaan seni arsitektur Islami Eropa.',
                    'Tokoh filosof Ibnu Rusyd (Averroes) menghubungkan pemikiran Aristoteles dengan dunia ilmiah.'
                ],
                figures: [
                    { name: 'Ibnu Rusyd (Averroes)', role: 'Filsuf & ilmuwan sains medis terkemuka Andalusia' },
                    { name: 'Abul Qasim al-Zahrawi', role: 'Bapak Bedah Modern dari Cordoba' }
                ],
                quiz: {
                    question: 'Istana mega megah warisan arsitektur Islam di Granada, Spanyol adalah...',
                    options: ['Istana Topkapi', 'Istana Alhambra', 'Taj Mahal', 'Qutub Minar'],
                    correctIndex: 1,
                    explanation: 'Istana Alhambra merupakan mahakarya seni arsitektur Islam di Andalusia.'
                }
            },
            {
                id: 'bab4',
                title: 'Perkembangan Islam di Indonesia (Nusantara)',
                purpose: 'Menganalisis saluran penyebaran Islam di Nusantara, peran Wali Sanga, Kerajaan Islam, dan dakwah kultural.',
                content: `
                    <p class="text-slate-700 leading-relaxed">
                        Islam masuk ke Nusantara secara damai melalui saluran <strong>perdagangan, perkawinan, pendidikan (pesantren), tasawuf, dan kesenian</strong>. Kehadiran para ulama dan Wali Sanga di Jawa, Kerajaan Samudera Pasai di Sumatra, serta Kesultanan Demak dan Gowa-Tallo mempercepat dakwah Islam.
                    </p>
                    <div class="bg-amber-50 border-l-4 border-amber-500 p-4 rounded-r-xl my-4 text-sm text-slate-700">
                        <strong>Strategi Akulturasi Kultural:</strong> Sunan Kalijaga memanfaatkan media wayang kulit dan tembang Jawa (Gundul Pacul, Lir Ilir) sebagai sarana penanaman aqidah tanpa merusak tradisi lokal.
                    </div>
                `,
                summary: [
                    'Teori Gujarati, Mekah, dan Persia menjelaskan asal mula masuknya Islam ke Indonesia.',
                    'Wali Sanga menerapkan metode dakwah yang ramah, santun, dan kearifan lokal.',
                    'Kerajaan Samudera Pasai adalah kerajaan Islam tertua di Nusantara.'
                ],
                figures: [
                    { name: 'Sunan Kalijaga', role: 'Wali Sanga pelopor dakwah seni wayang & tembang' },
                    { name: 'Sultan Malik as-Saleh', role: 'Pendiri & Raja pertama Kerajaan Samudera Pasai' }
                ],
                quiz: {
                    question: 'Strategi dakwah Islam di Nusantara yang dilakukan Sunan Kalijaga adalah menggunakan media...',
                    options: ['Kekuatan Militer', 'Seni Wayang & Akulturasi Budaya', 'Perdagangan Senjata', 'Pajak Daerah'],
                    correctIndex: 1,
                    explanation: 'Sunan Kalijaga sangat piawai menggunakan media seni wayang dan budaya lokal untuk dakwah.'
                }
            },
            {
                id: 'bab5',
                title: 'Nilai dan Keteladanan Sejarah Islam',
                purpose: 'Menginternalisasi nilai-nilai positif kepemimpinan, toleransi, dan semangat menuntut ilmu untuk kehidupan modern.',
                content: `
                    <p class="text-slate-700 leading-relaxed mb-3">
                        Sejarah bukan sekadar hapalan tahun, melainkan sumber inspirasi untuk merancang masa depan generasi muda. Nilai-nilai utama yang dipetik dari sejarah peradaban Islam antara lain:
                    </p>
                    <ul class="grid grid-cols-1 sm:grid-cols-2 gap-3 text-sm">
                        <li class="bg-slate-50 p-3 rounded-lg border border-slate-200"><strong>1. Spirit Otodidak & Menuntut Ilmu:</strong> Saintis Muslim mengkaji Al-Qur'an sekaligus alam semesta.</li>
                        <li class="bg-slate-50 p-3 rounded-lg border border-slate-200"><strong>2. Toleransi Beragama:</strong> Piagam Madinah meletakkan dasar pluralisme yang diakui dunia.</li>
                        <li class="bg-slate-50 p-3 rounded-lg border border-slate-200"><strong>3. Integritas Kepemimpinan:</strong> Keadilan Umar bin Abdul Aziz dalam memimpin rakyat.</li>
                        <li class="bg-slate-50 p-3 rounded-lg border border-slate-200"><strong>4. Moderasi Beragama (Wasathiyah):</strong> Menyebarkan Islam dengan damai dan santun.</li>
                    </ul>
                `,
                summary: [
                    'Nilai keadilan dan keterbukaan adalah fondasi utama kemajuan peradaban Islam.',
                    'Siswa kelas XII SMA/MA hendaknya menjadi agen perubahan berakhlak mulia.'
                ],
                figures: [
                    { name: 'Umar bin Abdul Aziz', role: 'Khalifah Umayyah yang terkenal sangat adil dan sederhana' }
                ],
                quiz: {
                    question: 'Dokumen sejarah pertama yang menjamin toleransi dan kerukunan antarumat beragama di Madinah dipimpin Nabi Muhammad SAW adalah...',
                    options: ['Perjanjian Hudaibiyah', 'Piagam Madinah', 'Deklarasi Kairo', 'Fathul Mekah'],
                    correctIndex: 1,
                    explanation: 'Piagam Madinah (Sahifat al-Madinah) adalah piagam toleransi beragama pertama dalam sejarah.'
                }
            }
        ];

        /* -------------------------------------------------------------
           2. GAMES DATA (MATCHING & DRAG DROP)
           ------------------------------------------------------------- */
        const MATCH_DATA = [
            { id: 1, pairId: 'A', text: 'Ibnu Sina', type: 'Tokoh' },
            { id: 2, pairId: 'A', text: 'Bapak Kedokteran (Penulis Kitab Al-Qanun)', type: 'Peran' },
            
            { id: 3, pairId: 'B', text: 'Al-Khawarizmi', type: 'Tokoh' },
            { id: 4, pairId: 'B', text: 'Penemu Aljabar & Angka Nol', type: 'Peran' },

            { id: 5, pairId: 'C', text: 'Dinasti Umayyah', type: 'Dinasti' },
            { id: 6, pairId: 'C', text: 'Pusat di Damaskus & Perluasan Andalusia', type: 'Fakta' },

            { id: 7, pairId: 'D', text: 'Wali Sanga', type: 'Tokoh' },
            { id: 8, pairId: 'D', text: 'Penyebar Islam Kultural di Pulau Jawa', type: 'Peran' },

            { id: 9, pairId: 'E', text: 'Bayt al-Hikmah', type: 'Tempat' },
            { id: 10, pairId: 'E', text: 'Pusat Penerjemahan Ilmu di Baghdad', type: 'Fakta' },

            { id: 11, pairId: 'F', text: 'Samudera Pasai', type: 'Kerajaan' },
            { id: 12, pairId: 'F', text: 'Kerajaan Islam Pertama di Nusantara', type: 'Fakta' }
        ];

        const DRAG_DATA = {
            categories: [
                { id: 'cat-abbasiyah', title: 'Peradaban Abbasiyah (Baghdad)' },
                { id: 'cat-andalusia', title: 'Peradaban Andalusia (Spanyol)' },
                { id: 'cat-nusantara', title: 'Peradaban Islam Nusantara' }
            ],
            items: [
                { id: 'item-1', name: 'Al-Khawarizmi', targetCat: 'cat-abbasiyah' },
                { id: 'item-2', name: 'Bayt al-Hikmah', targetCat: 'cat-abbasiyah' },
                { id: 'item-3', name: 'Istana Alhambra', targetCat: 'cat-andalusia' },
                { id: 'item-4', name: 'Ibnu Rusyd', targetCat: 'cat-andalusia' },
                { id: 'item-5', name: 'Sunan Kalijaga', targetCat: 'cat-nusantara' },
                { id: 'item-6', name: 'Samudera Pasai', targetCat: 'cat-nusantara' }
            ]
        };

        /* -------------------------------------------------------------
           3. APPLICATION STATE MANAGEMENT
           ------------------------------------------------------------- */
        let currentChapterIndex = 0;
        let currentUser = null;
        let audioContext = null;
        let isAudioOn = true;
        let isMusicOn = false;
        let musicSynthInterval = null;

        // Game Match states
        let flippedCards = [];
        let matchedPairsCount = 0;
        let matchScore = 0;
        let matchAttempts = 0;

        // Game Drag states
        let dragAnswers = {};

        /* -------------------------------------------------------------
           4. NAVIGATION AND VIEW CONTROLLER
           ------------------------------------------------------------- */
        function showSection(sectionId) {
            playBeepSound(440, 0.05);

            // Hide all sections
            document.querySelectorAll('.view-section').forEach(sec => {
                sec.classList.remove('active');
            });

            // Show selected section
            const targetSection = document.getElementById(sectionId);
            if (targetSection) {
                targetSection.classList.add('active');
            }

            // Update Header Text Indicator
            const indicatorText = document.getElementById('currentPageText');
            if (indicatorText) {
                const labels = {
                    'dashboard': 'Dashboard Utama',
                    'materi': 'Ayo Belajar - Modul SKI',
                    'gamesMenu': 'Menu Permainan Interaktif',
                    'gameMatch': 'Permainan 1: Matching Card',
                    'gameDrag': 'Permainan 2: Drag & Drop',
                    'skor': 'Papan Skor & Catatan',
                    'pengembang': 'Profil Pengembang'
                };
                indicatorText.innerText = labels[sectionId] || 'SKI Interaktif';
            }

            // Trigger specific section initializers
            if (sectionId === 'materi') {
                renderMateriSection();
            } else if (sectionId === 'skor') {
                renderScoreTable();
            }
        }

        /* -------------------------------------------------------------
           5. MATERI & LEARNING MODULE LOGIC
           ------------------------------------------------------------- */
        function renderMateriSection() {
            // Render Tabs
            const tabsContainer = document.getElementById('chapterTabs');
            tabsContainer.innerHTML = MATERI_DATA.map((bab, index) => `
                <button onclick="selectChapter(${index})" class="px-4 py-2 rounded-xl text-xs font-bold whitespace-nowrap transition border ${index === currentChapterIndex ? 'bg-emerald-800 text-gold-300 border-gold-400 shadow' : 'bg-slate-100 text-slate-600 hover:bg-slate-200 border-slate-200'}">
                    Bab ${index + 1}: ${bab.title.split(':')[0]}
                </button>
            `).join('');

            // Render Content Card
            const bab = MATERI_DATA[currentChapterIndex];
            const contentCard = document.getElementById('materiContentCard');

            contentCard.innerHTML = `
                <div class="space-y-4">
                    <div class="inline-block px-3 py-1 rounded-full bg-emerald-100 text-emerald-800 text-xs font-extrabold uppercase tracking-wide">
                        Bab ${currentChapterIndex + 1}
                    </div>
                    <h2 class="text-2xl sm:text-3xl font-extrabold text-emerald-950">${bab.title}</h2>
                    
                    <div class="p-4 rounded-xl bg-gold-50 border border-gold-200 text-xs sm:text-sm text-gold-950 flex items-start gap-3">
                        <i class="fa-solid fa-bullseye text-gold-600 text-lg mt-0.5"></i>
                        <div>
                            <strong>Tujuan Pembelajaran:</strong>
                            <p>${bab.purpose}</p>
                        </div>
                    </div>
                </div>

                <div class="prose max-w-none text-slate-700 space-y-4 pt-2">
                    ${bab.content}
                </div>

                <!-- Tokoh / Peristiwa Penting -->
                <div class="border-t border-slate-100 pt-6 space-y-3">
                    <h3 class="font-bold text-emerald-900 text-sm flex items-center gap-2">
                        <i class="fa-solid fa-user-astronaut text-gold-500"></i> Tokoh & Peristiwa Kunci:
                    </h3>
                    <div class="grid grid-cols-1 sm:grid-cols-2 gap-3">
                        ${bab.figures.map(fig => `
                            <div class="bg-slate-50 p-3 rounded-xl border border-slate-200 flex items-center gap-3">
                                <div class="w-8 h-8 rounded-full bg-emerald-700 text-white flex items-center justify-center font-bold text-xs shrink-0">
                                    <i class="fa-solid fa-star"></i>
                                </div>
                                <div class="text-xs">
                                    <div class="font-bold text-slate-800">${fig.name}</div>
                                    <div class="text-slate-500">${fig.role}</div>
                                </div>
                            </div>
                        `).join('')}
                    </div>
                </div>

                <!-- Ringkasan Point -->
                <div class="bg-slate-50 p-5 rounded-2xl border border-slate-200 space-y-2">
                    <h3 class="font-bold text-slate-800 text-sm flex items-center gap-2">
                        <i class="fa-solid fa-list-check text-emerald-600"></i> Ringkasan Materi:
                    </h3>
                    <ul class="list-disc list-inside text-xs sm:text-sm text-slate-600 space-y-1">
                        ${bab.summary.map(item => `<li>${item}</li>`).join('')}
                    </ul>
                </div>

                <!-- Mini Refleksi Quiz -->
                <div class="bg-emerald-950 text-white p-6 rounded-2xl border border-gold-400/40 space-y-4">
                    <div class="flex items-center gap-2 text-gold-400 font-bold text-xs uppercase tracking-wider">
                        <i class="fa-solid fa-circle-question"></i> Kuis Refleksi Bab ${currentChapterIndex + 1}
                    </div>
                    <div class="text-sm font-semibold">${bab.quiz.question}</div>
                    
                    <div class="space-y-2" id="quizOptionsContainer">
                        ${bab.quiz.options.map((opt, oIdx) => `
                            <button onclick="checkBabQuiz(${oIdx})" class="w-full text-left p-3 rounded-xl bg-emerald-900 hover:bg-emerald-800 border border-emerald-700 text-xs text-emerald-100 transition flex items-center justify-between">
                                <span>${String.fromCharCode(65 + oIdx)}. ${opt}</span>
                                <i class="fa-regular fa-circle text-emerald-400"></i>
                            </button>
                        `).join('')}
                    </div>
                    
                    <div id="quizFeedback" class="hidden text-xs p-3 rounded-xl font-medium"></div>
                </div>
            `;

            // Update Progress Bar
            const progress = Math.round(((currentChapterIndex + 1) / MATERI_DATA.length) * 100);
            document.getElementById('progressPercent').innerText = `${progress}%`;
            document.getElementById('progressBar').style.width = `${progress}%`;

            // Update Prev/Next Buttons
            document.getElementById('btnPrevMateri').disabled = currentChapterIndex === 0;
            document.getElementById('btnPrevMateri').style.opacity = currentChapterIndex === 0 ? '0.5' : '1';

            document.getElementById('btnNextMateri').disabled = currentChapterIndex === MATERI_DATA.length - 1;
            document.getElementById('btnNextMateri').style.opacity = currentChapterIndex === MATERI_DATA.length - 1 ? '0.5' : '1';
        }

        function selectChapter(index) {
            currentChapterIndex = index;
            renderMateriSection();
        }

        function navigateChapter(direction) {
            const newIndex = currentChapterIndex + direction;
            if (newIndex >= 0 && newIndex < MATERI_DATA.length) {
                currentChapterIndex = newIndex;
                renderMateriSection();
            }
        }

        function checkBabQuiz(optionIndex) {
            const bab = MATERI_DATA[currentChapterIndex];
            const feedbackEl = document.getElementById('quizFeedback');
            
            if (optionIndex === bab.quiz.correctIndex) {
                playBeepSound(880, 0.15);
                feedbackEl.className = 'text-xs p-3 rounded-xl font-medium bg-emerald-800 text-gold-300 border border-gold-400 block';
                feedbackEl.innerHTML = `<i class="fa-solid fa-circle-check text-gold-400 mr-1"></i> <strong>Benar!</strong> ${bab.quiz.explanation}`;
            } else {
                playBeepSound(220, 0.2);
                feedbackEl.className = 'text-xs p-3 rounded-xl font-medium bg-red-900/80 text-red-200 border border-red-500 block';
                feedbackEl.innerHTML = `<i class="fa-solid fa-circle-xmark mr-1"></i> <strong>Kurang Tepat.</strong> Silakan coba lagi!`;
            }
        }

        /* -------------------------------------------------------------
           6. LOGIN & USER MANAGEMENT
           ------------------------------------------------------------- */
        function showLoginModal() {
            if (currentUser) {
                showSection('gamesMenu');
                updateStudentBadge();
            } else {
                document.getElementById('loginModal').classList.remove('hidden');
            }
        }

        function closeLoginModal() {
            document.getElementById('loginModal').classList.add('hidden');
        }

        function handleLogin(event) {
            event.preventDefault();
            const name = document.getElementById('studentName').value.trim();
            const school = document.getElementById('studentSchool').value.trim();

            if (name && school) {
                currentUser = { name, school };
                closeLoginModal();
                updateStudentBadge();
                showSection('gamesMenu');
            } else {
                document.getElementById('loginError').classList.remove('hidden');
            }
        }

        function updateStudentBadge() {
            if (currentUser) {
                document.getElementById('badgeName').innerText = currentUser.name;
                document.getElementById('badgeSchool').innerText = currentUser.school;
            }
        }

        /* -------------------------------------------------------------
           7. GAME 1: MATCHING CARDS LOGIC
           ------------------------------------------------------------- */
        function startMatchGame() {
            flippedCards = [];
            matchedPairsCount = 0;
            matchScore = 0;
            matchAttempts = 0;

            document.getElementById('matchScore').innerText = '0';
            document.getElementById('matchAttempts').innerText = '0';

            // Shuffle cards
            const shuffled = [...MATCH_DATA].sort(() => Math.random() - 0.5);

            const grid = document.getElementById('matchGrid');
            grid.innerHTML = shuffled.map((card, idx) => `
                <div onclick="flipCard(this, ${card.id}, '${card.pairId}')" class="match-card bg-white p-4 h-32 rounded-2xl border-2 border-slate-200 hover:border-gold-400 shadow-md flex flex-col items-center justify-center text-center cursor-pointer transition transform active:scale-95 select-none" data-id="${card.id}" data-pair="${card.pairId}">
                    <div class="card-back text-emerald-800 text-3xl">
                        <i class="fa-solid fa-star-and-crescent"></i>
                    </div>
                    <div class="card-front hidden space-y-1">
                        <span class="text-[10px] font-bold uppercase text-gold-600 tracking-wider">${card.type}</span>
                        <p class="text-xs font-bold text-slate-800">${card.text}</p>
                    </div>
                </div>
            `).join('');

            showSection('gameMatch');
        }

        function flipCard(cardEl, id, pairId) {
            if (flippedCards.length >= 2 || cardEl.classList.contains('matched') || flippedCards.some(c => c.el === cardEl)) {
                return;
            }

            playBeepSound(600, 0.05);

            // Flip visual
            cardEl.querySelector('.card-back').classList.add('hidden');
            cardEl.querySelector('.card-front').classList.remove('hidden');
            cardEl.classList.add('border-gold-500', 'bg-gold-50');

            flippedCards.push({ el: cardEl, id, pairId });

            if (flippedCards.length === 2) {
                matchAttempts++;
                document.getElementById('matchAttempts').innerText = matchAttempts;

                const [card1, card2] = flippedCards;

                if (card1.pairId === card2.pairId) {
                    // Match found
                    playBeepSound(880, 0.2);
                    card1.el.classList.add('matched', 'bg-emerald-100', 'border-emerald-500');
                    card2.el.classList.add('matched', 'bg-emerald-100', 'border-emerald-500');
                    
                    matchedPairsCount++;
                    matchScore += 20;
                    document.getElementById('matchScore').innerText = matchScore;

                    flippedCards = [];

                    // Check game finish
                    if (matchedPairsCount === MATCH_DATA.length / 2) {
                        setTimeout(() => {
                            saveScore('Mencocokkan Sejarah', matchScore);
                            alert(`Selamat! Anda menyelesaikan Permainan Matching dengan Skor: ${matchScore}`);
                        }, 500);
                    }
                } else {
                    // Not match
                    playBeepSound(200, 0.2);
                    setTimeout(() => {
                        card1.el.querySelector('.card-back').classList.remove('hidden');
                        card1.el.querySelector('.card-front').classList.add('hidden');
                        card1.el.classList.remove('border-gold-500', 'bg-gold-50');

                        card2.el.querySelector('.card-back').classList.remove('hidden');
                        card2.el.querySelector('.card-front').classList.add('hidden');
                        card2.el.classList.remove('border-gold-500', 'bg-gold-50');

                        flippedCards = [];
                    }, 1000);
                }
            }
        }

        /* -------------------------------------------------------------
           8. GAME 2: DRAG & DROP LOGIC
           ------------------------------------------------------------- */
        function startDragGame() {
            dragAnswers = {};
            document.getElementById('dragScore').innerText = '0';

            // Pool elements
            const poolContainer = document.getElementById('draggablePool');
            const shuffledItems = [...DRAG_DATA.items].sort(() => Math.random() - 0.5);

            poolContainer.innerHTML = shuffledItems.map(item => `
                <div id="${item.id}" draggable="true" ondragstart="handleDragStart(event)" class="draggable-item bg-white px-4 py-2.5 rounded-xl border border-slate-300 shadow-sm text-xs font-bold text-slate-800 flex items-center gap-2 hover:bg-gold-50 hover:border-gold-400 transition">
                    <i class="fa-solid fa-grip-vertical text-slate-400"></i>
                    <span>${item.name}</span>
                </div>
            `).join('');

            // Category zones
            const zonesContainer = document.getElementById('dropZonesContainer');
            zonesContainer.innerHTML = DRAG_DATA.categories.map(cat => `
                <div class="drop-zone bg-white p-5 rounded-2xl border-2 border-dashed border-slate-300 space-y-3 transition" ondragover="handleDragOver(event)" ondragleave="handleDragLeave(event)" ondrop="handleDrop(event, '${cat.id}')">
                    <h4 class="font-extrabold text-sm text-emerald-950 border-b border-slate-100 pb-2 flex items-center gap-2">
                        <i class="fa-solid fa-box-archive text-emerald-600"></i> ${cat.title}
                    </h4>
                    <div id="target-${cat.id}" class="space-y-2 min-h-[120px] flex flex-col justify-start">
                        <!-- Placed items will go here -->
                    </div>
                </div>
            `).join('');

            showSection('gameDrag');
        }

        function handleDragStart(event) {
            event.dataTransfer.setData('text/plain', event.target.id);
        }

        function handleDragOver(event) {
            event.preventDefault();
            event.currentTarget.classList.add('hovered');
        }

        function handleDragLeave(event) {
            event.currentTarget.classList.remove('hovered');
        }

        function handleDrop(event, catId) {
            event.preventDefault();
            event.currentTarget.classList.remove('hovered');

            const itemId = event.dataTransfer.getData('text/plain');
            const draggedEl = document.getElementById(itemId);

            if (draggedEl) {
                const targetBox = document.getElementById(`target-${catId}`);
                targetBox.appendChild(draggedEl);
                dragAnswers[itemId] = catId;
                playBeepSound(500, 0.05);
            }
        }

        function checkDragGameResult() {
            let correctCount = 0;
            const total = DRAG_DATA.items.length;

            DRAG_DATA.items.forEach(item => {
                if (dragAnswers[item.id] === item.targetCat) {
                    correctCount++;
                }
            });

            const score = Math.round((correctCount / total) * 100);
            document.getElementById('dragScore').innerText = score;

            saveScore('Drag & Drop Klasifikasi', score);
            playBeepSound(score > 60 ? 880 : 300, 0.3);

            alert(`Pemeriksaan Selesai! Anda menjawab ${correctCount} dari ${total} item dengan benar.\nSkor Akhir: ${score}`);
        }

        /* -------------------------------------------------------------
           9. SCOREBOARD AND LOCAL STORAGE
           ------------------------------------------------------------- */
        function saveScore(gameType, score) {
            if (!currentUser) return;

            const scores = JSON.parse(localStorage.getItem('ski_scores') || '[]');
            const newRecord = {
                date: new Date().toLocaleDateString('id-ID'),
                name: currentUser.name,
                school: currentUser.school,
                game: gameType,
                score: score
            };

            scores.unshift(newRecord);
            localStorage.setItem('ski_scores', JSON.stringify(scores));
        }

        function renderScoreTable() {
            const scores = JSON.parse(localStorage.getItem('ski_scores') || '[]');
            const tbody = document.getElementById('scoreTableBody');

            if (scores.length === 0) {
                tbody.innerHTML = `
                    <tr>
                        <td colspan="5" class="text-center p-6 text-slate-400 italic">Belum ada catatan skor. Silakan mainkan permainan terlebih dahulu!</td>
                    </tr>
                `;
                return;
            }

            tbody.innerHTML = scores.map(row => `
                <tr class="hover:bg-slate-50">
                    <td class="p-3 text-slate-500">${row.date}</td>
                    <td class="p-3 font-bold text-slate-800">${row.name}</td>
                    <td class="p-3 text-slate-600">${row.school}</td>
                    <td class="p-3 text-emerald-700 font-semibold">${row.game}</td>
                    <td class="p-3 font-extrabold text-gold-600 text-right">${row.score}</td>
                </tr>
            `).join('');
        }

        function clearScores() {
            if (confirm('Apakah Anda yakin ingin menghapus semua rekap skor?')) {
                localStorage.removeItem('ski_scores');
                renderScoreTable();
            }
        }

        /* -------------------------------------------------------------
           10. ISLAMIC INSTRUMENTAL MUSIC & AUDIO SYNTHESIZER
           ------------------------------------------------------------- */
        const HIJAZ_SCALE = [
            146.83, 155.56, 185.00, 196.00, 220.00, 233.08, 261.63, 293.66, 311.13, 369.99, 392.00, 440.00
        ];

        function initAudio() {
            if (!audioContext) {
                audioContext = new (window.AudioContext || window.webkitAudioContext)();
            }
            if (audioContext.state === 'suspended') {
                audioContext.resume();
            }
        }

        function playOudNote(freq, duration = 2.5) {
            if (!isMusicOn) return;
            try {
                initAudio();
                const now = audioContext.currentTime;

                const osc = audioContext.createOscillator();
                const gain = audioContext.createGain();

                osc.type = 'triangle';
                osc.frequency.setValueAtTime(freq, now);

                const filter = audioContext.createBiquadFilter();
                filter.type = 'lowpass';
                filter.frequency.setValueAtTime(800, now);
                filter.frequency.exponentialRampToValueAtTime(200, now + duration);

                gain.gain.setValueAtTime(0.001, now);
                gain.gain.linearRampToValueAtTime(0.18, now + 0.04);
                gain.gain.exponentialRampToValueAtTime(0.0001, now + duration);

                osc.connect(filter);
                filter.connect(gain);
                gain.connect(audioContext.destination);

                osc.start(now);
                osc.stop(now + duration);
            } catch (e) {
                console.log("Audio synth error", e);
            }
        }

        function startIslamicAmbientMusic() {
            if (musicSynthInterval) clearInterval(musicSynthInterval);

            let step = 0;
            const melodyPattern = [0, 2, 1, 3, 4, 3, 5, 4, 7, 6, 4, 2, 1, 0];

            musicSynthInterval = setInterval(() => {
                if (!isMusicOn) return;

                if (step % 8 === 0) {
                    playOudNote(HIJAZ_SCALE[0], 4.0);
                }

                const noteIndex = melodyPattern[step % melodyPattern.length];
                const freq = HIJAZ_SCALE[noteIndex];
                
                const randomPitch = freq * (1 + (Math.random() * 0.01 - 0.005));
                playOudNote(randomPitch, 2.2);

                step++;
            }, 650);
        }

        function stopIslamicAmbientMusic() {
            if (musicSynthInterval) {
                clearInterval(musicSynthInterval);
                musicSynthInterval = null;
            }
        }

        function toggleMusic() {
            initAudio();
            isMusicOn = !isMusicOn;
            
            const icon = document.getElementById('musicIcon');
            const text = document.getElementById('musicText');
            const floatingPlayer = document.getElementById('musicFloatingPlayer');
            const floatingIcon = document.getElementById('floatingMusicIcon');

            if (isMusicOn) {
                icon.className = 'fa-solid fa-music text-sm text-gold-400 animate-bounce';
                text.innerText = 'Musik On';
                if (floatingIcon) floatingIcon.className = 'fa-solid fa-pause text-xs';
                if (floatingPlayer) floatingPlayer.classList.remove('hidden');

                startIslamicAmbientMusic();
            } else {
                icon.className = 'fa-solid fa-music-slash text-sm';
                text.innerText = 'Musik Off';
                if (floatingIcon) floatingIcon.className = 'fa-solid fa-play text-xs';
                if (floatingPlayer) floatingPlayer.classList.add('hidden');

                stopIslamicAmbientMusic();
            }
        }

        function playBeepSound(freq, duration) {
            if (!isAudioOn) return;
            try {
                initAudio();
                const osc = audioContext.createOscillator();
                const gain = audioContext.createGain();
                osc.type = 'sine';
                osc.frequency.value = freq;
                gain.gain.setValueAtTime(0.08, audioContext.currentTime);
                gain.gain.exponentialRampToValueAtTime(0.0001, audioContext.currentTime + duration);
                osc.connect(gain);
                gain.connect(audioContext.destination);
                osc.start();
                osc.stop(audioContext.currentTime + duration);
            } catch (e) {
                // Audio fallback
            }
        }

        function toggleAudio() {
            isAudioOn = !isAudioOn;
            const icon = document.getElementById('audioIcon');
            const text = document.getElementById('audioText');
            if (isAudioOn) {
                icon.className = 'fa-solid fa-volume-high text-sm';
                text.innerText = 'SFX On';
            } else {
                icon.className = 'fa-solid fa-volume-xmark text-sm';
                text.innerText = 'SFX Off';
            }
        }

        function toggleFullScreen() {
            if (!document.fullscreenElement) {
                document.documentElement.requestFullscreen().catch(() => {});
            } else {
                if (document.exitFullscreen) {
                    document.exitFullscreen();
                }
            }
        }

        // Initialize default view on window load & user interaction listeners
        window.onload = function() {
            showSection('dashboard');

            // Enable audio context on user interaction
            document.body.addEventListener('click', function userGesture() {
                initAudio();
                document.body.removeEventListener('click', userGesture);
            }, { once: true });
        };
    </script>
</body>
</html>
