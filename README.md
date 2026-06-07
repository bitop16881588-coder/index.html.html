<!DOCTYPE html>
<html lang="zh-TW">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>麻將助理 - 灰藍色系版</title>

<style>
:root {
  --primary-color: #6f8fa8;
  --accent-color: #4f6f8f;
}

body {
  font-family: "Comic Sans MS", "Chalkboard SE", "Comic Neue", "Microsoft JhengHei", sans-serif;
  background-color: #eef4f8;
  margin: 0;
  padding: 15px;
}

.grid-container {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 15px;
  max-width: 1200px;
  margin: auto;
}

.card {
  background: rgba(248, 251, 253, 0.95);
  padding: 15px;
  border-radius: 15px;
  box-shadow: 0 4px 6px rgba(0,0,0,0.05);
  border: 1px solid #d7e2ea;
}

h3 {
  color: var(--accent-color);
  margin-top: 0;
  border-left: 4px solid var(--primary-color);
  padding-left: 10px;
}

.row-input {
  display: flex;
  gap: 5px;
  margin-bottom: 5px;
}

.entry-row {
  align-items: center;
}

.entry-row .player-select {
  width: 48%;
}

.entry-row .score-input {
  width: 34%;
}

.btn-remove-player {
  width: 18%;
  background: #8b9aaa;
  padding: 6px;
  font-size: 13px;
  flex-shrink: 0;
}

.btn-add-player-row {
  background: #5f7894;
  margin-top: 6px;
}

.btn-add-player-row:disabled,
.btn-remove-player:disabled {
  opacity: 0.45;
  cursor: not-allowed;
}

.record-tip {
  font-size: 12px;
  color: #64788a;
  margin: 6px 0 4px;
  line-height: 1.5;
}

select,
input {
  font-family: "Comic Sans MS", "Microsoft JhengHei", sans-serif;
  padding: 6px;
  border: 2px solid #c7d6e2;
  border-radius: 8px;
  box-sizing: border-box;
  width: 100%;
}

button {
  font-family: "Comic Sans MS", "Microsoft JhengHei", sans-serif;
  background: var(--primary-color);
  color: white;
  border: none;
  padding: 8px;
  border-radius: 8px;
  cursor: pointer;
  width: 100%;
  font-weight: bold;
}

button:hover {
  opacity: 0.9;
}

.btn-group {
  display: flex;
  gap: 8px;
  margin-top: 5px;
}

.btn-clear {
  background: #7c8b99;
}

.btn-delete {
  background: #6b7f93;
  margin-top: 5px;
  padding: 6px;
  font-size: 13px;
}

.btn-danger {
  background: #7b8794;
  margin-top: 6px;
  padding: 7px;
  font-size: 13px;
}

table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 10px;
}

th,
td {
  padding: 8px;
  text-align: center;
  border-bottom: 1px solid #eee;
}

.score-pos {
  color: #536f8a;
  font-weight: bold;
}

.score-neg {
  color: #647789;
  font-weight: bold;
}

.fun-box {
  padding: 12px;
  border-radius: 12px;
  margin-bottom: 10px;
  text-align: center;
  box-shadow: inset 0 0 5px rgba(0,0,0,0.05);
}

.king-box {
  background: #edf4f8;
  border: 2px solid #6f8798;
}

.ghost-box {
  background: #f1f5f8;
  border: 2px solid #536f8a;
}

.stat-box {
  background: #fff;
  border: 1px solid #c7d6e2;
  padding: 10px;
  border-radius: 8px;
  margin-top: 8px;
  font-size: 14px;
}

.player-total-row {
  display: flex;
  justify-content: space-between;
  padding: 4px 0;
  border-bottom: 1px dashed #eee;
}

.player-total-row:last-child {
  border-bottom: none;
}

.big-name {
  font-size: 18px;
  font-weight: bold;
  margin-top: 3px;
}

