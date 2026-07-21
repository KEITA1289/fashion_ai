<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>FASHION AI</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&family=Noto+Sans+JP:wght@300;400;500;700&display=swap" rel="stylesheet">
    <style>
        :root { --accent: #2563EB; --light-blue: #E0F2FE; --navy: #1E3A8A; --bg: #F8FAFC; }
        body { font-family: 'Inter', 'Noto Sans JP', sans-serif; background-color: var(--bg); color: #0F172A; -webkit-tap-highlight-color: transparent; overflow-x: hidden; }
        
        .bg-home-gradient { background: linear-gradient(135deg, #FFFFFF 0%, #EFF6FF 50%, #DBEAFE 100%); }
        .btn-blue-gradient { background: linear-gradient(135deg, #60A5FA 0%, #2563EB 100%); box-shadow: 0 10px 20px -5px rgba(37, 99, 235, 0.4); border: none; color: white; transition: all 0.2s cubic-bezier(0.4, 0, 0.2, 1); }
        .btn-blue-gradient:active { transform: scale(0.95); opacity: 0.9; }

        .premium-card { background: white; border-radius: 28px; box-shadow: 0 4px 15px rgba(0,0,0,0.03); border: 1px solid rgba(226, 232, 240, 0.8); overflow: hidden; }
        .bottom-nav { position: fixed; bottom: 0; left: 0; right: 0; height: 85px; background: rgba(255, 255, 255, 0.9); backdrop-filter: blur(20px); border-top: 1px solid rgba(0,0,0,0.05); display: flex; justify-content: space-around; align-items: center; z-index: 1000; padding-bottom: 10px; }
        
        .screen { display: none; min-height: 100vh; padding-bottom: 100px; animation: fadeIn 0.3s ease-out; }
        .screen.active { display: block; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

        .toast { position: fixed; bottom: 100px; left: 50%; transform: translateX(-50%); background: #1E293B; color: #FFF; padding: 12px 24px; border-radius: 100px; font-size: 13px; z-index: 2000; opacity: 0; transition: opacity 0.3s; pointer-events: none; }
        
        .item-img-box { aspect-ratio: 3/4; background: #F1F5F9; position: relative; overflow: hidden; }
        .item-img-box img { width: 100%; height: 100%; object-fit: cover; }
        
        .purpose-card.selected { border: 2px solid var(--accent); background: #EFF6FF; }
        input, select, textarea { border: 1px solid #E2E8F0; border-radius: 14px; padding: 12px; width: 100%; outline: none; background: #FFF; font-size: 14px; }
        .no-scrollbar::-webkit-scrollbar { display: none; }
    </style>
</head>
<body class="max-w-md mx-auto relative min-h-screen">

    <!-- トースト通知 -->
    <div id="toast" class="toast">完了しました ✓</div>

    <!-- 画面: ホーム -->
    <div id="screen-home" class="screen active bg-home-gradient">
        <header class="pt-12 px-6 mb-8 text-center">
            <h1 class="text-3xl font-bold tracking-tighter mb-1 italic text-blue-900">FASHION AI</h1>
            <p class="text-[10px] text-blue-500 font-bold uppercase tracking-[0.3em]">あなたの服を、AIがコーディネート</p>
        </header>

        <section class="px-6 mb-8">
            <div class="premium-card p-6 flex justify-between items-center bg-white/60">
                <div>
                    <h2 class="text-[10px] text-gray-400 uppercase font-bold tracking-widest mb-1">学習レベル</h2>
                    <p id="home-lv-text" class="text-xl font-bold italic text-blue-800">Lv.1 初心者</p>
                </div>
                <div id="home-lv-icon" class="w-12 h-12 rounded-full bg-blue-100 flex items-center justify-center text-2xl shadow-inner">🌱</div>
            </div>
        </section>

        <section class="px-6 mb-10 text-center">
            <button onclick="navigateTo('purpose-select')" class="btn-blue-gradient w-full py-8 rounded-[36px] font-bold text-lg flex flex-col items-center justify-center gap-1 shadow-2xl">
                <span>今日のコーデを作る</span>
                <span class="text-[9px] opacity-70 uppercase tracking-widest">AI Stylist Engine</span>
            </button>
        </section>

        <section class="px-6 space-y-6">
            <div>
                <h3 class="text-lg font-bold text-blue-900 italic mb-3">最近追加した服</h3>
                <div id="home-recent-closet" class="grid grid-cols-3 gap-3"></div>
            </div>
            <div>
                <h3 class="text-lg font-bold text-blue-900 italic mb-3">最近の着用履歴</h3>
                <div id="home-recent-history" class="space-y-3"></div>
            </div>
        </section>
    </div>

    <!-- 画面: 目的選択 -->
    <div id="screen-purpose-select" class="screen bg-home-gradient">
        <header class="pt-12 px-6 mb-4 flex items-center">
            <button onclick="navigateTo('home')" class="p-2 -ml-2 text-blue-900 font-bold">← 戻る</button>
        </header>
        <div class="px-6 mb-8">
            <h2 class="text-3xl font-bold text-blue-900 mb-2">今日はどんな予定？</h2>
            <p class="text-sm text-blue-500">目的に合わせて、あなたのクローゼットからコーデを提案します。</p>
        </div>
        <div class="px-6 grid grid-cols-2 gap-4 mb-10" id="purpose-grid">
            <!-- 目的カードが動的に生成されます -->
        </div>
        <div class="px-6 pb-10">
            <button onclick="confirmPurpose()" class="btn-blue-gradient w-full py-5 rounded-3xl font-bold shadow-xl tracking-widest">この目的でコーデを作る</button>
        </div>
    </div>

    <!-- 画面: コーデ提案結果 -->
    <div id="screen-outfit-result" class="screen">
        <header class="pt-12 px-6 mb-4 flex items-center justify-between">
            <button onclick="navigateTo('purpose-select')" class="text-blue-600 font-bold">← 戻る</button>
            <h2 class="font-bold text-lg italic text-blue-900">Proposed Outfit</h2>
            <div class="w-10"></div>
        </header>
        <div class="px-6 space-y-6">
            <div id="result-card" class="premium-card p-6 shadow-2xl">
                <!-- コーデ内容 -->
            </div>
            <div class="space-y-3">
                <button onclick="recordWearing()" class="btn-blue-gradient w-full py-5 rounded-3xl font-bold tracking-widest">👕 今日着た</button>
                <div class="grid grid-cols-3 gap-2">
                    <button onclick="rateResult(2)" class="bg-white border border-blue-100 py-4 rounded-2xl text-xl">❤️</button>
                    <button onclick="rateResult(0)" class="bg-white border border-blue-100 py-4 rounded-2xl text-xl">😐</button>
                    <button onclick="rateResult(-2)" class="bg-white border border-blue-100 py-4 rounded-2xl text-xl">👎</button>
                </div>
                <button onclick="generateOutfit()" class="w-full py-4 bg-white border border-gray-200 rounded-2xl text-[10px] font-bold text-gray-400 uppercase tracking-widest">🔄 別のコーデを見る</button>
            </div>
        </div>
    </div>

    <!-- 画面: クローゼット -->
    <div id="screen-closet" class="screen">
        <header class="pt-12 px-6 mb-6 flex justify-between items-center">
            <h1 class="text-3xl font-bold italic text-blue-900">Closet</h1>
            <button onclick="showAddItem()" class="bg-blue-600 text-white px-5 py-2.5 rounded-full shadow-lg font-bold text-xs">+ 服を追加</button>
        </header>
        <div class="px-6 mb-6 flex gap-2">
            <input type="text" id="closet-search" placeholder="検索..." oninput="renderCloset()">
            <select id="closet-filter-cat" onchange="renderCloset()" class="w-1/3">
                <option value="すべて">すべて</option>
                <option value="トップス">トップス</option>
                <option value="ボトムス">ボトムス</option>
                <option value="アウター">アウター</option>
                <option value="シューズ">シューズ</option>
                <option value="バッグ">バッグ</option>
                <option value="アクセサリー">アクセ</option>
            </select>
        </div>
        <div id="closet-grid" class="px-6 grid grid-cols-2 gap-4"></div>
    </div>

    <!-- 画面: 服の追加 (サブ画面) -->
    <div id="screen-add-item" class="screen">
        <header class="pt-12 px-6 mb-6 flex items-center gap-4">
            <button onclick="navigateTo('closet')" class="text-blue-600 font-bold">← 戻る</button>
            <h1 class="text-xl font-bold text-blue-900 uppercase italic">Add New Item</h1>
        </header>
        <div class="px-6 space-y-6">
            <div class="item-img-box rounded-3xl cursor-pointer flex flex-col items-center justify-center border-2 border-dashed border-blue-200 text-blue-300" onclick="document.getElementById('file-input').click()" id="upload-preview-box">
                <span class="text-4xl mb-2">📸</span>
                <p class="text-xs font-bold uppercase tracking-widest">写真をアップロード</p>
                <img id="add-preview-img" class="hidden">
            </div>
            <input type="file" id="file-input" class="hidden" accept="image/*" onchange="handleFile(event)">
            
            <div class="space-y-4">
                <input type="text" id="add-name" placeholder="アイテム名">
                <div class="grid grid-cols-2 gap-2">
                    <select id="add-cat"><option value="トップス">トップス</option><option value="ボトムス">ボトムス</option><option value="アウター">アウター</option><option value="シューズ">シューズ</option><option value="バッグ">バッグ</option><option value="アクセサリー">アクセ</option></select>
                    <select id="add-season"><option value="春">春</option><option value="夏">夏</option><option value="秋">秋</option><option value="冬">冬</option></select>
                </div>
                <input type="text" id="add-color" placeholder="カラー">
                <input type="text" id="add-brand" placeholder="ブランド">
                <textarea id="add-memo" placeholder="メモ・ブランドなど" rows="2"></textarea>
            </div>
            <button onclick="saveNewItem()" class="btn-blue-gradient w-full py-5 rounded-3xl font-bold tracking-widest uppercase">クローゼットに保存</button>
        </div>
    </div>

    <!-- 画面: お気に入り -->
    <div id="screen-favorites" class="screen">
        <header class="pt-12 px-6 mb-6 text-center"><h1 class="text-3xl font-bold italic text-blue-900">Favorites</h1></header>
        <div class="px-6 flex gap-4 mb-6">
            <button onclick="toggleFavTab('items')" id="fav-tab-items" class="flex-1 border-b-2 border-blue-600 pb-2 font-bold text-blue-900">アイテム</button>
            <button onclick="toggleFavTab('outfits')" id="fav-tab-outfits" class="flex-1 border-b-2 border-transparent pb-2 font-bold text-gray-400">コーデ</button>
        </div>
        <div id="fav-grid" class="px-6 grid grid-cols-2 gap-4"></div>
    </div>

    <!-- 画面: 履歴 -->
    <div id="screen-history" class="screen">
        <header class="pt-12 px-6 mb-8 text-center"><h1 class="text-3xl font-bold italic text-blue-900">History</h1></header>
        <div id="history-list" class="px-6 space-y-4"></div>
    </div>

    <!-- 画面: マイページ -->
    <div id="screen-profile" class="screen">
        <header class="pt-12 px-6 mb-8 flex justify-between items-center">
            <h1 class="text-3xl font-bold italic text-blue-900">My Page</h1>
            <button onclick="navigateTo('settings')" class="text-2xl">⚙️</button>
        </header>
        <div class="px-6 space-y-6 text-center">
            <div class="premium-card p-10 bg-blue-900 text-white flex flex-col items-center">
                <div class="w-20 h-20 bg-white/20 rounded-full flex items-center justify-center text-4xl mb-4">👤</div>
                <h2 id="me-lv-label" class="text-2xl font-bold italic">Lv.1 初心者</h2>
                <p class="text-[10px] opacity-60 uppercase tracking-widest mt-1">Learning status</p>
            </div>
            <div class="grid grid-cols-2 gap-4">
                <div class="premium-card p-6"><p class="text-xs text-gray-400 font-bold mb-1">身長</p><p class="text-xl font-bold"><span id="me-height">--</span> cm</p></div>
                <div class="premium-card p-6"><p class="text-xs text-gray-400 font-bold mb-1">体重</p><p class="text-xl font-bold"><span id="me-weight">--</span> kg</p></div>
            </div>
        </div>
    </div>

    <!-- 画面: 設定 -->
    <div id="screen-settings" class="screen">
        <header class="pt-12 px-6 mb-8 flex items-center gap-4">
            <button onclick="navigateTo('profile')" class="text-blue-600 font-bold">← 戻る</button>
            <h1 class="text-xl font-bold text-blue-900 italic uppercase">Settings</h1>
        </header>
        <div class="px-6 space-y-8">
            <section class="space-y-4">
                <h3 class="font-bold text-blue-900 italic">プロフィール設定</h3>
                <div class="flex items-center gap-4 bg-white p-4 rounded-2xl border">
                    <label class="w-16 text-sm font-bold">身長</label>
                    <input type="number" id="set-height" class="flex-1 text-right border-none p-0 focus:ring-0">
                    <span class="text-gray-400 text-sm">cm</span>
                </div>
                <div class="flex items-center gap-4 bg-white p-4 rounded-2xl border">
                    <label class="w-16 text-sm font-bold">体重</label>
                    <input type="number" id="set-weight" class="flex-1 text-right border-none p-0 focus:ring-0">
                    <span class="text-gray-400 text-sm">kg</span>
                </div>
            </section>
            <button onclick="saveProfile()" class="btn-blue-gradient w-full py-5 rounded-3xl font-bold shadow-lg">設定を保存</button>
        </div>
    </div>

    <!-- 固定下部ナビ -->
    <nav class="bottom-nav">
        <button onclick="navigateTo('home')" id="nav-home" class="flex flex-col items-center text-blue-600">
            <span class="text-2xl">🏠</span><span class="text-[8px] font-bold mt-1 uppercase">Home</span>
        </button>
        <button onclick="navigateTo('closet')" id="nav-closet" class="flex flex-col items-center text-gray-400">
            <span class="text-2xl">👕</span><span class="text-[8px] font-bold mt-1 uppercase">Closet</span>
        </button>
        <button onclick="navigateTo('favorites')" id="nav-favorites" class="flex flex-col items-center text-gray-400">
            <span class="text-2xl">❤️</span><span class="text-[8px] font-bold mt-1 uppercase">Fav</span>
        </button>
        <button onclick="navigateTo('history')" id="nav-history" class="flex flex-col items-center text-gray-400">
            <span class="text-2xl">📖</span><span class="text-[8px] font-bold mt-1 uppercase">History</span>
        </button>
        <button onclick="navigateTo('profile')" id="nav-profile" class="flex flex-col items-center text-gray-400">
            <span class="text-2xl">👤</span><span class="text-[8px] font-bold mt-1 uppercase">Me</span>
        </button>
    </nav>

    <script>
        // --- 1. データ構造 & 永続化 ---
        let appData = {
            items: [],
            history: [],
            favorites: [], // fav outfits
            profile: { height: 175, weight: 65, score: 0 },
            favTab: 'items' // 'items' or 'outfits'
        };

        const STORAGE_KEY = 'fashionAIData_blue_v3';

        function loadData() {
            const saved = localStorage.getItem(STORAGE_KEY);
            if (saved) {
                appData = JSON.parse(saved);
                if (!appData.favorites) appData.favorites = [];
            }
            renderHome();
            updateLvDisplay();
        }

        function saveData() {
            localStorage.setItem(STORAGE_KEY, JSON.stringify(appData));
        }

        // --- 2. 画面遷移ロジック ---
        function navigateTo(screenId) {
            document.querySelectorAll('.screen').forEach(s => s.classList.remove('active'));
            document.getElementById(`screen-${screenId}`).classList.add('active');

            // ナビ強調
            const navIds = ['home', 'closet', 'favorites', 'history', 'profile'];
            navIds.forEach(id => {
                const el = document.getElementById(`nav-${id}`);
                const isMatch = (screenId === id || (screenId === 'purpose-select' && id === 'home') || (screenId === 'outfit-result' && id === 'home'));
                el.classList.toggle('text-blue-600', isMatch);
                el.classList.toggle('text-gray-400', !isMatch);
            });

            // 画面ごとの描画トリガー
            if (screenId === 'closet') renderCloset();
            if (screenId === 'favorites') renderFavs();
            if (screenId === 'history') renderHistory();
            if (screenId === 'home') renderHome();
            if (screenId === 'purpose-select') renderPurposeSelect();
            if (screenId === 'profile') {
                document.getElementById('me-height').innerText = appData.profile.height;
                document.getElementById('me-weight').innerText = appData.profile.weight;
            }
            if (screenId === 'settings') {
                document.getElementById('set-height').value = appData.profile.height;
                document.getElementById('set-weight').value = appData.profile.weight;
            }
            window.scrollTo(0,0);
        }

        function showToast(msg) {
            const t = document.getElementById('toast');
            t.innerText = msg; t.style.opacity = '1';
            setTimeout(() => t.style.opacity = '0', 2500);
        }

        // --- 3. クローゼット機能 (写真圧縮含む) ---
        let tempBase64 = null;

        function showAddItem() {
            navigateTo('add-item');
            tempBase64 = null;
            document.getElementById('add-preview-img').classList.add('hidden');
            document.getElementById('upload-preview-box').querySelector('span').classList.remove('hidden');
            document.getElementById('upload-preview-box').querySelector('p').classList.remove('hidden');
        }

        function handleFile(e) {
            const file = e.target.files[0];
            if (!file) return;

            const reader = new FileReader();
            reader.onload = (event) => {
                const img = new Image();
                img.onload = () => {
                    const canvas = document.createElement('canvas');
                    const ctx = canvas.getContext('2d');
                    let w = img.width, h = img.height, max = 800;
                    if (w > h) { if (w > max) { h *= max / w; w = max; } } else { if (h > max) { w *= max / h; h = max; } }
                    canvas.width = w; canvas.height = h;
                    ctx.drawImage(img, 0, 0, w, h);
                    tempBase64 = canvas.toDataURL('image/jpeg', 0.7);
                    
                    const preview = document.getElementById('add-preview-img');
                    preview.src = tempBase64;
                    preview.classList.remove('hidden');
                    document.getElementById('upload-preview-box').querySelectorAll('span, p').forEach(el => el.classList.add('hidden'));
                };
                img.src = event.target.result;
            };
            reader.readAsDataURL(file);
        }

        function saveNewItem() {
            const name = document.getElementById('add-name').value;
            const cat = document.getElementById('add-cat').value;
            const season = document.getElementById('add-season').value;
            const color = document.getElementById('add-color').value;

            if (!name || !tempBase64) return alert("写真とアイテム名が必要です");

            const item = {
                id: Date.now(),
                name, cat, season, color,
                brand: document.getElementById('add-brand').value,
                memo: document.getElementById('add-memo').value,
                img: tempBase64,
                isFav: false,
                score: 0,
                lastWorn: 0
            };

            appData.items.unshift(item);
            saveData();
            showToast("クローゼットに保存しました ✓");
            
            // リセット
            document.getElementById('add-name').value = "";
            document.getElementById('file-input').value = "";
            navigateTo('closet');
        }

        function renderCloset() {
            const grid = document.getElementById('closet-grid');
            const search = document.getElementById('closet-search').value.toLowerCase();
            const cat = document.getElementById('closet-filter-cat').value;

            const filtered = appData.items.filter(i => {
                const mSearch = i.name.toLowerCase().includes(search) || i.brand.toLowerCase().includes(search);
                const mCat = cat === 'すべて' || i.cat === cat;
                return mSearch && mCat;
            });

            grid.innerHTML = filtered.map(i => `
                <div class="premium-card relative">
                    <button onclick="toggleItemFav(${i.id}, event)" class="absolute top-3 right-3 z-10 w-8 h-8 bg-white/80 rounded-full shadow-sm flex items-center justify-center">
                        ${i.isFav ? '❤️' : '♡'}
                    </button>
                    <div class="item-img-box"><img src="${i.img}"></div>
                    <div class="p-3">
                        <p class="text-[9px] text-gray-400 font-bold uppercase">${i.cat} / ${i.color}</p>
                        <p class="text-[10px] font-bold truncate">${i.name}</p>
                    </div>
                </div>
            `).join('');
        }

        function toggleItemFav(id, e) {
            e.stopPropagation();
            const item = appData.items.find(i => i.id === id);
            if (item) {
                item.isFav = !item.isFav;
                saveData();
                renderCloset();
            }
        }

        // --- 4. 目的選択 & コーデ提案 ---
        const PURPOSES = [
            { name: "デート", icon: "❤️" }, { name: "旅行", icon: "✈️" }, { name: "仕事", icon: "💼" },
            { name: "カジュアル", icon: "👕" }, { name: "雨の日", icon: "☔" }, { name: "暑い日", icon: "☀️" },
            { name: "寒い日", icon: "❄️" }, { name: "おしゃれ", icon: "✨" }, { name: "おまかせ", icon: "🎲" }
        ];
        let selectedPurposeName = "";

        function renderPurposeSelect() {
            const grid = document.getElementById('purpose-grid');
            grid.innerHTML = PURPOSES.map(p => `
                <div onclick="selectPurpose('${p.name}')" id="p-${p.name}" class="purpose-card premium-card p-6 flex flex-col items-center gap-2 cursor-pointer active:scale-95 transition-all">
                    <span class="text-2xl">${p.icon}</span>
                    <span class="text-sm font-bold text-blue-900">${p.name}</span>
                </div>
            `).join('');
            selectedPurposeName = "";
        }

        function selectPurpose(name) {
            selectedPurposeName = name;
            document.querySelectorAll('.purpose-card').forEach(c => c.classList.remove('selected'));
            document.getElementById(`p-${name}`).classList.add('selected');
        }

        function confirmPurpose() {
            if (!selectedPurposeName) return alert("目的を選択してください");
            generateOutfit();
        }

        let currentOutfit = [];

        function generateOutfit() {
            if (appData.items.length < 1) {
                alert("まずクローゼットに服を追加してください");
                return navigateTo('closet');
            }

            // ロジック: スコアリング
            const scoredItems = appData.items.map(item => {
                let s = item.score || 0;
                if (item.isFav) s += 10;
                
                // 重複回避 (直近3回)
                const recentIds = appData.history.slice(0, 3).flatMap(h => h.items.map(i => i.id));
                if (recentIds.includes(item.id)) s -= 30;

                // 季節ロジック (簡易)
                if (selectedPurposeName === "暑い日" && item.season === "夏") s += 20;
                if (selectedPurposeName === "寒い日" && item.season === "冬") s += 20;

                return { ...item, _temp: s + Math.random() * 5 };
            }).sort((a,b) => b._temp - a._temp);

            // カテゴリごとに選出
            const outfit = [];
            const t = scoredItems.find(i => i.cat === 'トップス');
            const b = scoredItems.find(i => i.cat === 'ボトムス');
            const s = scoredItems.find(i => i.cat === 'シューズ');
            const o = scoredItems.find(i => i.cat === 'アウター');

            if (t) outfit.push(t);
            if (b) outfit.push(b);
            if (o && (selectedPurposeName === '寒い日' || Math.random() > 0.5)) outfit.push(o);
            if (s) outfit.push(s);

            currentOutfit = outfit;
            renderResult();
            navigateTo('outfit-result');
        }

        function renderResult() {
            const card = document.getElementById('result-card');
            card.innerHTML = `
                <div class="mb-6"><p class="text-[10px] text-gray-400 font-bold uppercase tracking-widest">Selected for</p><h3 class="text-2xl font-bold italic text-blue-900">${selectedPurposeName}</h3></div>
                <div class="grid grid-cols-2 gap-3 mb-6">
                    ${currentOutfit.map(i => `
                        <div class="space-y-1 text-center">
                            <div class="item-img-box rounded-2xl"><img src="${i.img}"></div>
                            <p class="text-[10px] font-bold truncate mt-1 text-blue-800">${i.name}</p>
                        </div>
                    `).join('')}
                </div>
                <div class="bg-blue-50 p-4 rounded-2xl italic text-[11px] text-blue-600 leading-relaxed">
                    AIの分析: 目的の「${selectedPurposeName}」とあなたの好みを考慮し、最近着ていないアイテムを中心に清潔感のあるスタイルを構築しました。
                </div>
            `;
        }

        function rateResult(p) {
            currentOutfit.forEach(it => {
                const item = appData.items.find(i => i.id === it.id);
                if (item) item.score = (item.score || 0) + p;
            });
            if (p > 0) {
                appData.favorites.unshift({ id: Date.now(), purpose: selectedPurposeName, items: [...currentOutfit], date: new Date().toLocaleDateString() });
            }
            saveData();
            showToast("好みを学習しました ✓");
        }

        function recordWearing() {
            const entry = { id: Date.now(), purpose: selectedPurposeName, date: new Date().toLocaleDateString(), items: [...currentOutfit] };
            appData.history.unshift(entry);
            saveData();
            showToast("履歴に保存しました ✓");
            navigateTo('history');
        }

        // --- 5. 履歴 / お気に入り / ホーム描画 ---
        function renderHistory() {
            const box = document.getElementById('history-list');
            if (appData.history.length === 0) return box.innerHTML = `<p class="py-20 text-center text-gray-300">履歴なし</p>`;
            box.innerHTML = appData.history.map(h => `
                <div class="premium-card p-4 flex gap-4 items-center">
                    <div class="flex -space-x-4">${h.items.slice(0,3).map(it => `<div class="w-12 h-16 rounded-lg border-2 border-white bg-cover bg-center shadow-md" style="background-image:url(${it.img})"></div>`).join('')}</div>
                    <div class="flex-1">
                        <p class="text-[8px] font-bold text-gray-400">${h.date}</p>
                        <p class="font-bold text-sm text-blue-900">${h.purpose}</p>
                    </div>
                    <button onclick="deleteHistory(${h.id})" class="text-xs text-red-300 px-2">削除</button>
                </div>
            `).join('');
        }

        function deleteHistory(id) {
            appData.history = appData.history.filter(h => h.id !== id);
            saveData(); renderHistory();
        }

        function toggleFavTab(tab) {
            appData.favTab = tab;
            document.getElementById('fav-tab-items').className = tab === 'items' ? 'flex-1 border-b-2 border-blue-600 pb-2 font-bold text-blue-900' : 'flex-1 border-b-2 border-transparent pb-2 font-bold text-gray-400';
            document.getElementById('fav-tab-outfits').className = tab === 'outfits' ? 'flex-1 border-b-2 border-blue-600 pb-2 font-bold text-blue-900' : 'flex-1 border-b-2 border-transparent pb-2 font-bold text-gray-400';
            renderFavs();
        }

        function renderFavs() {
            const grid = document.getElementById('fav-grid');
            if (appData.favTab === 'items') {
                const favItems = appData.items.filter(i => i.isFav);
                grid.innerHTML = favItems.map(i => `
                    <div class="premium-card"><div class="item-img-box"><img src="${i.img}"></div><div class="p-3 font-bold text-[10px] text-blue-900">${i.name}</div></div>
                `).join('') || `<p class="col-span-2 py-20 text-center text-gray-300">なし</p>`;
            } else {
                grid.innerHTML = appData.favorites.map(f => `
                    <div class="premium-card p-3 col-span-2 flex gap-3 items-center">
                         <div class="flex -space-x-3">${f.items.slice(0,3).map(it => `<div class="w-10 h-14 rounded border bg-cover bg-center" style="background-image:url(${it.img})"></div>`).join('')}</div>
                         <div class="flex-1 font-bold text-xs text-blue-900">${f.purpose}</div>
                         <button onclick="deleteFavOutfit(${f.id})" class="text-[10px] text-gray-300">削除</button>
                    </div>
                `).join('') || `<p class="col-span-2 py-20 text-center text-gray-300">なし</p>`;
            }
        }

        function deleteFavOutfit(id) {
            appData.favorites = appData.favorites.filter(f => f.id !== id);
            saveData(); renderFavs();
        }

        function renderHome() {
            const recentBox = document.getElementById('home-recent-closet');
            recentBox.innerHTML = appData.items.slice(0, 3).map(i => `<div class="premium-card aspect-[3/4] overflow-hidden"><img src="${i.img}" class="w-full h-full object-cover"></div>`).join('');
            
            const histBox = document.getElementById('home-recent-history');
            histBox.innerHTML = appData.history.slice(0, 2).map(h => `<div class="bg-white/40 p-3 rounded-2xl flex justify-between items-center"><span class="text-xs font-bold text-blue-900">${h.date} ${h.purpose}</span><span class="text-[10px] text-gray-400">Wearing</span></div>`).join('');
            updateLvDisplay();
        }

        function updateLvDisplay() {
            const lv = Math.floor(appData.history.length / 5) + 1;
            const titles = ["初心者", "見習い", "学習中", "理解者", "パートナー"];
            const icons = ["🌱", "🍀", "💎", "✨", "👑"];
            const title = titles[Math.min(lv-1, 4)];
            const icon = icons[Math.min(lv-1, 4)];
            
            document.getElementById('home-lv-text').innerText = `Lv.${lv} ${title}`;
            document.getElementById('home-lv-icon').innerText = icon;
            if (document.getElementById('me-lv-label')) {
                document.getElementById('me-lv-label').innerText = `Lv.${lv} ${title}`;
            }
        }

        function saveProfile() {
            appData.profile.height = document.getElementById('set-height').value;
            appData.profile.weight = document.getElementById('set-weight').value;
            saveData();
            showToast("設定を保存しました ✓");
            navigateTo('profile');
        }

        // 起動
        loadData();
    </script>
</body>
</html>
