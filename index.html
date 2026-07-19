<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>FASHION AI</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&family=Noto+Sans+JP:wght@300;400;500;700&display=swap" rel="stylesheet">
    <style>
        :root { 
            --accent-blue: #2563EB; 
            --light-blue: #E0F2FE;
            --navy-blue: #1E3A8A;
            --bg: #F8FAFC; 
            --card: #FFFFFF; 
        }
        body { font-family: 'Inter', 'Noto Sans JP', sans-serif; background-color: var(--bg); color: #0F172A; -webkit-tap-highlight-color: transparent; }
        
        /* ホーム画面：ブルーグラデーション背景 */
        .bg-home-blue {
            background: linear-gradient(135deg, #FFFFFF 0%, #F0F9FF 40%, #E0F2FE 100%);
        }

        .premium-card { background: var(--card); border-radius: 28px; box-shadow: 0 4px 20px rgba(37, 99, 235, 0.04); border: 1px solid rgba(37, 99, 235, 0.05); }
        
        /* ブルースタイルのボタン */
        .btn-blue-glam {
            background: linear-gradient(135deg, #60A5FA 0%, #2563EB 100%);
            box-shadow: 0 10px 25px -5px rgba(37, 99, 235, 0.4);
            border: none;
            color: white;
            transition: all 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }
        .btn-blue-glam:active { transform: scale(0.95); opacity: 0.9; }

        .bottom-nav { backdrop-filter: blur(20px); background: rgba(255, 255, 255, 0.85); border-top: 1px solid rgba(0,0,0,0.05); }
        .screen { display: none; min-height: 100vh; padding-bottom: 120px; animation: fadeIn 0.3s ease-out; }
        .screen.active { display: block; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

        .modal { display: none; position: fixed; inset: 0; background: rgba(15, 23, 42, 0.4); z-index: 1000; backdrop-filter: blur(8px); }
        .modal-content { position: absolute; bottom: 0; width: 100%; max-width: 28rem; background: #FFF; border-radius: 32px 32px 0 0; padding: 24px; max-height: 90vh; overflow-y: auto; }
        
        .toast { position: fixed; bottom: 110px; left: 50%; transform: translateX(-50%); background: #1E293B; color: #FFF; padding: 14px 28px; border-radius: 100px; font-size: 13px; z-index: 2000; opacity: 0; transition: opacity 0.3s; pointer-events: none; box-shadow: 0 10px 20px rgba(0,0,0,0.1); }
        
        input, select, textarea { border: 1px solid #E2E8F0; border-radius: 14px; padding: 14px; width: 100%; outline: none; background: #F8FAFC; transition: all 0.2s; }
        input:focus { border-color: var(--accent-blue); background: #FFF; }

        .item-img-container { aspect-ratio: 3/4; background: #F1F5F9; overflow: hidden; border-radius: 20px; position: relative; }
        .item-img-container img { width: 100%; height: 100%; object-fit: cover; }
        
        /* 目的選択カードのブルーバリエーション */
        .purpose-card { border: none; transition: all 0.2s; border-radius: 24px; }
        .purpose-card.selected { transform: scale(0.96); box-shadow: inset 0 0 0 3px var(--accent-blue); }
    </style>
</head>
<body class="max-w-md mx-auto relative min-h-screen">

    <div id="toast" class="toast">設定を保存しました ✓</div>

    <!-- ホーム画面 -->
    <div id="screen-home" class="screen active bg-home-blue">
        <header class="pt-12 px-6 mb-10 text-center">
            <h1 class="text-4xl font-bold tracking-tighter mb-1 italic text-blue-900">FASHION AI</h1>
            <p class="text-[10px] text-blue-400 font-bold tracking-[0.4em] uppercase">Intelligence & Clean Style</p>
        </header>

        <section class="px-6 mb-10">
            <div id="lv-card" class="premium-card p-6 flex justify-between items-center bg-white border-blue-100">
                <div>
                    <h2 class="text-[10px] text-blue-400 uppercase font-bold tracking-widest mb-1">AI学習ステータス</h2>
                    <p id="learning-lv-text" class="text-xl font-bold italic text-blue-900">Lv.1 初心者</p>
                </div>
                <div class="w-12 h-12 rounded-full bg-blue-50 flex items-center justify-center text-2xl shadow-inner">🔹</div>
            </div>
        </section>

        <section class="px-6 mb-12">
            <button onclick="startOutfitFlow()" class="btn-blue-glam w-full py-10 rounded-[36px] font-bold text-xl flex flex-col items-center justify-center gap-1">
                <span class="tracking-widest">今日のコーデを作る</span>
                <span class="text-[10px] opacity-80 font-normal uppercase tracking-[0.2em]">Start AI Styling</span>
            </button>
        </section>

        <section class="px-6">
            <div class="flex justify-between items-center mb-5">
                <h2 class="text-2xl font-bold italic text-blue-900">My Closet</h2>
                <button onclick="navigateTo('closet')" class="text-[11px] font-bold text-blue-400 uppercase tracking-widest">すべて見る</button>
            </div>
            <div id="home-closet-preview" class="grid grid-cols-2 gap-4"></div>
        </section>
    </div>

    <!-- 目的選択画面 (ブルーイメージ) -->
    <div id="screen-purpose-select" class="screen bg-home-blue">
        <header class="pt-12 px-6 mb-4 flex items-center">
            <button onclick="navigateTo('home')" class="p-2 -ml-2 text-blue-900"><svg class="h-7 w-7" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-width="2" d="M15 19l-7-7 7-7" /></svg></button>
            <h2 class="text-3xl font-bold ml-2 tracking-tight text-blue-900">今日はどんな予定？</h2>
        </header>
        <div class="px-6 mb-8 text-blue-500 text-sm font-medium">
            爽やかなブルーのAIが、あなたの目的に合う最高の選択を。
        </div>
        <div class="px-6 grid grid-cols-2 gap-4 mb-40" id="purpose-grid-container">
            <!-- 目的別カード (JSで生成) -->
        </div>
        <div class="fixed bottom-24 left-0 right-0 max-w-md mx-auto px-6 pb-6">
            <button onclick="triggerGeneration()" class="btn-blue-glam w-full py-6 rounded-3xl font-bold text-lg tracking-[0.2em] uppercase">
                コーデを提案する
            </button>
        </div>
    </div>

    <!-- コーデ提案結果画面 -->
    <div id="screen-results" class="screen">
        <header class="pt-12 px-6 mb-6 flex justify-between items-center">
            <button onclick="navigateTo('purpose-select')" class="p-2 -ml-2"><svg class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-width="2" d="M15 19l-7-7 7-7" /></svg></button>
            <h2 class="font-bold text-xl uppercase italic text-blue-900">Outfit Result</h2>
            <div class="w-6"></div>
        </header>
        <div class="px-6 space-y-6">
            <div id="main-outfit-card" class="premium-card p-6 shadow-2xl"></div>
            <div class="flex flex-col gap-3">
                <button id="btn-wear-today" class="btn-blue-glam w-full py-5 rounded-3xl font-bold text-sm tracking-widest uppercase">👕 今日着た</button>
                <div class="grid grid-cols-3 gap-2">
                    <button onclick="rateOutfit(2)" class="bg-white border-2 border-blue-50 py-4 rounded-2xl flex flex-col items-center gap-1"><span class="text-xl">❤️</span><span class="text-[8px] font-bold text-blue-600">好き</span></button>
                    <button onclick="rateOutfit(0)" class="bg-white border-2 border-blue-50 py-4 rounded-2xl flex flex-col items-center gap-1"><span class="text-xl">😐</span><span class="text-[8px] font-bold text-gray-400">普通</span></button>
                    <button onclick="rateOutfit(-2)" class="bg-white border-2 border-blue-50 py-4 rounded-2xl flex flex-col items-center gap-1"><span class="text-xl">👎</span><span class="text-[8px] font-bold text-gray-400">なし</span></button>
                </div>
            </div>
        </div>
    </div>

    <!-- クローゼット / お気に入り / 履歴 -->
    <div id="screen-closet" class="screen"><header class="pt-12 px-6 mb-6 flex justify-between items-center"><h1 class="text-2xl font-bold uppercase italic text-blue-900">Closet</h1><button onclick="openModal('modal-add-item')" class="bg-blue-600 text-white px-5 py-3 rounded-full shadow-lg font-bold text-xs">+ 服を追加</button></header><div class="px-6 mb-4 flex gap-2"><input type="text" id="closet-search" placeholder="アイテムを検索..." class="flex-1 text-sm" oninput="renderCloset()"><select id="closet-filter" onchange="renderCloset()" class="w-1/3 text-xs font-bold"><option value="すべて">すべて</option><option value="トップス">トップス</option><option value="ボトムス">ボトムス</option><option value="アウター">アウター</option><option value="シューズ">シューズ</option></select></div><div id="closet-grid" class="px-6 grid grid-cols-2 gap-4"></div></div>
    <div id="screen-favorites" class="screen"><header class="pt-12 px-6 mb-6 text-center"><h1 class="text-2xl font-bold italic uppercase text-blue-900">Favorites</h1></header><div class="px-6 flex gap-4 mb-6"><button onclick="toggleFavTab('items')" id="tab-items" class="flex-1 border-b-2 border-blue-600 pb-2 font-bold text-sm">アイテム</button><button onclick="toggleFavTab('outfits')" id="tab-outfits" class="flex-1 border-b-2 border-transparent text-gray-400 pb-2 font-bold text-sm">コーデ</button></div><div id="fav-container" class="px-6 grid grid-cols-2 gap-4"></div></div>
    <div id="screen-history" class="screen"><header class="pt-12 px-6 mb-6 text-center"><h1 class="text-2xl font-bold italic uppercase text-blue-900">History</h1></header><div id="history-container" class="px-6 space-y-4"></div></div>

    <!-- マイページ画面 (⚙️設定ボタン追加) -->
    <div id="screen-profile" class="screen">
        <header class="pt-12 px-6 mb-8 flex justify-between items-center">
            <h1 class="text-2xl font-bold italic uppercase tracking-tighter text-blue-900">My Page</h1>
            <button onclick="openModal('modal-settings')" class="p-2 bg-blue-50 rounded-full text-blue-600 text-xl">⚙️</button>
        </header>
        
        <div class="px-6 space-y-6">
            <div class="premium-card p-8 bg-blue-900 text-white flex justify-between items-center">
                <div><p class="text-[10px] opacity-60 uppercase tracking-widest mb-1">現在の学習レベル</p><h3 id="display-lv-me" class="text-3xl font-bold italic">LV. 01</h3></div>
                <button onclick="openModal('modal-settings')" class="text-xs font-bold bg-white/20 px-4 py-2 rounded-full">⚙️ 設定</button>
            </div>

            <section class="premium-card p-6 space-y-6">
                <h3 class="text-xs font-bold text-blue-400 uppercase tracking-widest">現在のプロフィール</h3>
                <div class="grid grid-cols-2 gap-6">
                    <div class="text-center border-r border-blue-50">
                        <p class="text-[10px] text-gray-400 font-bold uppercase mb-1">身長</p>
                        <p class="text-2xl font-bold text-blue-900"><span id="me-height-display">---</span> <span class="text-sm">cm</span></p>
                    </div>
                    <div class="text-center">
                        <p class="text-[10px] text-gray-400 font-bold uppercase mb-1">体重</p>
                        <p class="text-2xl font-bold text-blue-900"><span id="me-weight-display">---</span> <span class="text-sm">kg</span></p>
                    </div>
                </div>
                <div class="pt-4 border-t border-blue-50">
                    <p class="text-[10px] text-gray-400 font-bold uppercase mb-1">性別</p>
                    <p class="text-sm font-bold text-blue-900" id="me-gender-display">未設定</p>
                </div>
            </section>
        </div>
    </div>

    <!-- モーダル: 設定画面 (プロフィール編集) -->
    <div id="modal-settings" class="modal" onclick="if(event.target==this) closeModal('modal-settings')">
        <div class="modal-content no-scrollbar">
            <h2 class="text-xl font-bold mb-8 italic uppercase tracking-tight text-blue-900">⚙️ プロフィール設定</h2>
            <div class="space-y-8 pb-10">
                <div class="space-y-6">
                    <!-- 身長入力 -->
                    <div class="flex items-center justify-between gap-4">
                        <label class="text-sm font-bold text-blue-900 w-1/4">身長</label>
                        <div class="flex-1 flex items-center gap-3">
                            <input type="number" id="setting-height" placeholder="175" class="text-right text-lg font-bold">
                            <span class="text-sm font-bold text-blue-400">cm</span>
                        </div>
                    </div>
                    <!-- 体重入力 -->
                    <div class="flex items-center justify-between gap-4">
                        <label class="text-sm font-bold text-blue-900 w-1/4">体重</label>
                        <div class="flex-1 flex items-center gap-3">
                            <input type="number" id="setting-weight" placeholder="65" class="text-right text-lg font-bold">
                            <span class="text-sm font-bold text-blue-400">kg</span>
                        </div>
                    </div>
                    <!-- 性別入力 -->
                    <div class="space-y-2">
                        <label class="text-xs font-bold text-gray-400 uppercase">性別</label>
                        <select id="setting-gender" class="font-bold">
                            <option value="男性">男性</option>
                            <option value="女性">女性</option>
                            <option value="その他">その他</option>
                        </select>
                    </div>
                </div>

                <button onclick="saveSettings()" class="btn-blue-glam w-full py-6 rounded-3xl font-bold text-sm tracking-widest uppercase">
                    設定を保存
                </button>
                <button onclick="closeModal('modal-settings')" class="w-full text-gray-400 text-xs font-bold py-2">キャンセル</button>
            </div>
        </div>
    </div>

    <!-- モーダル: 服を追加 / コーデ詳細 (略) -->
    <div id="modal-add-item" class="modal" onclick="if(event.target==this) closeModal('modal-add-item')">
        <div class="modal-content no-scrollbar">
            <h2 class="text-xl font-bold mb-6 italic uppercase text-blue-900">Add New Item</h2>
            <div class="space-y-6">
                <div class="item-img-container cursor-pointer" onclick="document.getElementById('file-input').click()"><div id="add-preview" class="w-full h-full flex flex-col items-center justify-center text-blue-200"><p class="text-xs font-bold uppercase tracking-widest">写真をアップロード</p></div></div>
                <input type="file" id="file-input" class="hidden" accept="image/*" onchange="previewFile()"><input type="text" id="add-name" placeholder="アイテム名"><div class="grid grid-cols-2 gap-2"><select id="add-cat"><option value="トップス">トップス</option><option value="ボトムス">ボトムス</option><option value="アウター">アウター</option><option value="シューズ">シューズ</option></select><select id="add-season"><option value="春">春</option><option value="夏">夏</option><option value="秋">秋</option><option value="冬">冬</option></select></div><button onclick="addClosetItem()" class="btn-blue-glam w-full py-5 rounded-3xl font-bold text-sm uppercase">クローゼットに追加</button>
            </div>
        </div>
    </div>

    <script>
        // --- データ管理 ---
        let state = {
            closetItems: [],
            history: [],
            favoriteOutfits: [],
            profile: { height: '175', weight: '65', gender: '男性' },
            lastPurpose: '',
            currentOutfit: []
        };

        const STORAGE_KEY = 'fashionAI_blue_v2';
        const PURPOSES = [
            { id: 'date', name: '❤️ デート', color: '#EFF6FF' },
            { id: 'travel', name: '✈️ 旅行', color: '#F0F9FF' },
            { id: 'work', name: '💼 仕事', color: '#F8FAFC' },
            { id: 'casual', name: '👕 カジュアル', color: '#F0FDFA' },
            { id: 'rainy', name: '☔ 雨の日', color: '#F1F5F9' },
            { id: 'hot', name: '☀️ 暑い日', color: '#FEFCE8' },
            { id: 'cold', name: '❄️ 寒い日', color: '#EEF2FF' },
            { id: 'special', name: '✨ 特別な日', color: '#F5F3FF' },
            { id: 'random', name: '🎲 おまかせ', color: 'linear-gradient(135deg, #F0F9FF 0%, #E0F2FE 100%)' }
        ];

        function loadData() {
            const data = localStorage.getItem(STORAGE_KEY);
            if (data) state = JSON.parse(data);
            syncProfileUI();
            renderHome();
        }

        function saveData() {
            try {
                localStorage.setItem(STORAGE_KEY, JSON.stringify(state));
            } catch (e) {
                alert("データの保存に失敗しました。画像のサイズを確認してください。");
            }
        }

        function syncProfileUI() {
            // 表示用
            document.getElementById('me-height-display').innerText = state.profile.height || '---';
            document.getElementById('me-weight-display').innerText = state.profile.weight || '---';
            document.getElementById('me-gender-display').innerText = state.profile.gender || '未設定';
            // 入力用
            document.getElementById('setting-height').value = state.profile.height;
            document.getElementById('setting-weight').value = state.profile.weight;
            document.getElementById('setting-gender').value = state.profile.gender;
        }

        function saveSettings() {
            const h = document.getElementById('setting-height').value;
            const w = document.getElementById('setting-weight').value;
            const g = document.getElementById('setting-gender').value;

            if (!h || !w) {
                alert("身長と体重を入力してください");
                return;
            }

            state.profile.height = h;
            state.profile.weight = w;
            state.profile.gender = g;

            saveData();
            syncProfileUI();
            closeModal('modal-settings');
            showToast("設定を保存しました ✓");
        }

        function navigateTo(screenId) {
            document.querySelectorAll('.screen').forEach(s => s.classList.remove('active'));
            document.getElementById(`screen-${screenId}`).classList.add('active');
            document.querySelectorAll('.nav-btn').forEach(btn => btn.classList.replace('text-black', 'text-gray-300'));
            const mainTabId = (screenId === 'purpose-select' || screenId === 'results') ? 'home' : screenId;
            const activeNav = document.getElementById(`nav-${mainTabId}`);
            if(activeNav) activeNav.classList.replace('text-gray-300', 'text-black');
            
            if(screenId === 'home') renderHome();
            if(screenId === 'closet') renderCloset();
            if(screenId === 'history') renderHistory();
            if(screenId === 'favorites') renderFavs();
            if(screenId === 'purpose-select') renderPurposeGrid();
            window.scrollTo(0,0);
        }

        function showToast(text) {
            const t = document.getElementById('toast');
            t.innerText = text; t.style.opacity = '1';
            setTimeout(() => t.style.opacity = '0', 2500);
        }

        // --- Outfit Flow ---
        function startOutfitFlow() {
            if (state.closetItems.length < 2) { alert("まずクローゼットに服を追加してください。"); navigateTo('closet'); return; }
            navigateTo('purpose-select');
        }

        function renderPurposeGrid() {
            const container = document.getElementById('purpose-grid-container');
            container.innerHTML = PURPOSES.map(p => `
                <div id="purpose-${p.id}" onclick="selectPurpose('${p.id}')" 
                     class="purpose-card premium-card p-6 flex flex-col items-center justify-center cursor-pointer active:scale-95" 
                     style="background: ${p.color}">
                    <span class="text-lg font-bold text-blue-900">${p.name}</span>
                </div>
            `).join('');
        }

        let tempSelectedPurpose = null;
        function selectPurpose(id) {
            tempSelectedPurpose = id;
            document.querySelectorAll('.purpose-card').forEach(c => c.classList.remove('selected'));
            document.getElementById(`purpose-${id}`).classList.add('selected');
        }

        function triggerGeneration() {
            if (!tempSelectedPurpose) { alert("目的を選択してください"); return; }
            const pObj = PURPOSES.find(p => p.id === tempSelectedPurpose);
            generateOutfit(pObj.name);
        }

        function generateOutfit(purposeName) {
            const pool = state.closetItems.map(item => {
                let s = item.score || 0;
                const recentIds = state.history.slice(0, 3).flatMap(h => h.items.map(i => i.id));
                if(recentIds.includes(item.id)) s -= 30;
                return { ...item, _ts: s + Math.random() * 10 };
            });
            const sorted = pool.sort((a,b) => b._ts - a._ts);
            let outfit = [];
            const t = sorted.find(i => i.cat === 'トップス');
            const b = sorted.find(i => i.cat === 'ボトムス');
            const shoes = sorted.find(i => i.cat === 'シューズ');
            if(t) outfit.push(t);
            if(b) outfit.push(b);
            if(shoes) outfit.push(shoes);

            state.currentOutfit = outfit;
            state.lastPurpose = purposeName;
            const container = document.getElementById('main-outfit-card');
            container.innerHTML = `
                <div class="mb-6"><span class="text-[10px] text-blue-400 font-bold uppercase tracking-widest">Outfit for</span><h3 class="text-2xl font-bold italic text-blue-900">${state.lastPurpose}</h3></div>
                <div class="grid grid-cols-2 gap-3 mb-6">${state.currentOutfit.map(i => `<div class="item-img-container aspect-square rounded-xl"><img src="${i.image}"></div>`).join('')}</div>
                <div class="bg-blue-50 p-5 rounded-2xl italic text-[11px] text-blue-700 leading-relaxed">AIが今日のコンディションに合わせて厳選。清潔感のあるブルーのアルゴリズムに基づいた提案です。</div>`;
            navigateTo('results');
        }

        function rateOutfit(points) {
            state.currentOutfit.forEach(item => {
                const i = state.closetItems.find(ci => ci.id === item.id);
                if(i) i.score = (i.score || 0) + points;
            });
            saveData(); showToast("好みを学習しました ✓");
        }

        function confirmWearToday() {
            state.history.unshift({ id: Date.now(), date: new Date().toLocaleDateString(), purpose: state.lastPurpose, items: [...state.currentOutfit] });
            saveData(); showToast("履歴に保存しました ✓"); navigateTo('history');
        }

        // --- Closet & Image ---
        let tempImageBase64 = null;
        function previewFile() {
            const file = document.getElementById('file-input').files[0];
            const reader = new FileReader();
            reader.onload = (e) => {
                const img = new Image();
                img.onload = () => {
                    const canvas = document.createElement('canvas');
                    let w = img.width, h = img.height, max = 800;
                    if(w > h) { if(w > max) { h *= max/w; w = max; } } else { if(h > max) { w *= max/h; h = max; } }
                    canvas.width = w; canvas.height = h;
                    canvas.getContext('2d').drawImage(img, 0, 0, w, h);
                    tempImageBase64 = canvas.toDataURL('image/jpeg', 0.7);
                    document.getElementById('add-preview').innerHTML = `<img src="${tempImageBase64}" class="w-full h-full object-cover rounded-2xl">`;
                };
                img.src = e.target.result;
            };
            reader.readAsDataURL(file);
        }

        function addClosetItem() {
            const name = document.getElementById('add-name').value;
            const cat = document.getElementById('add-cat').value;
            if (!tempImageBase64 || !name) { alert("写真とアイテム名を入力してください"); return; }
            state.closetItems.unshift({ id: Date.now(), name, cat, image: tempImageBase64, score: 0 });
            saveData(); showToast("クローゼットに追加しました ✓"); closeModal('modal-add-item');
            document.getElementById('add-name').value = ''; tempImageBase64 = null;
        }

        function renderCloset() {
            const grid = document.getElementById('closet-grid');
            grid.innerHTML = state.closetItems.map(i => `<div class="premium-card"><div class="item-img-container"><img src="${i.image}"></div><div class="p-3"><p class="text-[9px] text-blue-400 font-bold uppercase">${i.cat}</p><p class="text-[10px] font-bold truncate text-blue-900">${i.name}</p></div></div>`).join('') || `<div class="col-span-2 py-20 text-center text-gray-300 text-xs">アイテムがありません</div>`;
        }

        function renderHistory() {
            const container = document.getElementById('history-container');
            container.innerHTML = state.history.map(h => `<div class="premium-card p-4 flex gap-4 items-center"><div class="flex -space-x-4">${h.items.slice(0,2).map(i => `<div class="w-10 h-14 rounded-lg border-2 border-white bg-cover bg-center" style="background-image:url(${i.image})"></div>`).join('')}</div><div><p class="text-[8px] font-bold text-blue-400 uppercase tracking-widest">${h.date}</p><p class="font-bold text-sm italic tracking-tight text-blue-900">${h.purpose}</p></div></div>`).join('');
        }

        function renderHome() {
            const score = state.history.length + (state.closetItems.length);
            const lv = Math.floor(score / 5) + 1;
            document.getElementById('learning-lv-text').innerText = `Lv.${lv} ${lv < 3 ? '初心者' : 'スタイリスト'}`;
            document.getElementById('display-lv-me').innerText = `LV. ${String(lv).padStart(2, '0')}`;
            const container = document.getElementById('home-closet-preview');
            container.innerHTML = state.closetItems.slice(0, 4).map(it => `<div class="premium-card p-2"><div class="item-img-container rounded-2xl"><img src="${it.image}"></div></div>`).join('') || `<div class="col-span-2 py-10 text-center bg-white rounded-3xl border-2 border-dashed border-blue-50 text-blue-200 text-xs">服を追加してください</div>`;
        }

        function openModal(id) { document.getElementById(id).style.display = 'block'; }
        function closeModal(id) { document.getElementById(id).style.display = 'none'; }

        loadData();
    </script>
</body>
</html>
