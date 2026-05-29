
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
  <title>她说 · 你的树洞</title>
  <style>
    :root {
      --bg: #fdf6f0;
      --card-bg: #ffffff;
      --primary: #e8c5c5;
      --primary-dark: #d4a0a0;
      --accent: #c97d7d;
      --text: #5d4037;
      --text-light: #8b6b5e;
      --text-lighter: #a89080;
      --soft-pink: #f9ecec;
      --rose: #d4a5a5;
      --shadow-sm: 0 2px 12px rgba(180, 150, 140, 0.12);
      --shadow-md: 0 6px 28px rgba(180, 150, 140, 0.18);
      --radius: 20px;
      --transition: 0.3s ease;
      --font-serif: 'Georgia', 'Noto Serif SC', serif;
      --font-sans: 'PingFang SC', 'Microsoft YaHei', sans-serif;
      --read-bg: #fff7e6;
      --replied-bg: #eaf7ea;
      --pending-bg: #fff3e8;
    }

    body.night {
      --bg: #2b2b2b;
      --card-bg: #3a3a3a;
      --primary: #b08a8a;
      --accent: #d4a0a0;
      --text: #e0d6cc;
      --text-light: #bfafa3;
      --text-lighter: #9e8b7e;
      --soft-pink: #4a3a3a;
      --shadow-sm: 0 2px 12px rgba(0,0,0,0.25);
      --shadow-md: 0 6px 28px rgba(0,0,0,0.35);
      --read-bg: #4a4030;
      --replied-bg: #3a4a3a;
      --pending-bg: #4a3a30;
    }

    * { margin: 0; padding: 0; box-sizing: border-box; }
    body {
      font-family: var(--font-sans);
      background: var(--bg);
      color: var(--text);
      min-height: 100vh;
      display: flex;
      justify-content: center;
      align-items: flex-start;
      padding: 20px;
      background-image: radial-gradient(ellipse at 20% 10%, rgba(232,197,197,0.15) 0%, transparent 60%),
                        radial-gradient(ellipse at 80% 85%, rgba(212,165,165,0.1) 0%, transparent 60%);
      background-attachment: fixed;
      transition: background 0.4s, color 0.4s;
    }

    .container {
      width: 100%;
      max-width: 520px;
      display: flex;
      flex-direction: column;
      gap: 14px;
      padding-bottom: 40px;
    }

    .header {
      text-align: center;
      padding: 20px 0 6px;
      position: relative;
    }
    .logo-icon {
      font-size: 44px;
      display: block;
      margin-bottom: 4px;
      animation: gentleBounce 3s infinite;
    }
    @keyframes gentleBounce {
      0%,100%{transform:translateY(0);}
      30%{transform:translateY(-6px);}
      50%{transform:translateY(0);}
      70%{transform:translateY(-3px);}
    }
    h1 {
      font-family: var(--font-serif);
      font-size: 2rem;
      font-weight: 400;
      color: var(--accent);
      letter-spacing: 2px;
    }
    .subtitle {
      font-size: 0.85rem;
      color: var(--text-lighter);
      letter-spacing: 1px;
    }

    .daily-sentence {
      background: var(--soft-pink);
      border-radius: 30px;
      padding: 12px 20px;
      text-align: center;
      font-size: 0.9rem;
      color: var(--accent);
      font-style: italic;
      box-shadow: var(--shadow-sm);
      margin-bottom: 4px;
      transition: all 0.4s;
    }

    .card {
      background: var(--card-bg);
      border-radius: var(--radius);
      padding: 22px;
      box-shadow: var(--shadow-sm);
      border: 1px solid rgba(200,160,150,0.25);
      transition: all 0.3s;
    }

    .entry-cards {
      display: flex;
      gap: 12px;
    }
    .entry-card {
      flex:1;
      background: var(--card-bg);
      border-radius: var(--radius);
      padding: 24px 16px;
      text-align: center;
      cursor: pointer;
      box-shadow: var(--shadow-sm);
      transition: all 0.3s;
      border: 1.5px solid transparent;
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 8px;
      user-select: none;
    }
    .entry-card:hover { transform: translateY(-2px); box-shadow: var(--shadow-md); border-color: #d4a5a5; }
    .entry-card .icon { font-size: 38px; }
    .entry-card .label { font-weight: 500; }

    .btn {
      border: none;
      padding: 12px 24px;
      border-radius: 30px;
      font-size: 0.95rem;
      font-weight: 500;
      letter-spacing: 1px;
      cursor: pointer;
      transition: all 0.25s;
      background: linear-gradient(135deg, #e8b8b8, #d49e9e);
      color: white;
      box-shadow: 0 4px 14px rgba(200,140,140,0.35);
      width: 100%;
    }
    .btn:hover { box-shadow: 0 6px 20px rgba(200,140,140,0.5); transform: translateY(-1px); }
    .btn.secondary {
      background: white;
      color: var(--accent);
      border: 1.5px solid #e0c8c0;
      box-shadow: var(--shadow-sm);
    }
    .btn.danger {
      background: white;
      color: #b57171;
      border: 1.5px solid #e8d0d0;
    }
    .btn.small { padding: 8px 18px; font-size: 0.8rem; width: auto; }

    .form-group { margin-bottom: 14px; }
    .form-group label { display: block; font-size: 0.85rem; margin-bottom: 6px; color: var(--text); }
    input, textarea {
      width: 100%;
      padding: 12px 14px;
      border: 1.5px solid #e0d3c9;
      border-radius: 14px;
      font-size: 0.95rem;
      background: #fefcfb;
      color: var(--text);
      font-family: var(--font-sans);
      resize: vertical;
      outline: none;
    }
    textarea { min-height: 140px; line-height: 1.7; }
    input:focus, textarea:focus { border-color: #d4a5a5; box-shadow: 0 0 0 3px rgba(212,165,165,0.1); }

    .hidden { display: none !important; }
    .back-link { cursor: pointer; color: var(--text-lighter); font-size: 0.85rem; padding: 8px 0; display: inline-block; }

    .letter-item {
      background: var(--card-bg);
      border-radius: 14px;
      padding: 16px;
      margin-bottom: 10px;
      cursor: pointer;
      border-left: 4px solid #e8b8b8;
      transition: all 0.2s;
    }
    .letter-item.read { border-left-color: #f0c084; background: var(--read-bg); }
    .letter-item.replied { border-left-color: #86b886; background: var(--replied-bg); }
    .letter-meta { display: flex; justify-content: space-between; align-items: center; }
    .badge {
      padding: 4px 12px;
      border-radius: 20px;
      font-size: 0.7rem;
      font-weight: 500;
      background: #fff3e8;
      color: #c09070;
    }
    .badge.read { background: #fff7e6; color: #b08050; }
    .badge.replied { background: #eaf7ea; color: #6a9b6a; }

    .watermark {
      position: absolute; top:0; left:0; right:0; bottom:0;
      display: flex; flex-wrap: wrap; align-content: center; justify-content: center;
      gap: 30px 50px; opacity: 0.08; transform: rotate(-16deg);
      font-family: var(--font-serif); font-size: 2rem; color: #b56565;
      pointer-events: none; z-index: 1;
    }

    .reply-card {
      position: relative; background: #fffdfc; border-radius: var(--radius);
      padding: 24px; border: 1.5px solid #f0e0d6; margin-top: 10px;
    }
    .reply-content { position: relative; z-index: 2; white-space: pre-wrap; line-height: 1.9; }

    .mode-toggle {
      position: fixed; top: 20px; right: 20px; background: var(--card-bg);
      border: none; font-size: 24px; border-radius: 50%; width: 44px; height: 44px;
      box-shadow: var(--shadow-sm); cursor: pointer; z-index: 50;
    }

    .toast {
      position: fixed; bottom: 30px; left: 50%; transform: translateX(-50%);
      background: #5d4037; color: white; padding: 10px 24px;
      border-radius: 30px; font-size: 0.85rem; z-index: 200;
      animation: toastIn 0.3s, toastOut 0.3s 2.2s forwards;
    }
    @keyframes toastIn { from{opacity:0;transform:translateX(-50%) translateY(20px);} to{opacity:1;transform:translateX(-50%) translateY(0);} }
    @keyframes toastOut { from{opacity:1;transform:translateX(-50%) translateY(0);} to{opacity:0;transform:translateX(-50%) translateY(-10px);} }

    .destroy-animation {
      position: fixed; top:0; left:0; width:100%; height:100%;
      pointer-events: none; z-index: 999;
    }
    .petal {
      position: absolute;
      font-size: 24px;
      animation: fall 3s linear forwards;
    }
    @keyframes fall {
      0% { transform: translateY(-10vh) rotate(0deg); opacity:1; }
      100% { transform: translateY(110vh) rotate(360deg); opacity:0; }
    }

    @media (max-width: 400px) {
      .entry-cards { flex-direction: column; }
    }
  </style>
</head>
<body>
  <button class="mode-toggle" id="modeToggle" title="切换日/夜间模式">🌙</button>

  <div class="container" id="app">
    <!-- 主页 -->
    <div id="homePage">
      <div class="header">
        <span class="logo-icon">🌸</span>
        <h1>她说</h1>
        <p class="subtitle">你的心事 · 温柔安放</p>
      </div>
      <div class="daily-sentence" id="dailySentence">“今天，也有姐姐在听。” </div>
      <div class="entry-cards">
        <div class="entry-card" onclick="showWritePage()">
          <span class="icon">✍️</span>
          <span class="label">写一封信</span>
          <small style="color:var(--text-lighter);">24-48小时内回信</small>
        </div>
        <div class="entry-card" onclick="showCheckPage()">
          <span class="icon">📬</span>
          <span class="label">查收回信</span>
          <small style="color:var(--text-lighter);">销毁或留存</small>
        </div>
      </div>
      <div style="text-align:center; margin-top:8px;">
        <span onclick="showWarmWall()" style="cursor:pointer; color:var(--accent); font-size:0.9rem;">🌸 温暖传递墙</span>
      </div>
      <div class="admin-entry" style="text-align:center; margin-top:18px; opacity:0.7;" onclick="showAdminLogin()">
        <span style="font-size:0.8rem;">🔐 管理员入口</span>
      </div>
      <div style="text-align:center; margin-top:12px;">
        <button class="btn secondary small" id="playSoundBtn" onclick="toggleSound()">🎵 播放白噪音</button>
      </div>
    </div>

    <!-- 写信页 -->
    <div id="writePage" class="hidden">
      <div class="back-link" onclick="goHome()">← 返回</div>
      <div class="header"><h1>写一封信</h1></div>
      <div class="card">
        <div class="form-group">
          <label>🌷 你的昵称</label>
          <input type="text" id="writeNickname" placeholder="取一个只有你知道的名字" maxlength="30">
        </div>
        <div class="form-group">
          <label>📝 你的心事</label>
          <textarea id="writeContent" placeholder="写下任何你想说的..." maxlength="2000"></textarea>
          <small id="charCount">0/2000</small>
        </div>
        <div style="margin:10px 0; display: flex; align-items: center; gap: 8px;">
          <input type="checkbox" id="delaySend"> <label for="delaySend">⏳ 写完后等待5分钟再发送（让情绪沉淀）</label>
        </div>
        <button class="btn" onclick="submitLetter()">📮 投递信件</button>
        <p style="font-size:0.75rem; color:var(--text-lighter); margin-top:8px;">提交后24-48小时回信，请记住昵称</p>
      </div>
    </div>

    <!-- 查收页 -->
    <div id="checkPage" class="hidden">
      <div class="back-link" onclick="goHome()">← 返回</div>
      <div class="header"><h1>查收回信</h1></div>
      <div class="card" id="checkSearchCard">
        <div class="form-group">
          <label>🔍 你的昵称</label>
          <input type="text" id="checkNickname" placeholder="输入写信时的昵称">
        </div>
        <button class="btn" onclick="searchLetters()">查找我的信件</button>
      </div>
      <div id="lettersListContainer"></div>
      <div id="replyDetailContainer"></div>
    </div>

    <!-- 管理员登录 -->
    <div id="adminLoginPage" class="hidden">
      <div class="back-link" onclick="goHome()">← 返回</div>
      <div class="header"><h1>管理员登录</h1></div>
      <div class="card">
        <div class="form-group">
          <label>🔑 密码</label>
          <input type="password" id="adminPassword" placeholder="管理员密码">
        </div>
        <button class="btn" onclick="adminLogin()">验证</button>
      </div>
    </div>

    <!-- 管理员面板 -->
    <div id="adminPanelPage" class="hidden">
      <div class="back-link" onclick="adminLogout()">← 退出</div>
      <div class="header"><h1>管理面板</h1></div>
      <div class="card">
        <div class="form-group">
          <label>🌸 你的管理员署名</label>
          <input type="text" id="adminSignature" placeholder="例如：木棉姐姐" maxlength="20" onchange="saveAdminSignature()">
        </div>
        <small style="color:var(--text-lighter);">这个名字会显示在回信末尾</small>
      </div>
      <div class="card" style="text-align:center;">
        <span>📨 待回复：<strong id="pendingCount">0</strong> 封</span>
      </div>
      <div id="adminLettersList"></div>
      <div id="adminReplyEditor" class="hidden card">
        <h4>💌 回复信件</h4>
        <p><strong>写给：</strong><span id="adminReplyTo"></span></p>
        <p style="background:var(--soft-pink); padding:10px; border-radius:10px; white-space:pre-wrap;" id="adminOriginalLetter"></p>
        <div class="form-group">
          <textarea id="adminReplyContent" placeholder="写下温暖的回信..." maxlength="3000"></textarea>
        </div>
        <div style="display:flex; gap:8px;">
          <button class="btn secondary small" onclick="cancelAdminReply()">取消</button>
          <button class="btn small" onclick="submitAdminReply()">发送回信</button>
        </div>
      </div>
      <!-- 温暖墙管理 -->
      <div class="card" style="margin-top:10px;">
        <h4 style="margin-bottom:8px;">🌟 温暖传递墙管理</h4>
        <p style="font-size:0.8rem;">从已回复信件中选择，匿名分享给更多人（内容将模糊处理）</p>
        <div id="wallCandidates"></div>
      </div>
    </div>

    <!-- 温暖墙展示页 -->
    <div id="warmWallPage" class="hidden">
      <div class="back-link" onclick="goHome()">← 返回</div>
      <div class="header"><h1>🌸 温暖传递墙</h1></div>
      <div id="wallItems"></div>
    </div>
  </div>

  <!-- 销毁动画容器 -->
  <div class="destroy-animation" id="destroyAnimation"></div>

  <!-- Toast -->
  <div id="toast" class="hidden"></div>

  <!-- 隐藏音频 -->
  <audio id="bgAudio" loop src="https://cdn.pixabay.com/download/audio/2022/03/10/audio_c8c8f0b9b1.mp3?filename=light-rain-ambient-114354.mp3"></audio>

  <script>
    // ---------- 数据 ----------
    const STORAGE_KEY = 'tashuo_letters_v2';
    const WALL_KEY = 'tashuo_warmwall';
    const ADMIN_PWD = 'tashuo2024';
    const SESSION_KEY = 'tashuo_admin_session';

    function getLetters() {
      try { return JSON.parse(localStorage.getItem(STORAGE_KEY)) || []; } catch { return []; }
    }
    function saveLetters(arr) { localStorage.setItem(STORAGE_KEY, JSON.stringify(arr)); }
    function getWall() {
      try { return JSON.parse(localStorage.getItem(WALL_KEY)) || []; } catch { return []; }
    }
    function saveWall(arr) { localStorage.setItem(WALL_KEY, JSON.stringify(arr)); }

    // 初始化模拟数据
    if (!localStorage.getItem(STORAGE_KEY)) {
      const mock = [
        { id:'1', nickname:'迷茫的小鹿', content:'最近和朋友吵架了...', status:'pending', read:false, reply:'', repliedAt:null, createdAt: new Date().toISOString(), signature:'' },
        { id:'2', nickname:'职场新人小雨', content:'刚入职压力好大...', status:'pending', read:false, reply:'', repliedAt:null, createdAt: new Date().toISOString(), signature:'' }
      ];
      saveLetters(mock);
    }

    // 工具
    function escapeHtml(s) { const d = document.createElement('div'); d.textContent = s; return d.innerHTML; }
    function formatTime(iso) {
      if(!iso) return '';
      const d = new Date(iso);
      return d.toLocaleString('zh-CN', {month:'2-digit',day:'2-digit', hour:'2-digit',minute:'2-digit'});
    }

    // ---------- 页面切换 ----------
    function hideAll() {
      ['homePage','writePage','checkPage','adminLoginPage','adminPanelPage','warmWallPage'].forEach(id => document.getElementById(id).classList.add('hidden'));
    }
    window.goHome = function() {
      hideAll(); document.getElementById('homePage').classList.remove('hidden');
      updatePendingCount();
    };
    window.showWritePage = function() {
      hideAll(); document.getElementById('writePage').classList.remove('hidden');
      document.getElementById('writeNickname').value = '';
      document.getElementById('writeContent').value = '';
      document.getElementById('charCount').textContent = '0/2000';
      document.getElementById('delaySend').checked = false;
    };
    window.showCheckPage = function() {
      hideAll(); document.getElementById('checkPage').classList.remove('hidden');
      document.getElementById('checkNickname').value = '';
      document.getElementById('lettersListContainer').innerHTML = '';
      document.getElementById('replyDetailContainer').innerHTML = '';
      document.getElementById('checkSearchCard').classList.remove('hidden');
    };
    window.showAdminLogin = function() {
      if(sessionStorage.getItem(SESSION_KEY)==='true') { showAdminPanel(); return; }
      hideAll(); document.getElementById('adminLoginPage').classList.remove('hidden');
    };
    function showAdminPanel() {
      hideAll(); document.getElementById('adminPanelPage').classList.remove('hidden');
      sessionStorage.setItem(SESSION_KEY, 'true');
      loadAdminSignature();
      renderAdminLetters();
      renderWallCandidates();
      updatePendingCount();
    }
    window.showWarmWall = function() {
      hideAll(); document.getElementById('warmWallPage').classList.remove('hidden');
      renderWallItems();
    };

    // 字数统计
    document.getElementById('writeContent').addEventListener('input', function() {
      document.getElementById('charCount').textContent = this.value.length + '/2000';
    });

    // 敏感词提醒
    const sensitiveWords = ['自杀','不想活','结束生命','伤害自己','自残','死掉','活不下去'];
    function checkSensitive(text) {
      const found = sensitiveWords.filter(w => text.includes(w));
      if(found.length > 0) {
        return confirm('我们很担心你。如果此刻情绪特别难过，请一定先联系信任的人或专业支持。\n\n仍然要发送这封信吗？');
      }
      return true;
    }

    // 写信提交
    window.submitLetter = function() {
      const nickname = document.getElementById('writeNickname').value.trim();
      const content = document.getElementById('writeContent').value.trim();
      if(!nickname || nickname.length<2) { showToast('请输入至少2字昵称'); return; }
      if(!content || content.length<10) { showToast('心事至少10个字哦'); return; }
      if(!checkSensitive(content)) return;

      const delay = document.getElementById('delaySend').checked;
      if(delay) {
        showToast('⏳ 信件将在5分钟后发送，请稍等...');
        setTimeout(() => {
          doSubmit(nickname, content);
        }, 300000); // 5分钟
      } else {
        doSubmit(nickname, content);
      }
    };
    function doSubmit(nickname, content) {
      const letter = {
        id: Date.now().toString(36),
        nickname, content,
        status: 'pending',
        read: false,
        reply: '',
        repliedAt: null,
        createdAt: new Date().toISOString(),
        signature: ''
      };
      const letters = getLetters();
      letters.unshift(letter);
      saveLetters(letters);
      showToast('信件已投递，请记住昵称~');
      goHome();
    }

    // 查收
    window.searchLetters = function() {
      const nickname = document.getElementById('checkNickname').value.trim();
      if(!nickname) return;
      const letters = getLetters().filter(l => l.nickname === nickname && l.status !== 'destroyed');
      const container = document.getElementById('lettersListContainer');
      const detail = document.getElementById('replyDetailContainer');
      detail.innerHTML = '';
      if(letters.length === 0) {
        container.innerHTML = '<div class="card">📭 没有找到信件</div>';
      } else {
        container.innerHTML = letters.map(l => {
          let statusText = l.status==='replied'?'已回复':'待回复';
          let readHint = l.read ? ' (已读)' : '';
          if(l.status==='pending' && l.read) statusText += ' · 姐姐已读';
          return `<div class="letter-item ${l.read?'read':''} ${l.status==='replied'?'replied':''}" onclick="showReplyDetail('${l.id}')">
            <div class="letter-meta"><strong>${escapeHtml(l.nickname)}</strong><span class="badge ${l.status}">${statusText}${readHint}</span></div>
            <small>${formatTime(l.createdAt)}</small>
          </div>`;
        }).join('');
      }
    };

    window.showReplyDetail = function(id) {
      const letter = getLetters().find(l => l.id===id);
      const container = document.getElementById('replyDetailContainer');
      if(!letter) return;
      if(letter.status==='pending') {
        let msg = '你的心事已被阅读，姐姐正在用心回复中…';
        if(!letter.read) msg = '信件已送达，等待姐姐阅读中…';
        container.innerHTML = `<div class="card" style="text-align:center;">💌 ${msg}</div>`;
      } else if(letter.status==='replied') {
        container.innerHTML = `
          <div class="reply-card" id="replyCard">
            <div class="watermark"><span>她说</span><span>她说</span><span>她说</span></div>
            <div class="reply-content">
              <div style="color:var(--accent); margin-bottom:8px;">💌 回信</div>
              <div>${escapeHtml(letter.reply)}</div>
              <div style="text-align:right; margin-top:12px; color:var(--accent);">—— ${escapeHtml(letter.signature||'她说管理员')} 💕</div>
              <small>${formatTime(letter.repliedAt)}</small>
            </div>
          </div>
          <div style="display:flex; gap:8px; margin-top:10px;">
            <button class="btn danger small" onclick="destroyLetter('${letter.id}')">🔥 销毁</button>
            <button class="btn secondary small" onclick="screenshotReply()">📸 截屏保存</button>
          </div>`;
      }
    };

    // 销毁（带动画）
    window.destroyLetter = function(id) {
      if(!confirm('销毁后不留痕迹，确定吗？')) return;
      // 播放花瓣动画
      const animDiv = document.getElementById('destroyAnimation');
      for(let i=0; i<20; i++) {
        const petal = document.createElement('div');
        petal.className = 'petal';
        petal.textContent = '🌸';
        petal.style.left = Math.random()*100 + '%';
        petal.style.animationDelay = Math.random()*0.8 + 's';
        animDiv.appendChild(petal);
        setTimeout(() => petal.remove(), 3500);
      }
      const letters = getLetters();
      const idx = letters.findIndex(l => l.id===id);
      if(idx!==-1) {
        letters[idx].status = 'destroyed';
        letters[idx].content = '';
        letters[idx].reply = '';
        saveLetters(letters);
      }
      document.getElementById('replyDetailContainer').innerHTML = '<div class="card">🕊️ 回信已销毁，愿你轻装前行。</div>';
      showToast('已销毁');
    };

    // 截屏
    window.screenshotReply = function() {
      const card = document.getElementById('replyCard');
      if(!card) return;
      html2canvas(card, {scale:2}).then(canvas => {
        const link = document.createElement('a');
        link.download = '她说_回信.png';
        link.href = canvas.toDataURL();
        link.click();
        showToast('截图已保存，带有她说印记');
      }).catch(() => alert('请允许截屏权限'));
    };

    // 管理员登录
    window.adminLogin = function() {
      if(document.getElementById('adminPassword').value === ADMIN_PWD) {
        showToast('欢迎回来');
        setTimeout(showAdminPanel, 400);
      } else showToast('密码错误');
    };
    window.adminLogout = function() {
      sessionStorage.removeItem(SESSION_KEY);
      goHome();
    };

    // 管理员签名
    function loadAdminSignature() {
      const sig = localStorage.getItem('tashuo_admin_sig') || '';
      document.getElementById('adminSignature').value = sig;
    }
    window.saveAdminSignature = function() {
      localStorage.setItem('tashuo_admin_sig', document.getElementById('adminSignature').value.trim());
    };

    // 渲染管理员列表
    function renderAdminLetters() {
      const letters = getLetters();
      const pending = letters.filter(l => l.status==='pending');
      const replied = letters.filter(l => l.status==='replied');
      let html = '';
      if(pending.length) {
        html += '<h4>⏳ 待回复</h4>';
        pending.forEach(l => {
          html += `<div class="letter-item ${l.read?'read':''}" onclick="openAdminReply('${l.id}')">
            <div class="letter-meta"><strong>${escapeHtml(l.nickname)}</strong><span class="badge ${l.read?'read':'pending'}">${l.read?'已读':'未读'}</span></div>
            <small>${escapeHtml(l.content.substring(0,60))}...</small>
          </div>`;
        });
      }
      if(replied.length) {
        html += '<h4>✅ 已回复</h4>';
        replied.forEach(l => {
          html += `<div class="letter-item replied">${escapeHtml(l.nickname)} · ${formatTime(l.repliedAt)}</div>`;
        });
      }
      document.getElementById('adminLettersList').innerHTML = html || '<p>暂无信件</p>';
      updatePendingCount();
    }

    window.openAdminReply = function(id) {
      const letters = getLetters();
      const l = letters.find(l => l.id===id);
      if(!l) return;
      if(l.status==='replied') { showToast('该信已有姐妹回复'); return; }
      // 标记已读
      if(!l.read) {
        l.read = true;
        saveLetters(letters);
        renderAdminLetters();
      }
      document.getElementById('adminReplyTo').textContent = l.nickname;
      document.getElementById('adminOriginalLetter').textContent = l.content;
      document.getElementById('adminReplyContent').value = '';
      document.getElementById('adminReplyEditor').classList.remove('hidden');
      document.getElementById('adminReplyEditor').dataset.replyToId = id;
    };
    window.cancelAdminReply = function() {
      document.getElementById('adminReplyEditor').classList.add('hidden');
    };
    window.submitAdminReply = function() {
      const id = document.getElementById('adminReplyEditor').dataset.replyToId;
      const content = document.getElementById('adminReplyContent').value.trim();
      if(!content || content.length<20) { showToast('回信至少20字'); return; }
      const letters = getLetters();
      const l = letters.find(l => l.id===id);
      if(l && l.status==='pending') {
        l.status = 'replied';
        l.reply = content;
        l.repliedAt = new Date().toISOString();
        l.signature = document.getElementById('adminSignature').value.trim() || '她说管理员';
        saveLetters(letters);
        showToast('回信已发送');
        cancelAdminReply();
        renderAdminLetters();
      } else showToast('状态已变化');
    };

    function updatePendingCount() {
      const count = getLetters().filter(l => l.status==='pending').length;
      const el = document.getElementById('pendingCount');
      if(el) el.textContent = count;
    }

    // 温暖墙
    function renderWallCandidates() {
      const replied = getLetters().filter(l => l.status==='replied');
      const wall = getWall();
      const container = document.getElementById('wallCandidates');
      container.innerHTML = replied.map(l => {
        const already = wall.some(w => w.letterId === l.id);
        return `<div style="display:flex; justify-content:space-between; align-items:center; margin:6px 0;">
          <span>${escapeHtml(l.nickname)} - ${escapeHtml(l.reply.substring(0,20))}...</span>
          <button class="btn secondary small" ${already?'disabled':''} onclick="addToWall('${l.id}')">${already?'已添加':'加入墙'}</button>
        </div>`;
      }).join('') || '<p>暂无已回复信件</p>';
    }
    window.addToWall = function(letterId) {
      const letter = getLetters().find(l => l.id===letterId);
      if(!letter) return;
      const wall = getWall();
      wall.push({
        letterId: letter.id,
        anonymousContent: letter.content.substring(0,40)+'……',
        replySnippet: letter.reply.substring(0,80)+'……',
        signature: letter.signature || '她说管理员'
      });
      saveWall(wall);
      renderWallCandidates();
      showToast('已添加到温暖墙');
    };
    function renderWallItems() {
      const wall = getWall();
      document.getElementById('wallItems').innerHTML = wall.map(w => `
        <div class="card" style="margin-bottom:10px;">
          <p style="font-style:italic;">“${escapeHtml(w.anonymousContent)}”</p>
          <p style="color:var(--accent); margin-top:6px;">💬 ${escapeHtml(w.replySnippet)}</p>
          <small>—— ${escapeHtml(w.signature)}</small>
        </div>
      `).join('') || '<div class="card">🌸 暂时还没有温暖故事，等管理员姐姐们添加~</div>';
    }

    // 每日一句
    const sentences = [
      '“今天，也有姐姐在听。”',
      '“你不必独自承受所有。”',
      '“慢慢来，我在这里。”',
      '“你的感受，值得被看见。”',
      '“即使微弱的光，也能照亮角落。”'
    ];
    document.getElementById('dailySentence').textContent = sentences[Math.floor(Math.random()*sentences.length)];

    // 夜间模式
    const modeToggle = document.getElementById('modeToggle');
    modeToggle.addEventListener('click', () => {
      document.body.classList.toggle('night');
      modeToggle.textContent = document.body.classList.contains('night') ? '☀️' : '🌙';
    });

    // 白噪音
    let audioPlaying = false;
    window.toggleSound = function() {
      const audio = document.getElementById('bgAudio');
      if(audioPlaying) { audio.pause(); audioPlaying = false; document.getElementById('playSoundBtn').textContent = '🎵 播放白噪音'; }
      else { audio.play().catch(()=>{}); audioPlaying = true; document.getElementById('playSoundBtn').textContent = '🔇 停止'; }
    };

    // Toast
    function showToast(msg) {
      const t = document.getElementById('toast');
      t.textContent = msg; t.classList.remove('hidden');
      setTimeout(() => t.classList.add('hidden'), 2500);
    }

    // 初始化
    updatePendingCount();
  </script>
  <script src="https://cdn.jsdelivr.net/npm/html2canvas@1.4.1/dist/html2canvas.min.js"></script>
</body>
</html>
