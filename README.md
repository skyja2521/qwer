[메뉴 추천받기 - 오늘 뭐 먹지_.html](https://github.com/user-attachments/files/34363831/-._.html)
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>오늘 뭐 먹지? | 맞춤 메뉴 추천</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts (Noto Sans KR) -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@300;400;500;700;900&display=swap" rel="stylesheet">
    
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Noto Sans KR', 'sans-serif'],
                    },
                    colors: {
                        brand: {
                            50: '#fff7ed',
                            100: '#ffedd5',
                            500: '#f97316',
                            600: '#ea580c',
                            700: '#c2410c',
                        }
                    },
                    animation: {
                        'bounce-short': 'bounce 0.6s ease-in-out 2',
                        'pulse-glow': 'pulseGlow 2s infinite',
                        'spin-fast': 'spin 0.2s linear infinite',
                    },
                    keyframes: {
                        pulseGlow: {
                            '0%, 100%': { boxShadow: '0 0 15px rgba(249, 115, 22, 0.3)' },
                            '50%': { boxShadow: '0 0 30px rgba(249, 115, 22, 0.7)' },
                        }
                    }
                }
            }
        }
    </script>
    <style>
        body {
            font-family: 'Noto Sans KR', sans-serif;
            background-color: #fafafa;
        }
        .glass-card {
            background: rgba(255, 255, 255, 0.85);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            border: 1px solid rgba(255, 255, 255, 0.3);
        }
        .gradient-btn {
            background: linear-gradient(135deg, #ff8a00 0%, #e52e71 100%);
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
        }
        .gradient-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 25px -5px rgba(229, 46, 113, 0.4);
        }
        .custom-scrollbar::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        .custom-scrollbar::-webkit-scrollbar-thumb {
            background: #cbd5e1;
            border-radius: 9999px;
        }
    </style>