.mj-tile {
  font-family: "Apple LiGothic", "Microsoft JhengHei", "Noto Sans TC", sans-serif;
  width: 36px;
  height: 48px;
  background: #ffffff;
  border: 1px solid #c7d6e2;
  border-radius: 8px;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  font-size: 28px;
  box-shadow: 0 2px 4px rgba(0,0,0,0.05);
  user-select: none;
  transition: background 0.1s;
  font-weight: 900 !important;
  -webkit-text-stroke: 1.2px;
  letter-spacing: -1px;
}

.mj-tile:hover {
  background: #f4f8fb;
}

.mj-tile:active {
  background: #e8f0f6;
}

.mj-tile.no-click {
  cursor: default;
  background: #ffffff;
}

.mj-tile.no-click:hover {
  background: #ffffff;
}

.mj-wan {
  color: #536f8a;
  -webkit-text-stroke-color: #536f8a;
}

.mj-tong {
  color: #647789;
  -webkit-text-stroke-color: #647789;
}

.mj-tiao {
  color: #6f8798;
  -webkit-text-stroke-color: #6f8798;
}

.mj-bai {
  color: #9aaaba;
  -webkit-text-stroke-color: #9aaaba;
}

.tile-display-zone {
  min-height: 58px;
  border: 1.5px dashed #b8c9d8;
  border-radius: 10px;
  display: flex;
  flex-wrap: wrap;
  padding: 10px;
  gap: 8px;
  margin-bottom: 5px;
  background: #ffffff;
  align-items: center;
}

.pool-row {
  display: flex;
  gap: 8px;
  margin-bottom: 10px;
  overflow-x: auto;
  padding-bottom: 4px;
  padding-left: 2px;
}

@media (max-width: 768px) {
  .grid-container {
    grid-template-columns: 1fr;
  }
}
</style>
</head>

<body>
<div class="grid-container">

  <div class="card">
    <h3>📈 戰績統計 (當日)</h3>

    <label for="datePicker" style="font-weight: bold; font-size: 14px;">選擇查詢日期：</label>
    <input type="date" id="datePicker" onchange="updateUI()">

    <button onclick="clearDayData()" class="btn-delete">🗑️ 清除該日所有戰績</button>

    <table>
      <thead>
        <tr>
          <th>當日總勝負</th>
        </tr>
      </thead>
      <tbody id="statsBody"></tbody>
    </table>
  </div>

  <div class="card">
    <h3>🔍 聽牌計算機 (<span id="handCount">0</span>/16)</h3>

    <div id="selectedHandZone" class="tile-display-zone"></div>
    <div id="pool-area"></div>

    <div class="btn-group" style="margin-top: 5px;">
      <button onclick="clearHand()" class="btn-clear" style="width: 30%;">🗑️ 清除</button>
      <button onclick="analyzeTing()" style="width: 70%; background: #5f7894;">分析聽牌</button>
    </div>

    <div id="result" style="margin-top:8px;"></div>
  </div>

  <div class="card">
    <h3>📊 戰績輸入</h3>

    <div id="entryContainer">
      <div class="row-input entry-row">
        <select class="player-select"></select>
        <input type="number" class="score-input" oninput="calcSum()" value="0">
        <button type="button" class="btn-remove-player" onclick="removeEntryRow(this)">刪除</button>
      </div>
    </div>

    <button type="button" id="addEntryRowBtn" onclick="addEntryRow()" class="btn-add-player-row">
      ➕ 新增一位戰績輸入
    </button>

    <div class="record-tip">
      可記錄 1～4 位玩家；4 人完整局會檢查合計是否為 0，1～3 人可作為個人／部分紀錄直接儲存。
    </div>

    <div style="margin:10px 0; font-weight:bold;">
      合計: <span id="totalSum" style="color:#4f6f8f;">0</span>
    </div>

    <div class="btn-group">
      <button onclick="clearInput()" class="btn-clear" style="width: 35%;">🧹 清除</button>
      <button onclick="saveRecord()" style="width: 65%;">💾 儲存本局</button>
    </div>

    <hr style="margin:15px 0; border: 0; border-top: 1px dashed #c7d6e2;">

    <h3>👥 選手管理</h3>

    <div class="row-input">
      <input type="text" id="newPlayerName" placeholder="輸入新選手名稱" style="width: 70%;">
      <button onclick="addPlayer()" style="width:30%;">新增</button>
    </div>

    <button onclick="clearAllPlayers()" class="btn-danger">
      🗑️ 清空所有選手
    </button>
  </div>

  <div class="card">
    <h3>🔥 終身成就總因果看板 💖</h3>

    <div id="funDashboard">
      <div style="color:#7f8d99; text-align:center; padding:20px;">
        請先新增選手並儲存戰績，將自動產生焦點排行！
      </div>
    </div>
  </div>

</div>

<script>
let players = JSON.parse(localStorage.getItem('players')) || [];

let mjData = JSON.parse(localStorage.getItem('mjData')) || {};

let mjHistory = JSON.parse(localStorage.getItem('mjHistory')) || [];

let currentHand = [];

const fullTilesList = [];

const mjTilesData = {
  '萬': {
    class: 'mj-wan',
    icons: ['🀇','🀈','🀉','🀊','🀋','🀌','🀍','🀎','🀏']
  },
  '筒': {
    class: 'mj-tong',
    icons: ['🀙','🀚','🀛','🀜','🀝','🀞','🀟','🀠','🀡']
  },
  '條': {
    class: 'mj-tiao',
    icons: ['🀐','🀑','🀒','🀓','🀔','🀕','🀖','🀗','🀘']
  },
  '字': {
    names: ['東','南','西','北','中','發','白'],
    icons: ['🀀','🀁','🀂','🀃','🀄','🀅','🀆'],
    classes: ['mj-tong','mj-tong','mj-tong','mj-tong','mj-wan','mj-tiao','mj-bai']
  }
};

['萬','筒','條'].forEach(type => {
  for (let i = 1; i <= 9; i++) {
    fullTilesList.push({
      id: i + type,
      text: i + type,
      icon: mjTilesData[type].icons[i - 1],
      class: mjTilesData[type].class
    });
  }
});

mjTilesData['字'].names.forEach((name, idx) => {
  fullTilesList.push({
    id: name,
    text: name,
    icon: mjTilesData['字'].icons[idx],
    class: mjTilesData['字'].classes[idx]
  });
});

function refreshSelectors() {
  document.querySelectorAll('.player-select').forEach((sel, idx) => {
    const val = sel.value;

    if (players.length === 0) {
      sel.innerHTML = `<option value="">請先新增選手</option>`;
      return;
    }

    sel.innerHTML = players.map(p => `<option value="${p}">${p}</option>`).join('');

    if (val && players.includes(val)) {
      sel.value = val;
    } else if (players[idx]) {
      sel.value = players[idx];
    } else {
      sel.value = players[0];
    }
  });

  updateEntryDeleteButtons();
}

function createEntryRow(defaultPlayer = '') {
  const row = document.createElement('div');

  row.className = 'row-input entry-row';

  row.innerHTML = `
    <select class="player-select"></select>
    <input type="number" class="score-input" oninput="calcSum()" value="0">
    <button type="button" class="btn-remove-player" onclick="removeEntryRow(this)">刪除</button>
  `;

  document.getElementById('entryContainer').appendChild(row);

  refreshSelectors();

  if (defaultPlayer && players.includes(defaultPlayer)) {
    row.querySelector('.player-select').value = defaultPlayer;
  }

  calcSum();
}

function addEntryRow() {
  const rows = document.querySelectorAll('#entryContainer .entry-row');

  if (rows.length >= 4) {
    alert('最多只能記錄 4 位玩家喔！');
    return;
  }

  createEntryRow();
}