</head>
<body class="min-h-screen text-slate-800 flex flex-col justify-between selection:bg-brand-500 selection:text-white">

    <!-- Header Navigation -->
    <header class="w-full max-w-6xl mx-auto px-4 py-6 flex items-center justify-between relative z-10">
        <div class="flex items-center gap-2 cursor-pointer" onclick="resetApp()">
            <div class="w-10 h-10 rounded-2xl bg-gradient-to-tr from-brand-500 to-amber-400 flex items-center justify-center text-white shadow-lg shadow-brand-500/20">
                <i class="fa-solid fa-utensils text-lg"></i>
            </div>
            <span class="font-extrabold text-xl tracking-tight text-slate-900">오늘뭐먹지<span class="text-brand-500">.</span></span>
        </div>
        <div class="flex items-center gap-3">
            <button onclick="toggleFilterModal()" class="px-4 py-2 rounded-xl bg-white/80 hover:bg-white text-slate-700 text-sm font-medium border border-slate-200/80 shadow-sm transition-all flex items-center gap-2 active:scale-95">
                <i class="fa-solid fa-sliders text-brand-500"></i>
                <span>조건 필터</span>
                <span id="activeFilterBadge" class="hidden w-2 h-2 rounded-full bg-brand-500"></span>
            </button>
            <button onclick="toggleFavoritesModal()" class="p-2.5 rounded-xl bg-white/80 hover:bg-white text-slate-700 border border-slate-200/80 shadow-sm transition-all active:scale-95 relative">
                <i class="fa-regular fa-bookmark text-slate-600"></i>
                <span id="favCount" class="hidden absolute -top-1 -right-1 bg-brand-500 text-white text-[10px] font-bold w-4 h-4 rounded-full flex items-center justify-center">0</span>
            </button>
        </div>
    </header>

    <!-- Main Container -->
    <main class="w-full max-w-4xl mx-auto px-4 flex-1 flex flex-col items-center justify-center py-8 relative">
        
        <!-- Hero Section (Default View) -->
        <div id="heroSection" class="w-full text-center space-y-8 my-auto transition-all duration-500">
            <div class="inline-flex items-center gap-2 px-4 py-2 rounded-full bg-orange-100/80 text-brand-700 text-xs font-semibold tracking-wide uppercase border border-orange-200/50">
                <i class="fa-solid fa-wand-magic-sparkles text-brand-500"></i>
                <span>스마트 AI 메뉴 큐레이터</span>
            </div>
            
            <h1 class="text-4xl md:text-6xl font-black text-slate-900 tracking-tight leading-tight">
                오늘 한 끼,<br class="sm:hidden"/>
                <span class="bg-clip-text text-transparent bg-gradient-to-r from-brand-500 via-rose-500 to-amber-500">무엇을 먹을지</span> 고민이신가요?
            </h1>
            
            <p class="text-slate-500 text-base md:text-lg max-w-lg mx-auto font-normal">
                카테고리, 날씨, 기분, 예산에 딱 맞는 최고의 식사 메뉴를 스마트하게 추천해 드립니다.
            </p>

            <!-- Prominent Central Action Button -->
            <div class="pt-4 flex flex-col items-center justify-center gap-4">
                <button id="mainRecommendBtn" onclick="startRecommendation()" class="gradient-btn group relative px-10 py-5 rounded-3xl text-white font-bold text-xl md:text-2xl shadow-2xl shadow-brand-500/30 flex items-center gap-4 cursor-pointer overflow-hidden active:scale-95">
                    <span class="relative z-10 flex items-center gap-3">
                        <i class="fa-solid fa-dice text-2xl group-hover:rotate-180 transition-transform duration-500"></i>
                        <span>메뉴 추천받기</span>
                    </span>
                    <div class="absolute inset-0 bg-white/20 translate-y-full group-hover:translate-y-0 transition-transform duration-300"></div>
                </button>
                <p class="text-xs text-slate-400 flex items-center gap-1">
                    <i class="fa-solid fa-shield-halved"></i> 결정장애 완치율 99.9% 보장
                </p>
            </div>

            <!-- Quick Category Tags -->
            <div class="pt-8 flex flex-wrap justify-center gap-2 max-w-xl mx-auto">
                <button onclick="quickFilter('한식')" class="px-3.5 py-1.5 rounded-full text-xs font-medium bg-white text-slate-600 border border-slate-200 hover:border-brand-500 hover:text-brand-600 transition-all">#한식</button>
                <button onclick="quickFilter('일식')" class="px-3.5 py-1.5 rounded-full text-xs font-medium bg-white text-slate-600 border border-slate-200 hover:border-brand-500 hover:text-brand-600 transition-all">#일식</button>
                <button onclick="quickFilter('중식')" class="px-3.5 py-1.5 rounded-full text-xs font-medium bg-white text-slate-600 border border-slate-200 hover:border-brand-500 hover:text-brand-600 transition-all">#중식</button>
                <button onclick="quickFilter('양식')" class="px-3.5 py-1.5 rounded-full text-xs font-medium bg-white text-slate-600 border border-slate-200 hover:border-brand-500 hover:text-brand-600 transition-all">#양식</button>
                <button onclick="quickFilter('분식/패스트푸드')" class="px-3.5 py-1.5 rounded-full text-xs font-medium bg-white text-slate-600 border border-slate-200 hover:border-brand-500 hover:text-brand-600 transition-all">#분식/패스트푸드</button>
                <button onclick="quickFilter('디저트')" class="px-3.5 py-1.5 rounded-full text-xs font-medium bg-white text-slate-600 border border-slate-200 hover:border-brand-500 hover:text-brand-600 transition-all">#디저트</button>
            </div>
        </div>

        <!-- Slot Machine / Rolling Animation View -->
        <div id="slotView" class="hidden w-full max-w-md mx-auto my-auto text-center space-y-6">
            <div class="glass-card rounded-3xl p-8 border border-white/60 shadow-2xl relative overflow-hidden">
                <div class="text-slate-400 text-sm font-medium mb-4 flex items-center justify-center gap-2">
                    <i class="fa-solid fa-spinner animate-spin text-brand-500"></i>
                    <span>오늘의 최고의 메뉴를 찾는 중...</span>
                </div>
                
                <!-- Animated Slot Wheel -->
                <div class="h-32 flex items-center justify-center overflow-hidden relative rounded-2xl bg-slate-900/5 border border-slate-200">
                    <div id="slotText" class="text-3xl md:text-4xl font-extrabold text-slate-800 transition-all duration-75 transform">
                        🍱 찌개류
                    </div>
                </div>

                <div class="mt-6 flex justify-center gap-1">
                    <span class="w-2 h-2 rounded-full bg-brand-500 animate-ping"></span>
                    <span class="w-2 h-2 rounded-full bg-brand-500"></span>
                    <span class="w-2 h-2 rounded-full bg-brand-500"></span>
                </div>
            </div>
        </div>

        <!-- Result View Card -->
        <div id="resultView" class="hidden w-full max-w-xl mx-auto my-auto transition-all duration-500">
            <div class="glass-card rounded-3xl overflow-hidden border border-white/80 shadow-2xl relative">
                
                <!-- Food Image Banner -->
                <div class="relative h-64 md:h-72 w-full overflow-hidden bg-slate-100">
                    <img id="foodImg" src="" alt="Menu Image" class="w-full h-full object-cover transition-transform duration-700 hover:scale-105" onerror="this.src='https://images.unsplash.com/photo-1546069901-ba9599a7e63c?auto=format&fit=crop&w=800&q=80'">
                    <div class="absolute inset-0 bg-gradient-to-t from-slate-900/80 via-slate-900/20 to-transparent"></div>
                    
                    <!-- Top Actions inside image -->
                    <div class="absolute top-4 left-4 right-4 flex justify-between items-center">
                        <span id="categoryBadge" class="px-3 py-1 rounded-full bg-white/90 backdrop-blur-md text-slate-800 text-xs font-bold shadow-md">
                            한식
                        </span>
                        <button id="favBtn" onclick="toggleFavoriteCurrent()" class="w-10 h-10 rounded-full bg-white/80 backdrop-blur-md flex items-center justify-center text-slate-600 hover:text-rose-500 transition-all shadow-md active:scale-90">
                            <i id="favIcon" class="fa-regular fa-heart text-lg"></i>
                        </button>
                    </div>

                    <!-- Title overlaid on image -->
                    <div class="absolute bottom-4 left-6 right-6 text-white">
                        <div class="flex items-center gap-2 mb-1">
                            <span id="spicyTag" class="text-xs px-2 py-0.5 rounded bg-rose-500/80 font-medium">🌶️ 매콤함</span>
                            <span id="priceTag" class="text-xs px-2 py-0.5 rounded bg-emerald-500/80 font-medium">₩ 1만원 안팎</span>
                        </div>
                        <h2 id="foodTitle" class="text-3xl md:text-4xl font-black tracking-tight">김치찌개</h2>
                    </div>
                </div>

                <!-- Card Details Body -->
                <div class="p-6 md:p-8 space-y-6">
                    
                    <!-- Description -->
                    <div>
                        <h4 class="text-xs font-bold text-slate-400 uppercase tracking-wider mb-2">메뉴 소개</h4>
                        <p id="foodDesc" class="text-slate-700 text-base leading-relaxed">
                            깊은 맛의 육수와 잘 익은 신김치가 어우러진 한국인의 영혼의 든든한 한 끼 식사입니다.
                        </p>
                    </div>

                    <!-- Recommendation Reason -->
                    <div class="p-4 rounded-2xl bg-orange-50/80 border border-orange-100 flex items-start gap-3">
                        <div class="p-2 rounded-xl bg-brand-500 text-white shrink-0 mt-0.5">
                            <i class="fa-solid fa-lightbulb"></i>
                        </div>
                        <div>
                            <h5 class="text-xs font-bold text-brand-700 mb-0.5">추천 이유</h5>
                            <p id="foodReason" class="text-xs md:text-sm text-slate-600">
                                오늘처럼 살짝 쌀쌀한 날씨에는 얼큰하고 따뜻한 국물이 스트레스를 해소해 줍니다.
                            </p>
                        </div>
                    </div>

                    <!-- Tags/Attributes -->
                    <div class="flex flex-wrap gap-2 pt-2">
                        <span id="tagMood" class="text-xs px-3 py-1.5 rounded-xl bg-slate-100 text-slate-600 font-medium">#스트레스해소</span>
                        <span id="tagWeather" class="text-xs px-3 py-1.5 rounded-xl bg-slate-100 text-slate-600 font-medium">#쌀쌀한날씨</span>
                        <span id="tagCalorie" class="text-xs px-3 py-1.5 rounded-xl bg-slate-100 text-slate-600 font-medium">#약 450kcal</span>
                    </div>

                    <!-- External Map Search & Action Buttons -->
                    <div class="pt-4 border-t border-slate-100 space-y-3">
                        <span class="text-xs font-bold text-slate-400 block text-center">주변 맛집 검색하기</span>
                        
                        <div class="grid grid-cols-2 gap-3">
                            <a id="naverMapLink" href="#" target="_blank" class="py-3 px-4 rounded-2xl bg-[#03C75A]/10 hover:bg-[#03C75A]/20 text-[#03C75A] text-xs font-bold flex items-center justify-center gap-2 transition-all">
                                <i class="fa-solid fa-map-location-dot"></i>
                                네이버 지도
                            </a>
                            <a id="kakaoMapLink" href="#" target="_blank" class="py-3 px-4 rounded-2xl bg-[#FFEB00]/30 hover:bg-[#FFEB00]/50 text-slate-800 text-xs font-bold flex items-center justify-center gap-2 transition-all">
                                <i class="fa-solid fa-location-arrow"></i>
                                카카오 맵
                            </a>
                        </div>

                        <div class="flex gap-3 pt-2">
                            <button onclick="startRecommendation()" class="flex-1 py-4 rounded-2xl bg-slate-900 hover:bg-slate-800 text-white font-bold text-sm shadow-lg transition-all flex items-center justify-center gap-2 active:scale-95">
                                <i class="fa-solid fa-rotate-right"></i>
                                다시 추천받기
                            </button>
                            <button onclick="shareResult()" class="py-4 px-5 rounded-2xl bg-slate-100 hover:bg-slate-200 text-slate-700 font-bold text-sm transition-all flex items-center justify-center active:scale-95" title="공유하기">
                                <i class="fa-solid fa-share-nodes"></i>
                            </button>
                        </div>
                    </div>

                </div>
            </div>
        </div>

    </main>

    <!-- Footer -->
    <footer class="w-full max-w-6xl mx-auto px-4 py-6 text-center text-xs text-slate-400 relative z-10">
        <p>© 2026 오늘뭐먹지. All rights reserved. | 당신의 완벽한 한 끼를 위하여</p>
    </footer>

    <!-- Filter Modal -->
    <div id="filterModal" class="fixed inset-0 bg-slate-900/40 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4 transition-opacity">
        <div class="glass-card w-full max-w-lg rounded-3xl p-6 md:p-8 shadow-2xl space-y-6 bg-white/95 border border-white">
            <div class="flex items-center justify-between border-b border-slate-100 pb-4">
                <h3 class="text-lg font-bold text-slate-900 flex items-center gap-2">
                    <i class="fa-solid fa-sliders text-brand-500"></i>
                    추천 조건 설정
                </h3>
                <button onclick="toggleFilterModal()" class="text-slate-400 hover:text-slate-600 p-1">
                    <i class="fa-solid fa-xmark text-xl"></i>
                </button>
            </div>

            <div class="space-y-5 custom-scrollbar max-h-[60vh] overflow-y-auto pr-1">
                <!-- Cuisine Type -->
                <div>
                    <label class="block text-xs font-bold text-slate-500 mb-2">카테고리</label>
                    <div class="grid grid-cols-3 gap-2" id="filterCategoryGroup">
                        <button data-val="전체" class="filter-btn active py-2 rounded-xl text-xs font-semibold border transition-all bg-brand-500 text-white border-brand-500">전체</button>
                        <button data-val="한식" class="filter-btn py-2 rounded-xl text-xs font-semibold border border-slate-200 text-slate-600 hover:border-slate-300">한식</button>
                        <button data-val="일식" class="filter-btn py-2 rounded-xl text-xs font-semibold border border-slate-200 text-slate-600 hover:border-slate-300">일식</button>
                        <button data-val="중식" class="filter-btn py-2 rounded-xl text-xs font-semibold border border-slate-200 text-slate-600 hover:border-slate-300">중식</button>
                        <button data-val="양식" class="filter-btn py-2 rounded-xl text-xs font-semibold border border-slate-200 text-slate-600 hover:border-slate-300">양식</button>
                        <button data-val="분식/패스트푸드" class="filter-btn py-2 rounded-xl text-xs font-semibold border border-slate-200 text-slate-600 hover:border-slate-300">분식/패스트푸드</button>
                        <button data-val="디저트" class="filter-btn py-2 rounded-xl text-xs font-semibold border border-slate-200 text-slate-600 hover:border-slate-300">디저트</button>
                    </div>
                </div>

                <!-- Spicy Level -->
                <div>
                    <label class="block text-xs font-bold text-slate-500 mb-2">매운 정도</label>
                    <div class="grid grid-cols-3 gap-2" id="filterSpicyGroup">
                        <button data-val="전체" class="filter-spicy-btn active py-2 rounded-xl text-xs font-semibold border transition-all bg-brand-500 text-white border-brand-500">상관없음</button>
                        <button data-val="순한맛" class="filter-spicy-btn py-2 rounded-xl text-xs font-semibold border border-slate-200 text-slate-600 hover:border-slate-300">🥦 순한맛</button>
                        <button data-val="매운맛" class="filter-spicy-btn py-2 rounded-xl text-xs font-semibold border border-slate-200 text-slate-600 hover:border-slate-300">🌶️ 매콤함 이상</button>
                    </div>
                </div>

                <!-- Budget -->
                <div>
                    <label class="block text-xs font-bold text-slate-500 mb-2">예산 범위</label>
                    <div class="grid grid-cols-3 gap-2" id="filterBudgetGroup">
                        <button data-val="전체" class="filter-budget-btn active py-2 rounded-xl text-xs font-semibold border transition-all bg-brand-500 text-white border-brand-500">상관없음</button>
                        <button data-val="가성비" class="filter-budget-btn py-2 rounded-xl text-xs font-semibold border border-slate-200 text-slate-600 hover:border-slate-300">1만원 이하</button>
                        <button data-val="프리미엄" class="filter-budget-btn py-2 rounded-xl text-xs font-semibold border border-slate-200 text-slate-600 hover:border-slate-300">1만원 이상</button>
                    </div>
                </div>
            </div>

            <div class="flex gap-2 pt-2">
                <button onclick="resetFilters()" class="px-4 py-3 rounded-2xl border border-slate-200 text-slate-600 font-bold text-xs hover:bg-slate-50 transition-all">초기화</button>
                <button onclick="applyFilters()" class="flex-1 py-3 rounded-2xl bg-brand-500 hover:bg-brand-600 text-white font-bold text-xs shadow-md transition-all">적용하기</button>
            </div>
        </div>
    </div>

    <!-- Favorites Modal -->
    <div id="favoritesModal" class="fixed inset-0 bg-slate-900/40 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4">
        <div class="glass-card w-full max-w-md rounded-3xl p-6 shadow-2xl bg-white/95 border border-white space-y-4">
            <div class="flex items-center justify-between border-b border-slate-100 pb-3">
                <h3 class="text-base font-bold text-slate-900 flex items-center gap-2">
                    <i class="fa-solid fa-bookmark text-brand-500"></i>
                    보관함 (북마크)
                </h3>
                <button onclick="toggleFavoritesModal()" class="text-slate-400 hover:text-slate-600 p-1">
                    <i class="fa-solid fa-xmark text-lg"></i>
                </button>
            </div>

            <div id="favoritesList" class="space-y-3 max-h-[50vh] overflow-y-auto pr-1 custom-scrollbar">
                <!-- Items populated dynamically -->
            </div>
        </div>
    </div>

    <!-- Toast Notification -->
    <div id="toast" class="fixed bottom-6 left-1/2 -translate-x-1/2 px-5 py-3 rounded-2xl bg-slate-900/90 text-white text-xs font-medium backdrop-blur-md shadow-2xl transition-all duration-300 opacity-0 pointer-events-none z-50 flex items-center gap-2">
        <i class="fa-solid fa-circle-check text-emerald-400"></i>
        <span id="toastMsg">알림 메시지</span>
    </div>

    <!-- JavaScript Data and Controller -->
    <script>
        // Database of Food Items
        const FOOD_DATABASE = [
            {
                id: 1,
                name: "돼지김치찌개",
                category: "한식",
                spicy: "매운맛",
                budget: "가성비",
                priceText: "₩ 9,000원 대",
                calorie: "약 460kcal",
                desc: "잘 익은 묵은지와 두툼한 돼지고기를 푹 끓여낸 깊고 얼큰한 한국인의 소울푸드.",
                reason: "얼큰한 국물로 오늘 쌓인 피로와 스트레스를 싹 날려버리기에 최고입니다.",
                mood: "스트레스해소",
                weather: "쌀쌀하거나 비오는 날",
                img: "https://images.unsplash.com/photo-1583224964978-2257b960c3d3?auto=format&fit=crop&w=800&q=80"
            },
            {
                id: 2,
                name: "연어 덮밥 (사케동)",
                category: "일식",
                spicy: "순한맛",
                budget: "프리미엄",
                priceText: "₩ 14,000원 대",
                calorie: "약 520kcal",
                desc: "신선하고 두툼한 생연어를 특제 간장 소스와 와사비를 더해 밥 위에 얹은 정갈한 일식 덮밥.",
                reason: "부드럽고 고소한 연어로 담백하면서도 기분 좋은 깔끔한 한 끼를 누려보세요.",
                mood: "기분전환",
                weather: "화창한 날",
                img: "https://images.unsplash.com/photo-1546069901-ba9599a7e63c?auto=format&fit=crop&w=800&q=80"
            },
            {
                id: 3,
                name: "마라탕",
                category: "중식",
                spicy: "매운맛",
                budget: "프리미엄",
                priceText: "₩ 12,000원 대",
                calorie: "약 680kcal",
                desc: "얼얼한 알싸함이 특징인 사천식 스파이시 국물 요리로 다양한 재료를 취향껏 골라먹는 재미가 있는 메뉴.",
                reason: "중독성 강한 매콤함과 화끈한 스파이스로 기분을 업시키기에 딱입니다.",
                mood: "자극이필요할때",
                weather: "바람부는 날",
                img: "https://images.unsplash.com/photo-1569718212165-3a8278d5f624?auto=format&fit=crop&w=800&q=80"
            },
            {
                id: 4,
                name: "수제 베이컨 치즈버거",
                category: "분식/패스트푸드",
                spicy: "순한맛",
                budget: "가성비",
                priceText: "₩ 8,500원 대",
                calorie: "약 720kcal",
                desc: "육즙 가득한 육향 패티에 고소한 체다 치즈와 크리스피 베이컨이 풍성하게 들어간 수제 버거.",
                reason: "빠르고 확실한 행복! 든든하고 리치한 칼로리가 필요할 때 강력 추천합니다.",
                mood: "에너지충전",
                weather: "언제나",
                img: "https://images.unsplash.com/photo-1568901346375-23c9450c58cd?auto=format&fit=crop&w=800&q=80"
            },
            {
                id: 5,
                name: "까르보나라 파스타",
                category: "양식",
                spicy: "순한맛",
                budget: "프리미엄",
                priceText: "₩ 13,000원 대",
                calorie: "약 580kcal",
                desc: "진한 크림과 고소한 파마산 치즈, 베이컨이 풍부하게 어우러진 클래식 이탈리안 파스타.",
                reason: "부드럽고 크리미한 풍미로 소소한 일상의 사치를 누리고 싶을 때 좋습니다.",
                mood: "로맨틱/힐링",
                weather: "나른한 오후",
                img: "https://images.unsplash.com/photo-1612874742237-6526221588e3?auto=format&fit=crop&w=800&q=80"
            },
            {
                id: 6,
                name: "떡볶이 & 튀김 세트",
                category: "분식/패스트푸드",
                spicy: "매운맛",
                budget: "가성비",
                priceText: "₩ 7,000원 대",
                calorie: "약 600kcal",
                desc: "매콤달콤한 양념에 쫄깃한 떡과 어묵, 바삭한 모둠 튀김을 소스에 찍어먹는 완벽 조합.",
                reason: "언제 먹어도 실패 없는 대중적인 맛! 출출함을 달래줄 최상의 분식 조합입니다.",
                mood: "출출할때",
                weather: "나른한 날",
                img: "https://images.unsplash.com/photo-1626777552726-4a6b54c97e46?auto=format&fit=crop&w=800&q=80"
            },
            {
                id: 7,
                name: "수제 돈카츠 (등심)",
                category: "일식",
                spicy: "순한맛",
                budget: "프리미엄",
                priceText: "₩ 11,000원 대",
                calorie: "약 650kcal",
                desc: "두툼한 도드람 한돈 등심을 겉은 바삭하고 속은 촉촉하게 튀겨낸 고급 일본식 돈가스.",
                reason: "겉바속촉의 정석! 씹는 맛과 고소함으로 만족스러운 한 끼를 보장합니다.",
                mood: "든든한한끼",
                weather: "맑은 날",
                img: "https://images.unsplash.com/photo-1591814468924-caf88d1232e1?auto=format&fit=crop&w=800&q=80"
            },
            {
                id: 8,
                name: "딸기 생크림 케이크 & 아메리카노",
                category: "디저트",
                spicy: "순한맛",
                budget: "가성비",
                priceText: "₩ 9,500원 대",
                calorie: "약 410kcal",
                desc: "상큼한 생딸기와 부드러운 우유 생크림 시트에 깔끔한 쌉싸름함의 핫/아이스 아메리카노.",
                reason: "달콤함과 쌉싸름함의 완벽한 밸런스로 식후 디저트 타임에 최적입니다.",
                mood: "당충전",
                weather: "나른한 오후",
                img: "https://images.unsplash.com/photo-1565958011703-44f9829ba187?auto=format&fit=crop&w=800&q=80"
            }
        ];

        // Filter State
        let activeFilters = {
            category: "전체",
            spicy: "전체",
            budget: "전체"
        };

        let currentFood = null;
        let favorites = JSON.parse(localStorage.getItem('food_favs') || '[]');

        // Initialize Page
        window.addEventListener('DOMContentLoaded', () => {
            updateFavBadge();
            setupFilterBtnListeners();
        });

        // Filter Setup
        function setupFilterBtnListeners() {
            setupGroupListeners('filterCategoryGroup', 'category');
            setupGroupListeners('filterSpicyGroup', 'spicy');
            setupGroupListeners('filterBudgetGroup', 'budget');
        }

        function setupGroupListeners(groupId, key) {
            const container = document.getElementById(groupId);
            if (!container) return;
            const buttons = container.querySelectorAll('button');
            buttons.forEach(btn => {
                btn.addEventListener('click', () => {
                    buttons.forEach(b => {
                        b.classList.remove('bg-brand-500', 'text-white', 'border-brand-500');
                        b.classList.add('border-slate-200', 'text-slate-600');
                    });
                    btn.classList.add('bg-brand-500', 'text-white', 'border-brand-500');
                    btn.classList.remove('border-slate-200', 'text-slate-600');
                    activeFilters[key] = btn.getAttribute('data-val');
                });
            });
        }

        function quickFilter(categoryName) {
            activeFilters.category = categoryName;
            // Sync filter modal UI buttons
            const buttons = document.querySelectorAll('#filterCategoryGroup button');
            buttons.forEach(b => {
                if (b.getAttribute('data-val') === categoryName) {
                    b.click();
                }
            });
            updateFilterBadge();
            startRecommendation();
        }

        function toggleFilterModal() {
            const modal = document.getElementById('filterModal');
            modal.classList.toggle('hidden');
        }

        function applyFilters() {
            updateFilterBadge();
            toggleFilterModal();
            showToast('필터가 적용되었습니다.');
        }

        function resetFilters() {
            activeFilters = { category: "전체", spicy: "전체", budget: "전체" };
            document.querySelectorAll('.filter-btn, .filter-spicy-btn, .filter-budget-btn').forEach(b => {
                b.classList.remove('bg-brand-500', 'text-white', 'border-brand-500');
                b.classList.add('border-slate-200', 'text-slate-600');
            });
            document.querySelectorAll('#filterCategoryGroup button')[0]?.classList.add('bg-brand-500', 'text-white', 'border-brand-500');
            document.querySelectorAll('#filterSpicyGroup button')[0]?.classList.add('bg-brand-500', 'text-white', 'border-brand-500');
            document.querySelectorAll('#filterBudgetGroup button')[0]?.classList.add('bg-brand-500', 'text-white', 'border-brand-500');
            updateFilterBadge();
            showToast('필터가 초기화되었습니다.');
        }

        function updateFilterBadge() {
            const badge = document.getElementById('activeFilterBadge');
            if (activeFilters.category !== "전체" || activeFilters.spicy !== "전체" || activeFilters.budget !== "전체") {
                badge.classList.remove('hidden');
            } else {
                badge.classList.add('hidden');
            }
        }

        // Core Recommendation Slot Logic
        function startRecommendation() {
            // Filter database
            let filteredList = FOOD_DATABASE.filter(item => {
                if (activeFilters.category !== "전체" && item.category !== activeFilters.category) return false;
                if (activeFilters.spicy !== "전체" && item.spicy !== activeFilters.spicy) return false;
                if (activeFilters.budget !== "전체" && item.budget !== activeFilters.budget) return false;
                return true;
            });

            if (filteredList.length === 0) {
                showToast('조건에 맞는 메뉴가 없어 전체 메뉴 중 추천합니다.');
                filteredList = FOOD_DATABASE;
            }

            // UI Switch
            document.getElementById('heroSection').classList.add('hidden');
            document.getElementById('resultView').classList.add('hidden');
            document.getElementById('slotView').classList.remove('hidden');

            const slotText = document.getElementById('slotText');
            let counter = 0;
            const maxSpins = 20;
            const interval = setInterval(() => {
                const randomTemp = FOOD_DATABASE[Math.floor(Math.random() * FOOD_DATABASE.length)];
                slotText.innerText = `${getCategoryEmoji(randomTemp.category)} ${randomTemp.name}`;
                counter++;

                if (counter >= maxSpins) {
                    clearInterval(interval);
                    // Select Final Pick
                    const picked = filteredList[Math.floor(Math.random() * filteredList.length)];
                    renderResult(picked);
                }
            }, 80);
        }

        function renderResult(food) {
            currentFood = food;

            document.getElementById('slotView').classList.add('hidden');
            const resultView = document.getElementById('resultView');
            resultView.classList.remove('hidden');

            // Populate data
            document.getElementById('foodImg').src = food.img;
            document.getElementById('categoryBadge').innerText = food.category;
            document.getElementById('spicyTag').innerText = food.spicy === '매운맛' ? '🌶️ 매콤함' : '🥦 순한맛';
            document.getElementById('priceTag').innerText = food.priceText;
            document.getElementById('foodTitle').innerText = food.name;
            document.getElementById('foodDesc').innerText = food.desc;
            document.getElementById('foodReason').innerText = food.reason;
            
            document.getElementById('tagMood').innerText = `#${food.mood}`;
            document.getElementById('tagWeather').innerText = `#${food.weather}`;
            document.getElementById('tagCalorie').innerText = `#${food.calorie}`;

            // Map Links
            document.getElementById('naverMapLink').href = `https://map.naver.com/v5/search/${encodeURIComponent(food.name)}`;
            document.getElementById('kakaoMapLink').href = `https://map.kakao.com/link/search/${encodeURIComponent(food.name)}`;

            // Fav Status Sync
            updateFavButtonUI();
        }

        function resetApp() {
            document.getElementById('resultView').classList.add('hidden');
            document.getElementById('slotView').classList.add('hidden');
            document.getElementById('heroSection').classList.remove('hidden');
        }

        // Favorites System
        function toggleFavoriteCurrent() {
            if (!currentFood) return;
            const index = favorites.findIndex(f => f.id === currentFood.id);
            if (index > -1) {
                favorites.splice(index, 1);
                showToast('북마크에서 제거되었습니다.');
            } else {
                favorites.push(currentFood);
                showToast('북마크에 추가되었습니다!');
            }
            localStorage.setItem('food_favs', JSON.stringify(favorites));
            updateFavButtonUI();
            updateFavBadge();
        }

        function updateFavButtonUI() {
            const favIcon = document.getElementById('favIcon');
            if (!currentFood || !favIcon) return;
            const isFav = favorites.some(f => f.id === currentFood.id);
            if (isFav) {
                favIcon.className = "fa-solid fa-heart text-lg text-rose-500";
            } else {
                favIcon.className = "fa-regular fa-heart text-lg text-slate-600";
            }
        }

        function updateFavBadge() {
            const favCount = document.getElementById('favCount');
            if (favorites.length > 0) {
                favCount.innerText = favorites.length;
                favCount.classList.remove('hidden');
            } else {
                favCount.classList.add('hidden');
            }
        }

        function toggleFavoritesModal() {
            const modal = document.getElementById('favoritesModal');
            const list = document.getElementById('favoritesList');
            
            if (modal.classList.contains('hidden')) {
                // Populate
                if (favorites.length === 0) {
                    list.innerHTML = `<div class="text-center py-8 text-slate-400 text-xs">저장된 메뉴가 없습니다.</div>`;
                } else {
                    list.innerHTML = favorites.map(f => `
                        <div class="flex items-center justify-between p-3 rounded-2xl bg-slate-50 hover:bg-slate-100 border border-slate-100 transition-all">
                            <div class="flex items-center gap-3">
                                <img src="${f.img}" class="w-12 h-12 rounded-xl object-cover" alt="${f.name}">
                                <div>
                                    <h5 class="text-xs font-bold text-slate-800">${f.name}</h5>
                                    <span class="text-[10px] text-slate-400">${f.category} • ${f.priceText}</span>
                                </div>
                            </div>
                            <button onclick="removeFavorite(${f.id})" class="text-slate-400 hover:text-rose-500 p-2">
                                <i class="fa-solid fa-trash-can text-sm"></i>
                            </button>
                        </div>
                    `).join('');
                }
                modal.classList.remove('hidden');
            } else {
                modal.classList.add('hidden');
            }
        }

        function removeFavorite(id) {
            favorites = favorites.filter(f => f.id !== id);
            localStorage.setItem('food_favs', JSON.stringify(favorites));
            updateFavBadge();
            updateFavButtonUI();
            toggleFavoritesModal();
            toggleFavoritesModal(); // refresh UI
            showToast('삭제되었습니다.');
        }

        // Sharing Functionality
        function shareResult() {
            if (!currentFood) return;
            const shareData = {
                title: '오늘 뭐 먹지?',
                text: `오늘의 추천 메뉴는 바로 [${currentFood.name}] 입니다!`,
                url: window.location.href
            };

            if (navigator.share) {
                navigator.share(shareData).catch(() => {});
            } else {
                // ExecCommand Fallback
                const dummy = document.createElement('input');
                document.body.appendChild(dummy);
                dummy.value = `${shareData.text} ${shareData.url}`;
                dummy.select();
                document.execCommand('copy');
                document.body.removeChild(dummy);
                showToast('추천 메뉴 정보가 클립보드에 복사되었습니다!');
            }
        }

        // Toast Helper
        function showToast(msg) {
            const toast = document.getElementById('toast');
            const toastMsg = document.getElementById('toastMsg');
            toastMsg.innerText = msg;
            toast.classList.remove('opacity-0', 'pointer-events-none');
            setTimeout(() => {
                toast.classList.add('opacity-0', 'pointer-events-none');
            }, 2500);
        }

        function getCategoryEmoji(cat) {
            switch (cat) {
                case '한식': return '🍲';
                case '일식': return '🍱';
                case '중식': return '🥢';
                case '양식': return '🍝';
                case '분식/패스트푸드': return '🍔';
                case '디저트': return '🍰';
                default: return '🍽️';
            }
        }
    </script>
</body>
</html>