function removeEntryRow(btn) {
  const rows = document.querySelectorAll('#entryContainer .entry-row');

  if (rows.length <= 1) {
    alert('至少要保留 1 位戰績輸入喔！');
    return;
  }

  btn.closest('.entry-row').remove();

  updateEntryDeleteButtons();

  calcSum();
}

function updateEntryDeleteButtons() {
  const rows = document.querySelectorAll('#entryContainer .entry-row');

  rows.forEach(row => {
    const btn = row.querySelector('.btn-remove-player');

    if (btn) {
      btn.disabled = rows.length <= 1;
    }
  });

  const addBtn = document.getElementById('addEntryRowBtn');

  if (addBtn) {
    addBtn.disabled = rows.length >= 4;
  }
}

function addPlayer() {
  const name = document.getElementById('newPlayerName').value.trim();

  if (name && !players.includes(name)) {
    players.push(name);

    localStorage.setItem('players', JSON.stringify(players));

    refreshSelectors();

    document.getElementById('newPlayerName').value = '';

    updateUI();

    alert(`成功新增選手：${name}`);
  } else if (players.includes(name)) {
    alert("此選手名稱已存在！");
  } else {
    alert("請輸入選手名稱！");
  }
}

function clearAllPlayers() {
  if (confirm("確定要清空所有選手嗎？這不會刪除已儲存戰績，但之後需要重新新增選手。")) {
    players = [];

    localStorage.setItem('players', JSON.stringify(players));

    refreshSelectors();

    updateUI();

    alert("所有選手已清空，請重新新增選手！");
  }
}

const pool = document.getElementById('pool-area');

['萬','筒','條'].forEach(type => {
  const row = document.createElement('div');

  row.className = 'pool-row';

  for (let i = 1; i <= 9; i++) {
    const btn = document.createElement('div');

    btn.className = `mj-tile ${mjTilesData[type].class}`;

    btn.innerText = mjTilesData[type].icons[i - 1];

    btn.title = i + type;

    btn.onclick = () => {
      if (currentHand.length < 16) {
        currentHand.push({
          text: i + type,
          icon: mjTilesData[type].icons[i - 1],
          class: mjTilesData[type].class
        });

        renderHand();
      }
    };

    row.appendChild(btn);
  }

  pool.appendChild(row);
});

const ziRow = document.createElement('div');

ziRow.className = 'pool-row';

mjTilesData['字'].names.forEach((name, idx) => {
  const btn = document.createElement('div');

  btn.className = `mj-tile ${mjTilesData['字'].classes[idx]}`;

  btn.innerText = mjTilesData['字'].icons[idx];

  btn.title = name;

  btn.onclick = () => {
    if (currentHand.length < 16) {
      currentHand.push({
        text: name,
        icon: mjTilesData['字'].icons[idx],
        class: mjTilesData['字'].classes[idx]
      });

      renderHand();
    }
  };

  ziRow.appendChild(btn);
});

pool.appendChild(ziRow);

function renderHand() {
  document.getElementById('handCount').innerText = currentHand.length;

  const zone = document.getElementById('selectedHandZone');

  zone.innerHTML = '';

  currentHand.forEach((tileObj, i) => {
    const el = document.createElement('div');

    el.className = `mj-tile ${tileObj.class}`;

    el.innerText = tileObj.icon;

    el.title = tileObj.text;

    el.onclick = () => {
      currentHand.splice(i, 1);
      renderHand();
    };

    zone.appendChild(el);
  });
}

function analyzeTing() {
  const resDiv = document.getElementById('result');

  if (currentHand.length !== 16) {
    resDiv.innerHTML = `
      <span style="color:#6b7f93; font-weight:bold;">
        ⚠️ 台灣麻將需要選滿 16 張牌才能進行聽牌分析喔！目前: ${currentHand.length} 張
      </span>
    `;
    return;
  }

  let handCounts = {};

  currentHand.forEach(t => {
    handCounts[t.text] = (handCounts[t.text] || 0) + 1;
  });

  let tingList = [];

  fullTilesList.forEach(testTile => {
    if ((handCounts[testTile.text] || 0) >= 4) return;

    let fakeHand = currentHand.map(t => t.text);

    fakeHand.push(testTile.text);

    if (canHu16(fakeHand)) {
      let leftCount = 4 - (handCounts[testTile.text] || 0);

      tingList.push({
        ...testTile,
        left: leftCount
      });
    }
  });

  if (tingList.length === 0) {
    resDiv.innerHTML = `
      <span style="color:#6f7f8d; font-weight:bold;">
        相公或沒聽牌！目前手牌無法湊成任何胡牌型。
      </span>
    `;
  } else {
    let tilesHtml = tingList.map(t => `
      <div style="display:inline-block; text-align:center; margin-right:12px; margin-bottom: 8px;">
        <div class="mj-tile no-click ${t.class}">${t.icon}</div>
        <div style="font-size:11px; color:#5f7386; margin-top:4px; font-weight: bold;">
          剩${t.left}張
        </div>
      </div>
    `).join('');

    resDiv.innerHTML = `
      <div style="font-weight:bold; color:#6f8798; margin-bottom:8px;">
        🎉 恭喜！目前聽牌如下：
      </div>
      <div style="display:flex; flex-wrap:wrap; gap:5px;">
        ${tilesHtml}
      </div>
    `;
  }
}

function canHu16(handTexts) {
  let counts = {};

  handTexts.forEach(t => {
    counts[t] = (counts[t] || 0) + 1;
  });

  for (let tile in counts) {
    if (counts[tile] >= 2) {
      let nextCounts = { ...counts };

      nextCounts[tile] -= 2;

      if (nextCounts[tile] === 0) {
        delete nextCounts[tile];
      }

      if (checkMianZi(nextCounts, 0)) {
        return true;
      }
    }
  }

  return false;
}

function checkMianZi(counts, mianziCount) {
  if (Object.keys(counts).length === 0) {
    return mianziCount === 5;
  }

  let keys = Object.keys(counts).sort();

  let current = keys[0];

  if (counts[current] >= 3) {
    let nextCounts = { ...counts };

    nextCounts[current] -= 3;

    if (nextCounts[current] === 0) {
      delete nextCounts[current];
    }

    if (checkMianZi(nextCounts, mianziCount + 1)) {
      return true;
    }
  }

  if (!['東','南','西','北','中','發','白'].includes(current)) {
    let num = parseInt(current);

    let type = current.replace(/[0-9]/g, '');

    let next1 = (num + 1) + type;

    let next2 = (num + 2) + type;

    if (counts[next1] > 0 && counts[next2] > 0) {
      let nextCounts = { ...counts };

      nextCounts[current]--;

      nextCounts[next1]--;

      nextCounts[next2]--;

      if (nextCounts[current] === 0) {
        delete nextCounts[current];
      }

      if (nextCounts[next1] === 0) {
        delete nextCounts[next1];
      }

      if (nextCounts[next2] === 0) {
        delete nextCounts[next2];
      }

      if (checkMianZi(nextCounts, mianziCount + 1)) {
        return true;
      }
    }
  }

  return false;
}

function clearHand() {
  currentHand = [];

  renderHand();

  document.getElementById('result').innerText = "";
}

function clearInput() {
  document.querySelectorAll('#entryContainer .score-input').forEach(i => {
    i.value = '0';
  });

  const el = document.getElementById('totalSum');

  el.innerText = '0';

  el.style.color = '#4f6f8f';
}

function clearDayData() {
  let date = document.getElementById('datePicker').value;

  if (!date) {
    return alert("請先選擇日期！");
  }

  if (!mjData[date] || Object.keys(mjData[date]).length === 0) {
    return alert(`${date} 本來就沒有戰績資料喔！`);
  }

  if (confirm(`⚠️ 確定要刪除 ${date} 的所有戰績嗎？`)) {
    delete mjData[date];

    mjHistory = mjHistory.filter(h => h.date !== date);

    localStorage.setItem('mjData', JSON.stringify(mjData));

    localStorage.setItem('mjHistory', JSON.stringify(mjHistory));

    updateUI();

    alert(`${date} 的戰績已完全清除！`);
  }
}

function saveRecord() {
  let date = document.getElementById('datePicker').value;

  if (!date) {
    return alert("請先選擇日期！");
  }

  if (players.length === 0) {
    return alert("請先新增選手後再儲存戰績！");
  }

  let sum = 0;

  let gamePlayers = [];

  let hasDuplicate = false;

  document.querySelectorAll('#entryContainer .entry-row').forEach(row => {
    let name = row.querySelector('.player-select').value;

    let score = parseInt(row.querySelector('.score-input').value) || 0;

    if (!name) return;

    if (gamePlayers.some(p => p.name === name)) {
      hasDuplicate = true;
    }

    gamePlayers.push({
      name,
      score
    });

    sum += score;
  });

  if (gamePlayers.length < 1) {
    return alert("請至少選擇 1 位玩家紀錄！");
  }

  if (gamePlayers.length > 4) {
    return alert("最多只能記錄 4 位玩家！");
  }

  if (hasDuplicate) {
    return alert("錯誤：戰績輸入中選擇了重複的選手！");
  }

  if (gamePlayers.length === 4 && sum !== 0) {
    return alert("4 人完整局的總分合計需為 0！目前合計: " + sum);
  }

  if (!mjData[date]) {
    mjData[date] = {};
  }

  gamePlayers.forEach(p => {
    mjData[date][p.name] = (mjData[date][p.name] || 0) + p.score;
  });

  mjHistory.unshift({
    date: date,
    players: gamePlayers
  });

  localStorage.setItem('mjData', JSON.stringify(mjData));

  localStorage.setItem('mjHistory', JSON.stringify(mjHistory));

  updateUI();

  clearInput();

  alert(gamePlayers.length === 4 ? "4 人完整局戰績儲存成功！" : `${gamePlayers.length} 人紀錄儲存成功！`);
}

function updateUI() {
  let date = document.getElementById('datePicker').value;

  const body = document.getElementById('statsBody');

  body.innerHTML = '';

  if (!date) return;

  let data = mjData[date] || {};

  let hasData = false;

  for (let p in data) {
    hasData = true;

    let scoreClass = data[p] >= 0 ? 'score-pos' : 'score-neg';

    body.innerHTML += `
      <tr>
        <td>${p}</td>
        <td class="${scoreClass}">
          ${data[p] >= 0 ? '+' + data[p] : data[p]}
        </td>
      </tr>
    `;
  }

  if (!hasData) {
    body.innerHTML = `
      <tr>
        <td colspan="2" style="color:#7f8d99;">本日尚無戰績資料</td>
      </tr>
    `;
  }

  calculateGlobalDashboard();
}

function calculateGlobalDashboard() {
  const dash = document.getElementById('funDashboard');

  if (players.length === 0) {
    dash.innerHTML = `
      <div class="fun-box" style="background: #eef3f7; border: 2px dashed #a8b8c6; margin-bottom:10px;">
        <div style="font-size: 15px; font-weight: bold; color: #6f7f8d;">
          👥 尚未新增選手
        </div>
        <div style="font-size: 13px; color: #7c8b99; margin-top: 5px;">
          請先在「選手管理」新增你的玩家名單。
        </div>
      </div>
    `;
    return;
  }

  let globalScores = {};

  players.forEach(name => {
    globalScores[name] = 0;
  });

  let hasAnyRecord = false;

  mjHistory.forEach(record => {
    record.players.forEach(p => {
      if (globalScores[p.name] !== undefined) {
        globalScores[p.name] += p.score;

        if (p.score !== 0) {
          hasAnyRecord = true;
        }
      }
    });
  });

  let scoreArray = Object.keys(globalScores).map(name => ({
    name,
    score: globalScores[name]
  }));

  let maxScore = Math.max(...scoreArray.map(p => p.score));

  let minScore = Math.min(...scoreArray.map(p => p.score));

  if (!hasAnyRecord || (maxScore === 0 && minScore === 0)) {
    let playerListHtml = scoreArray.map(p => `
      <div class="player-total-row">
        <span>👤 ${p.name}</span>
        <span style="font-weight:bold; color:#6f7f8d;">0 分</span>
      </div>
    `).join('');

    dash.innerHTML = `
      <div class="fun-box" style="background: #eef3f7; border: 2px dashed #a8b8c6; margin-bottom:10px;">
        <div style="font-size: 15px; font-weight: bold; color: #6f7f8d;">
          ⚔️ 終身戰局剛開啟
        </div>
        <div style="font-size: 13px; color: #7c8b99; margin-top: 5px;">
          目前尚無累積勝負分數！
        </div>
      </div>

      <div class="stat-box">
        <div style="font-weight: bold; margin-bottom: 8px; color: #6f7f8d;">
          📋 選手生涯累計總分：
        </div>
        ${playerListHtml}
      </div>
    `;

    return;
  }

  let kings = scoreArray.filter(p => p.score === maxScore).map(p => p.name);

  let ghosts = scoreArray.filter(p => p.score === minScore).map(p => p.name);

  let gap = maxScore - minScore;

  let kingTitle = kings.length > 1 ? "👑VIP" : "👑 VIP";

  let ghostTitle = ghosts.length > 1 ? "🧛 地獄倒楣鬼" : "🧛 地獄倒楣鬼";

  let sortedScores = scoreArray.sort((a, b) => b.score - a.score);

  let playerListHtml = sortedScores.map(p => {
    let scoreClass = p.score > 0 ? 'score-pos' : (p.score < 0 ? 'score-neg' : '');

    let scoreText = p.score > 0 ? `+${p.score} 分` : `${p.score} 分`;

    return `
      <div class="player-total-row">
        <span>👤 <strong>${p.name}</strong></span>
        <span class="${scoreClass}">${scoreText}</span>
      </div>
    `;
  }).join('');

  dash.innerHTML = `
    <div class="fun-box king-box">
      <div style="font-size: 14px; font-weight: bold; color: #6f8798;">
        ${kingTitle}
      </div>
      <div class="big-name">
        ${kings.join(', ')} <span class="score-pos">+${maxScore}</span>
      </div>
    </div>

    <div class="fun-box ghost-box">
      <div style="font-size: 14px; font-weight: bold; color: #536f8a;">
        ${ghostTitle}
      </div>
      <div class="big-name">
        ${ghosts.join(', ')} <span class="score-neg">${minScore}</span>
      </div>
      <div style="font-size: 12px; color: #6f7f8d; margin-top: 5px;">
        史詩級差距：落後首位 <strong style="color:#536f8a;">${gap}</strong> 分
      </div>
    </div>

    <div class="stat-box">
      <div style="font-weight: bold; margin-bottom: 8px; color: #354a5e;">
        📋 各選手生涯累計排名總分：
      </div>
      ${playerListHtml}
    </div>
  `;
}

function calcSum() {
  let s = 0;

  document.querySelectorAll('#entryContainer .score-input').forEach(i => {
    s += (+i.value || 0);
  });

  let el = document.getElementById('totalSum');

  el.innerText = s;

  el.style.color = (s === 0) ? '#4f6f8f' : '#536f8a';
}

window.onload = () => {
  refreshSelectors();

  let tzoffset = (new Date()).getTimezoneOffset() * 60000;

  let localISODate = (new Date(Date.now() - tzoffset)).toISOString().slice(0, 10);

  document.getElementById('datePicker').value = localISODate;

  updateUI();
};
</script>
</body>
</html>
