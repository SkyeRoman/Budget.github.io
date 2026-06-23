<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Skye & Jordan — Budget Tracker</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link href="https://fonts.googleapis.com/css2?family=Lora:wght@500;700&family=DM+Sans:wght@400;500;700&display=swap" rel="stylesheet">
  <style>
*{box-sizing:border-box;margin:0;padding:0;}
body{font-family:'DM Sans',sans-serif;background:linear-gradient(135deg,#D4DDB8 0%,#F2EBE0 40%,#F5E5D8 100%);min-height:100vh;padding-bottom:60px;}
:root{
  --olive:#6B7C45;--olive-light:#8FA35A;--olive-pale:#D4DDB8;
  --peach:#C9916A;--peach-pale:#F5E5D8;
  --ocean:#2E6E8E;--ocean-light:#4A9ABF;--ocean-pale:#C0DCE8;
  --sk-primary:#B5566A;--sk-pale:#F7E0E6;--sk-income:#8B3A52;
  --jo-primary:#2A5F6E;--jo-pale:#D0EAF0;--jo-income:#1E4A5C;
  --red:#C0392B;--green:#27AE60;--amber:#E67E22;
  --dark:#2A2A2A;--mid:#5A5A5A;--sand:#F2EBE0;
}
.header{background:linear-gradient(135deg,var(--olive),var(--olive-light));padding:20px 24px;box-shadow:0 4px 20px rgba(107,124,69,0.3);}
.header h1{color:#fff;font-family:'Lora',serif;font-size:22px;font-weight:700;}
.header p{color:var(--olive-pale);font-size:12px;margin-top:3px;}
.header-actions{display:flex;gap:8px;flex-wrap:wrap;align-items:center;margin-top:12px;}
.btn{padding:8px 18px;border-radius:50px;border:none;cursor:pointer;font-family:'DM Sans',sans-serif;font-weight:700;font-size:12px;transition:all 0.18s;}
.btn:hover{filter:brightness(1.08);}
.btn-save{background:rgba(255,255,255,0.9);color:var(--ocean);}
.btn-csv{background:rgba(255,255,255,0.2);color:#fff;border:1px solid rgba(255,255,255,0.4);}
.btn-add{background:none;border:1.5px dashed var(--olive-pale);color:var(--olive);padding:7px 14px;border-radius:8px;width:100%;margin-top:6px;cursor:pointer;font-family:'DM Sans',sans-serif;font-weight:700;font-size:12px;}
.btn-delete{width:26px;height:26px;border-radius:50%;border:none;background:#fee;color:#c44;cursor:pointer;font-size:14px;flex-shrink:0;}
.btn-sk{background:linear-gradient(135deg,var(--sk-income),var(--sk-primary));color:#fff;}
.btn-jo{background:linear-gradient(135deg,var(--jo-income),var(--jo-primary));color:#fff;}
.tabs{display:flex;gap:5px;flex-wrap:wrap;padding:16px 16px 0;max-width:1200px;margin:0 auto;}
.tab{padding:8px 16px;border-radius:50px;border:none;cursor:pointer;font-family:'DM Sans',sans-serif;font-size:11px;font-weight:700;background:rgba(255,255,255,0.85);color:var(--mid);transition:all 0.2s;}
.tab.active{color:#fff;}
.tab-household.active{background:linear-gradient(135deg,var(--ocean),var(--ocean-light));}
.tab-jordan.active{background:linear-gradient(135deg,var(--jo-income),var(--jo-primary));}
.tab-skye.active{background:linear-gradient(135deg,var(--sk-income),var(--sk-primary));}
.tab-josav.active{background:linear-gradient(135deg,var(--jo-primary),var(--ocean-light));}
.tab-sksav.active{background:linear-gradient(135deg,var(--sk-primary),var(--peach));}
.tab-nw.active{background:linear-gradient(135deg,#8E6B2E,#C9916A);}
.tab-hist.active{background:linear-gradient(135deg,var(--mid),var(--dark));}
.tab-sum.active{background:linear-gradient(135deg,var(--dark),#3A3A2A);}
.content{max-width:1200px;margin:0 auto;padding:16px;}
.page{display:none;}.page.active{display:block;}
.card{background:#fff;border-radius:18px;padding:20px;box-shadow:0 4px 20px rgba(0,0,0,0.07);border:1.5px solid var(--olive-pale);margin-bottom:16px;}
.card-title{font-family:'Lora',serif;font-size:15px;font-weight:700;color:var(--dark);margin-bottom:14px;}
.card-sk{border-color:var(--sk-pale);}
.card-jo{border-color:var(--jo-pale);}
.grid-2{display:grid;grid-template-columns:1fr 1fr;gap:16px;}
.grid-budget{display:grid;grid-template-columns:360px 1fr;gap:20px;}
@media(max-width:768px){.grid-2{grid-template-columns:1fr;}.grid-budget{grid-template-columns:1fr;}}
.hero{border-radius:20px;padding:24px 28px;position:relative;overflow:hidden;margin-bottom:16px;}
.hero-household{background:linear-gradient(135deg,var(--ocean),var(--olive));}
.hero-jordan{background:linear-gradient(135deg,var(--jo-income),var(--jo-primary));}
.hero-skye{background:linear-gradient(135deg,var(--sk-income),var(--sk-primary));}
.hero-nw-pos{background:linear-gradient(135deg,var(--ocean),var(--olive-light));}
.hero-nw-neg{background:linear-gradient(135deg,#8B3A3A,var(--peach));}
.hero-summary{background:linear-gradient(135deg,var(--dark),#3A3A2A);}
.hero-label{font-size:11px;color:rgba(255,255,255,0.7);font-weight:700;letter-spacing:0.08em;text-transform:uppercase;margin-bottom:6px;}
.hero-grid{display:flex;gap:24px;flex-wrap:wrap;margin-bottom:16px;}
.hero-item-label{font-size:10px;color:rgba(255,255,255,0.65);text-transform:uppercase;}
.hero-item-value{font-family:'Lora',serif;font-weight:700;font-size:18px;color:#fff;}
.hero-item-value.neg{color:#ffaaaa;}
.prog-bar-wrap{height:10px;background:rgba(255,255,255,0.2);border-radius:5px;overflow:hidden;margin:8px 0;}
.prog-bar{height:100%;border-radius:5px;transition:width 0.5s ease;background:rgba(255,255,255,0.7);}
.prog-labels{display:flex;justify-content:space-between;font-size:10px;color:rgba(255,255,255,0.6);}
.stat-cards{display:flex;gap:10px;flex-wrap:wrap;margin-bottom:16px;}
.stat-card{background:#fff;border-radius:14px;padding:14px 16px;flex:1;min-width:0;box-shadow:0 2px 12px rgba(0,0,0,0.07);}
.stat-icon{font-size:18px;margin-bottom:2px;}
.stat-label{font-size:10px;font-weight:700;letter-spacing:0.07em;color:var(--mid);text-transform:uppercase;margin-bottom:3px;}
.stat-value{font-family:'Lora',serif;font-weight:800;font-size:16px;line-height:1;}
.stat-sub{font-size:10px;color:var(--mid);margin-top:3px;}
.input-row{display:flex;gap:6px;align-items:center;margin-bottom:8px;}
.input-row input{border:1.5px solid var(--olive-pale);border-radius:8px;padding:8px 10px;font-size:13px;font-family:'DM Sans',sans-serif;color:var(--dark);outline:none;transition:border-color 0.2s;}
.input-row input:focus{border-color:var(--olive);}
.input-row .input-label{flex:1.2;}
.input-row .input-amount-wrap{display:flex;flex:1;border:1.5px solid var(--olive-pale);border-radius:8px;overflow:hidden;}
.input-row .input-amount-wrap:focus-within{border-color:var(--olive);}
.input-amount-prefix{padding:0 8px;font-size:12px;font-weight:700;background:var(--olive-pale);color:var(--olive);display:flex;align-items:center;}
.input-amount-prefix.sk{background:var(--sk-pale);color:var(--sk-primary);}
.input-amount-prefix.jo{background:var(--jo-pale);color:var(--jo-primary);}
.input-row .input-amount-wrap input{border:none;flex:1;outline:none;padding:8px 10px;font-size:13px;color:var(--dark);}
.type-badge{padding:4px 8px;border-radius:20px;border:none;cursor:pointer;font-size:10px;font-weight:700;flex-shrink:0;}
.type-recurring{background:var(--ocean-pale);color:var(--ocean);}
.type-once{background:var(--peach-pale);color:var(--peach);}
.section-pill{display:inline-block;font-size:11px;font-weight:700;color:#fff;padding:4px 12px;border-radius:6px;margin-bottom:10px;}
.section-pill.income-jo{background:linear-gradient(135deg,var(--jo-income),var(--jo-primary));}
.section-pill.expense-jo{background:linear-gradient(135deg,#8B3A3A,#B05050);}
.section-pill.income-sk{background:linear-gradient(135deg,var(--sk-income),var(--sk-primary));}
.section-pill.expense-sk{background:linear-gradient(135deg,#8B3A3A,#B05050);}
.total-row{display:flex;justify-content:space-between;align-items:center;padding:10px 14px;border-radius:8px;margin-top:6px;}
.total-row .total-label{font-size:12px;font-weight:700;}
.total-row .total-value{font-family:'Lora',serif;font-weight:800;font-size:15px;}
.total-income-jo{background:var(--jo-pale);}
.total-income-jo .total-label,.total-income-jo .total-value{color:var(--jo-primary);}
.total-income-sk{background:var(--sk-pale);}
.total-income-sk .total-label,.total-income-sk .total-value{color:var(--sk-primary);}
.total-expense{background:#fef0f0;}
.total-expense .total-label,.total-expense .total-value{color:#8B3A3A;}
.total-balance-pos{background:var(--ocean-pale);}
.total-balance-pos .total-label,.total-balance-pos .total-value{color:var(--ocean);}
.total-balance-neg{background:#fdd;}
.total-balance-neg .total-label,.total-balance-neg .total-value{color:var(--red);}
.alert-over{background:#fee;border:1.5px solid var(--red);border-radius:10px;padding:10px 14px;margin-bottom:12px;font-size:12px;color:var(--red);font-weight:700;}
.chart-wrap{position:relative;height:200px;}
.chart-wrap.tall{height:260px;}
.pot-tabs{display:flex;gap:6px;flex-wrap:wrap;align-items:center;margin-bottom:14px;}
.pot-tab{padding:7px 14px;border-radius:50px;border:none;cursor:pointer;font-size:11px;font-weight:700;background:#fff;color:var(--mid);box-shadow:0 2px 8px rgba(0,0,0,0.08);transition:all 0.2s;}
.pot-tab.active-sk{background:linear-gradient(135deg,var(--sk-primary),var(--peach));color:#fff;}
.pot-tab.active-jo{background:linear-gradient(135deg,var(--jo-primary),var(--ocean-light));color:#fff;}
.sub-tabs{display:flex;gap:6px;margin-bottom:16px;}
.sub-tab{padding:9px 20px;border-radius:50px;border:none;cursor:pointer;font-size:12px;font-weight:700;background:#fff;color:var(--mid);box-shadow:0 2px 8px rgba(0,0,0,0.08);transition:all 0.2s;}
.sub-tab.active-combined{background:linear-gradient(135deg,var(--ocean),var(--ocean-light));color:#fff;}
.sub-tab.active-skye{background:linear-gradient(135deg,var(--sk-income),var(--sk-primary));color:#fff;}
.sub-tab.active-jordan{background:linear-gradient(135deg,var(--jo-income),var(--jo-primary));color:#fff;}
.asset-row{background:#f9f9f7;border-radius:10px;padding:10px 12px;margin-bottom:8px;}
.asset-row-fields{display:flex;gap:6px;flex-wrap:wrap;align-items:flex-end;}
.asset-field{display:flex;flex-direction:column;gap:3px;}
.asset-field label{font-size:9px;color:var(--mid);text-transform:uppercase;font-weight:700;}
.asset-field input,.asset-field select{border:1.5px solid var(--olive-pale);border-radius:6px;padding:6px 8px;font-size:12px;font-family:'DM Sans',sans-serif;color:var(--dark);outline:none;background:#fff;}
.asset-field.grow{flex:1;min-width:80px;}
.hist-table{width:100%;border-collapse:collapse;font-size:13px;}
.hist-table th{padding:10px 12px;text-align:left;font-size:11px;font-weight:700;color:var(--olive);background:var(--olive-pale);}
.hist-table td{padding:10px 12px;border-bottom:1px solid var(--olive-pale);}
.hist-table tr:nth-child(even){background:#fafaf7;}
.grade-box{border-radius:16px;padding:16px 24px;text-align:center;}
.grade-letter{font-family:'Lora',serif;font-weight:800;font-size:52px;line-height:1;}
.who-wrap{display:flex;gap:0;background:rgba(255,255,255,0.15);border-radius:20px;padding:3px;}
.who-btn{padding:5px 14px;border-radius:17px;border:none;cursor:pointer;font-size:11px;font-weight:700;background:transparent;color:rgba(255,255,255,0.8);transition:all 0.2s;}
.who-btn.active{background:#fff;color:var(--olive);}
input[type=month]{border:none;border-radius:8px;padding:6px 10px;font-size:12px;outline:none;color:var(--dark);background:rgba(255,255,255,0.9);}
.legend{display:flex;flex-wrap:wrap;gap:4px 12px;margin-top:8px;}
.legend-item{display:flex;align-items:center;gap:4px;font-size:10px;color:var(--mid);}
.legend-dot{width:8px;height:8px;border-radius:50%;flex-shrink:0;}
.pill-row{display:flex;gap:8px;flex-wrap:wrap;margin:8px 0;}
.pill{border-radius:20px;padding:6px 14px;font-size:11px;font-weight:700;}
.pill-recurring{background:var(--sk-pale);color:var(--sk-primary);}
.pill-once{background:var(--ocean-pale);color:var(--ocean);}
.add-pot-row{display:flex;gap:6px;align-items:center;flex-wrap:wrap;margin-top:8px;}
.add-pot-row input{border:1.5px solid var(--olive-pale);border-radius:8px;padding:6px 10px;font-size:12px;outline:none;}
.hero-motiv{background:rgba(255,255,255,0.15);border-radius:12px;padding:12px 16px;margin-top:10px;font-size:13px;color:#fff;line-height:1.5;}
.update-toggle{display:flex;border:1.5px solid var(--olive-pale);border-radius:10px;overflow:hidden;margin-bottom:12px;}
.update-toggle button{flex:1;padding:10px;border:none;cursor:pointer;font-size:13px;font-weight:700;font-family:'DM Sans',sans-serif;transition:all 0.2s;}
.add-active{background:var(--jo-primary);color:#fff;}
.take-active{background:#8B3A3A;color:#fff;}
.inactive{background:#fafaf7;color:var(--mid);}
.amount-box{display:flex;align-items:center;border:1.5px solid var(--olive-pale);border-radius:8px;overflow:hidden;}
.amount-box input{border:none;outline:none;padding:10px 12px;font-size:14px;flex:1;font-family:'DM Sans',sans-serif;color:var(--dark);}
.amount-prefix{padding:0 10px;font-size:12px;font-weight:700;align-self:stretch;display:flex;align-items:center;}
.amount-prefix.olive{background:var(--olive-pale);color:var(--olive);}
.amount-prefix.sk{background:var(--sk-pale);color:var(--sk-primary);}
.amount-prefix.jo{background:var(--jo-pale);color:var(--jo-primary);}
.balance-pill{background:var(--ocean-pale);border-radius:10px;padding:10px 14px;display:flex;justify-content:space-between;align-items:center;margin-top:10px;}
.balance-pill .bal-label{font-size:12px;font-weight:700;color:var(--ocean);}
.balance-pill .bal-value{font-family:'Lora',serif;font-weight:800;font-size:16px;color:var(--ocean);}
.loading-screen{position:fixed;inset:0;background:linear-gradient(135deg,#D4DDB8,#F2EBE0);display:flex;flex-direction:column;align-items:center;justify-content:center;z-index:1000;}
.loading-screen h2{font-family:'Lora',serif;color:var(--olive);font-size:24px;margin-bottom:8px;}
.loading-screen p{color:var(--mid);font-size:13px;}
.spinner{width:40px;height:40px;border:4px solid var(--olive-pale);border-top-color:var(--olive);border-radius:50%;animation:spin 0.8s linear infinite;margin-bottom:16px;}
@keyframes spin{to{transform:rotate(360deg);}}

  </style>
  <script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.0/dist/chart.umd.min.js"></script>
</head>
<body>

<!-- LOADING SCREEN -->
<div id="loading-screen" class="loading-screen">
  <div class="spinner"></div>
  <h2>💰 Budget Tracker</h2>
  <p>Loading Skye & Jordan's data…</p>
</div>

<!-- HEADER -->
<div class="header">
  <div style="max-width:1200px;margin:0 auto;">
    <h1>💰 Budget & Savings Tracker</h1>
    <p>2025 — Skye & Jordan</p>
    <div class="header-actions">
      <div class="who-wrap">
        <button class="who-btn active" onclick="setMe('Jordan')" id="btn-jordan">👨 Jordan</button>
        <button class="who-btn" onclick="setMe('Skye')" id="btn-skye">👩 Skye</button>
      </div>
      <input type="month" id="monthPicker" value="">
      <button class="btn btn-save" id="saveBtn" onclick="saveAll()">💾 Save All</button>
      <button class="btn btn-csv" onclick="downloadCSV()">⬇️ CSV</button>
    </div>
  </div>
</div>

<!-- TABS -->
<div class="tabs">
  <button class="tab tab-household active" onclick="showTab('household')">🏠 Household</button>
  <button class="tab tab-jordan" onclick="showTab('jordan')">👨 Jordan Budget</button>
  <button class="tab tab-skye" onclick="showTab('skye')">👩 Skye Budget</button>
  <button class="tab tab-josav" onclick="showTab('josav')">🌊 Jordan Savings</button>
  <button class="tab tab-sksav" onclick="showTab('sksav')">🌸 Skye Savings</button>
  <button class="tab tab-nw" onclick="showTab('nw')">💎 Net Worth</button>
  <button class="tab tab-hist" onclick="showTab('hist')">📅 History</button>
  <button class="tab tab-sum" onclick="showTab('sum')">📋 Summary</button>
</div>

<!-- CONTENT -->
<div class="content">

  <!-- HOUSEHOLD -->
  <div id="page-household" class="page active">
    <div class="hero hero-household">
      <div class="hero-label">🏠 Skye & Jordan — Household Overview</div>
      <div class="hero-grid">
        <div class="hero-item"><div class="hero-item-label">Combined Income</div><div class="hero-item-value" id="hh-income">R 0.00</div></div>
        <div class="hero-item"><div class="hero-item-label">Combined Expenses</div><div class="hero-item-value" id="hh-exp">R 0.00</div></div>
        <div class="hero-item"><div class="hero-item-label">Monthly Balance</div><div class="hero-item-value" id="hh-bal">R 0.00</div></div>
        <div class="hero-item"><div class="hero-item-label">Net Worth</div><div class="hero-item-value" id="hh-nw">R 0.00</div></div>
      </div>
      <div style="font-size:11px;color:rgba(255,255,255,0.75);margin-bottom:6px;" id="hh-split-label">Income split — Skye 50% / Jordan 50%</div>
      <div class="prog-bar-wrap"><div class="prog-bar" id="hh-split-bar" style="width:50%"></div></div>
      <div class="prog-labels"><span id="hh-skye-amt">Skye R 0.00</span><span id="hh-jordan-amt">Jordan R 0.00</span></div>
    </div>
    <div class="grid-2">
      <div class="card card-sk">
        <div class="card-title" style="color:var(--sk-primary)">👩 Skye's Summary</div>
        <div class="total-row total-income-sk"><span class="total-label">Income</span><span class="total-value" id="hh-sk-inc">R 0.00</span></div>
        <div class="total-row total-expense" style="margin-top:6px"><span class="total-label">Expenses</span><span class="total-value" id="hh-sk-exp">R 0.00</span></div>
        <div class="total-row total-balance-pos" style="margin-top:6px"><span class="total-label">Balance</span><span class="total-value" id="hh-sk-bal">R 0.00</span></div>
      </div>
      <div class="card card-jo">
        <div class="card-title" style="color:var(--jo-primary)">👨 Jordan's Summary</div>
        <div class="total-row total-income-jo"><span class="total-label">Income</span><span class="total-value" id="hh-jo-inc">R 0.00</span></div>
        <div class="total-row total-expense" style="margin-top:6px"><span class="total-label">Expenses</span><span class="total-value" id="hh-jo-exp">R 0.00</span></div>
        <div class="total-row total-balance-pos" style="margin-top:6px"><span class="total-label">Balance</span><span class="total-value" id="hh-jo-bal">R 0.00</span></div>
      </div>
    </div>
    <div class="card"><div class="card-title">📊 Income vs Expenses</div><div class="chart-wrap"><canvas id="chart-household"></canvas></div></div>
  </div>

  <!-- JORDAN BUDGET -->
  <div id="page-jordan" class="page">
    <div id="jordan-alert" class="alert-over" style="display:none"></div>
    <div class="stat-cards">
      <div class="stat-card" style="border:2px solid var(--jo-pale)"><div class="stat-icon">💵</div><div class="stat-label">Income</div><div class="stat-value" style="color:var(--jo-primary)" id="jo-stat-inc">R 0.00</div></div>
      <div class="stat-card" style="border:2px solid #fcc"><div class="stat-icon">💸</div><div class="stat-label">Expenses</div><div class="stat-value" style="color:var(--peach)" id="jo-stat-exp">R 0.00</div></div>
      <div class="stat-card" style="border:2px solid var(--ocean-pale)"><div class="stat-icon" id="jo-stat-icon">✅</div><div class="stat-label">Balance</div><div class="stat-value" id="jo-stat-bal">R 0.00</div></div>
    </div>
    <div class="grid-budget">
      <div class="card card-jo">
        <div class="section-pill income-jo">💵 Money In</div>
        <div id="jordan-income-rows"></div>
        <button class="btn-add" onclick="addRow('jordan','income')" style="color:var(--jo-primary);border-color:var(--jo-pale)">+ Add income source</button>
        <div class="total-row total-income-jo" style="margin-top:10px"><span class="total-label">Total Income</span><span class="total-value" id="jo-total-inc">R 0.00</span></div>
        <div class="section-pill expense-jo" style="margin-top:16px">💸 Money Out</div>
        <div style="font-size:10px;color:var(--mid);margin-bottom:8px">🔁 tap badge = recurring / 1× = once-off</div>
        <div id="jordan-expense-rows"></div>
        <button class="btn-add" onclick="addRow('jordan','expense')" style="color:#8B3A3A;border-color:#fcc">+ Add expense</button>
        <div class="pill-row" style="margin-top:10px">
          <div class="pill pill-recurring">🔁 Recurring: <span id="jo-recur">R 0.00</span></div>
          <div class="pill pill-once">1× Once-off: <span id="jo-once">R 0.00</span></div>
        </div>
        <div class="total-row total-expense" style="margin-top:6px"><span class="total-label">Total Expenses</span><span class="total-value" id="jo-total-exp">R 0.00</span></div>
        <div class="total-row total-balance-pos" id="jo-bal-row" style="margin-top:6px"><span class="total-label">Money Left Over</span><span class="total-value" id="jo-total-bal">R 0.00</span></div>
        <div style="margin-top:14px;padding:10px 14px;background:var(--jo-pale);border-radius:10px;">
          <div style="font-size:11px;font-weight:700;color:var(--jo-primary);margin-bottom:6px">📅 Save snapshot for <span id="jo-month-label"></span></div>
          <button onclick="saveMonthSnapshot('Jordan')" style="width:100%;padding:9px;background:linear-gradient(135deg,var(--jo-income),var(--jo-primary));color:#fff;border:none;border-radius:8px;cursor:pointer;font-weight:700;font-size:12px;font-family:'DM Sans',sans-serif">💾 Save to History</button>
        </div>
      </div>
      <div>
        <div class="card card-jo"><div class="card-title" style="color:var(--jo-primary)">📊 Income vs Expenses</div><div class="chart-wrap"><canvas id="chart-jo-bar"></canvas></div></div>
        <div class="grid-2" style="margin-top:16px">
          <div class="card card-jo"><div class="card-title" style="color:var(--jo-primary)">🍩 Expense Split</div><div class="chart-wrap"><canvas id="chart-jo-pie"></canvas></div><div class="legend" id="jo-legend"></div></div>
          <div class="card card-jo"><div class="card-title" style="color:var(--jo-primary)">📉 Budget Used</div>
            <div style="text-align:center;padding:20px 0">
              <div style="font-size:36px;font-weight:800;font-family:'Lora',serif;color:var(--jo-primary)" id="jo-pct">0%</div>
              <div style="font-size:11px;color:var(--mid)">of income spent</div>
              <div style="height:8px;background:var(--jo-pale);border-radius:4px;overflow:hidden;margin-top:14px"><div id="jo-pct-bar" style="height:100%;border-radius:4px;background:linear-gradient(90deg,var(--jo-income),var(--jo-primary));transition:width 0.5s;width:0%"></div></div>
              <div id="jo-pct-warn" style="margin-top:8px;font-size:11px;font-weight:700;display:none"></div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- SKYE BUDGET -->
  <div id="page-skye" class="page">
    <div id="skye-alert" class="alert-over" style="display:none"></div>
    <div class="stat-cards">
      <div class="stat-card" style="border:2px solid var(--sk-pale)"><div class="stat-icon">💵</div><div class="stat-label">Income</div><div class="stat-value" style="color:var(--sk-primary)" id="sk-stat-inc">R 0.00</div></div>
      <div class="stat-card" style="border:2px solid #fcc"><div class="stat-icon">💸</div><div class="stat-label">Expenses</div><div class="stat-value" style="color:var(--peach)" id="sk-stat-exp">R 0.00</div></div>
      <div class="stat-card" style="border:2px solid var(--ocean-pale)"><div class="stat-icon" id="sk-stat-icon">✅</div><div class="stat-label">Balance</div><div class="stat-value" id="sk-stat-bal">R 0.00</div></div>
    </div>
    <div class="grid-budget">
      <div class="card card-sk">
        <div class="section-pill income-sk">💵 Money In</div>
        <div id="skye-income-rows"></div>
        <button class="btn-add" onclick="addRow('skye','income')" style="color:var(--sk-primary);border-color:var(--sk-pale)">+ Add income source</button>
        <div class="total-row total-income-sk" style="margin-top:10px"><span class="total-label">Total Income</span><span class="total-value" id="sk-total-inc">R 0.00</span></div>
        <div class="section-pill expense-sk" style="margin-top:16px">💸 Money Out</div>
        <div style="font-size:10px;color:var(--mid);margin-bottom:8px">🔁 tap badge = recurring / 1× = once-off</div>
        <div id="skye-expense-rows"></div>
        <button class="btn-add" onclick="addRow('skye','expense')" style="color:#8B3A3A;border-color:#fcc">+ Add expense</button>
        <div class="pill-row" style="margin-top:10px">
          <div class="pill pill-recurring">🔁 Recurring: <span id="sk-recur">R 0.00</span></div>
          <div class="pill pill-once">1× Once-off: <span id="sk-once">R 0.00</span></div>
        </div>
        <div class="total-row total-expense" style="margin-top:6px"><span class="total-label">Total Expenses</span><span class="total-value" id="sk-total-exp">R 0.00</span></div>
        <div class="total-row total-balance-pos" id="sk-bal-row" style="margin-top:6px"><span class="total-label">Money Left Over</span><span class="total-value" id="sk-total-bal">R 0.00</span></div>
        <div style="margin-top:14px;padding:10px 14px;background:var(--sk-pale);border-radius:10px;">
          <div style="font-size:11px;font-weight:700;color:var(--sk-primary);margin-bottom:6px">📅 Save snapshot for <span id="sk-month-label"></span></div>
          <button onclick="saveMonthSnapshot('Skye')" style="width:100%;padding:9px;background:linear-gradient(135deg,var(--sk-income),var(--sk-primary));color:#fff;border:none;border-radius:8px;cursor:pointer;font-weight:700;font-size:12px;font-family:'DM Sans',sans-serif">💾 Save to History</button>
        </div>
      </div>
      <div>
        <div class="card card-sk"><div class="card-title" style="color:var(--sk-primary)">📊 Income vs Expenses</div><div class="chart-wrap"><canvas id="chart-sk-bar"></canvas></div></div>
        <div class="grid-2" style="margin-top:16px">
          <div class="card card-sk"><div class="card-title" style="color:var(--sk-primary)">🍩 Expense Split</div><div class="chart-wrap"><canvas id="chart-sk-pie"></canvas></div><div class="legend" id="sk-legend"></div></div>
          <div class="card card-sk"><div class="card-title" style="color:var(--sk-primary)">📉 Budget Used</div>
            <div style="text-align:center;padding:20px 0">
              <div style="font-size:36px;font-weight:800;font-family:'Lora',serif;color:var(--sk-primary)" id="sk-pct">0%</div>
              <div style="font-size:11px;color:var(--mid)">of income spent</div>
              <div style="height:8px;background:var(--sk-pale);border-radius:4px;overflow:hidden;margin-top:14px"><div id="sk-pct-bar" style="height:100%;border-radius:4px;background:linear-gradient(90deg,var(--sk-income),var(--sk-primary));transition:width 0.5s;width:0%"></div></div>
              <div id="sk-pct-warn" style="margin-top:8px;font-size:11px;font-weight:700;display:none"></div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- JORDAN SAVINGS -->
  <div id="page-josav" class="page">
    <div class="pot-tabs" id="jo-pot-tabs"></div>
    <div class="add-pot-row">
      <input type="text" id="jo-new-dream" placeholder="Dream name e.g. PS5" style="width:130px">
      <input type="number" id="jo-new-goal" placeholder="Goal R" style="width:90px">
      <button class="btn btn-jo" onclick="addPot('jordan')">+ Add Pot</button>
    </div>
    <div id="jo-pot-content" style="margin-top:16px"></div>
  </div>

  <!-- SKYE SAVINGS -->
  <div id="page-sksav" class="page">
    <div class="pot-tabs" id="sk-pot-tabs"></div>
    <div class="add-pot-row">
      <input type="text" id="sk-new-dream" placeholder="Dream name" style="width:130px">
      <input type="number" id="sk-new-goal" placeholder="Goal R" style="width:90px">
      <button class="btn btn-sk" onclick="addPot('skye')">+ Add Pot</button>
    </div>
    <div id="sk-pot-content" style="margin-top:16px"></div>
  </div>

  <!-- NET WORTH -->
  <div id="page-nw" class="page">
    <div class="sub-tabs">
      <button class="sub-tab active-combined" onclick="setNwTab('combined')" id="nwt-combined">🏠 Combined</button>
      <button class="sub-tab" onclick="setNwTab('skye')" id="nwt-skye">👩 Skye</button>
      <button class="sub-tab" onclick="setNwTab('jordan')" id="nwt-jordan">👨 Jordan</button>
    </div>
    <div id="nw-hero"></div>
    <div class="grid-2">
      <div class="card">
        <div class="card-title">🏦 Assets — What You Own</div>
        <div style="font-size:11px;color:var(--mid);margin-bottom:10px">Tag Owner to split individual net worth. Savings pots auto-included.</div>
        <div id="assets-rows"></div>
        <button class="btn-add" onclick="addAsset()">+ Add asset</button>
        <div style="margin-top:10px;padding:10px 14px;background:var(--olive-pale);border-radius:10px;">
          <div style="font-size:11px;font-weight:700;color:var(--olive);margin-bottom:4px">💡 Savings auto-included</div>
          <div style="display:flex;justify-content:space-between;font-size:11px"><span style="color:var(--mid)">Skye's pots</span><span style="font-weight:700;color:var(--sk-primary)" id="nw-sk-sav">R 0.00</span></div>
          <div style="display:flex;justify-content:space-between;font-size:11px;margin-top:3px"><span style="color:var(--mid)">Jordan's pots</span><span style="font-weight:700;color:var(--jo-primary)" id="nw-jo-sav">R 0.00</span></div>
        </div>
      </div>
      <div class="card">
        <div class="card-title">💳 Liabilities — What You Owe</div>
        <div style="font-size:11px;color:var(--mid);margin-bottom:10px">Tag Owner to split debt into individual net worth.</div>
        <div id="debts-rows"></div>
        <button class="btn-add" onclick="addDebt()">+ Add debt / loan</button>
        <div style="margin-top:10px;padding:10px 14px;background:#fef0f0;border-radius:10px;">
          <div style="font-size:11px;font-weight:700;color:var(--red);margin-bottom:4px">Total Debt</div>
          <div style="display:flex;justify-content:space-between;font-size:11px"><span style="color:var(--mid)">Skye's share</span><span style="font-weight:700;color:var(--sk-primary)" id="nw-sk-debt">R 0.00</span></div>
          <div style="display:flex;justify-content:space-between;font-size:11px;margin-top:3px"><span style="color:var(--mid)">Jordan's share</span><span style="font-weight:700;color:var(--jo-primary)" id="nw-jo-debt">R 0.00</span></div>
        </div>
      </div>
    </div>
  </div>

  <!-- HISTORY -->
  <div id="page-hist" class="page">
    <div id="hist-chart-card" class="card" style="display:none"><div class="card-title">📊 Month-by-Month Trend</div><div class="chart-wrap tall"><canvas id="chart-history"></canvas></div></div>
    <div class="card">
      <div class="card-title">🗂️ Monthly Records</div>
      <div id="hist-empty" style="text-align:center;padding:40px 20px;color:var(--mid)">
        <div style="font-size:40px;margin-bottom:12px">📅</div>
        <div style="font-family:'Lora',serif;font-size:18px;margin-bottom:8px">No history yet</div>
        <div style="font-size:13px">Use "Save to History" in each budget tab to start tracking.</div>
      </div>
      <div style="overflow-x:auto"><table class="hist-table" id="hist-table" style="display:none">
        <thead><tr><th>Month</th><th>Skye Income</th><th>Skye Expenses</th><th>Jordan Income</th><th>Jordan Expenses</th><th>Combined Balance</th></tr></thead>
        <tbody id="hist-tbody"></tbody>
      </table></div>
    </div>
  </div>

  <!-- SUMMARY -->
  <div id="page-sum" class="page">
    <div class="hero hero-summary" style="padding:28px 32px">
      <div style="display:flex;justify-content:space-between;align-items:flex-start;flex-wrap:wrap;gap:16px">
        <div>
          <div class="hero-label">📋 Monthly Financial Report</div>
          <div style="font-family:'Lora',serif;font-weight:700;font-size:26px;color:#fff;margin-bottom:4px" id="sum-month-title">Summary</div>
          <div style="font-size:13px;color:rgba(255,255,255,0.65)">Skye & Jordan's Household</div>
        </div>
        <div id="sum-grade-box" class="grade-box" style="border:2px solid #27AE60;background:rgba(39,174,96,0.2)">
          <div class="grade-letter" id="sum-grade" style="color:#27AE60">A</div>
          <div style="font-size:10px;color:rgba(255,255,255,0.6);font-weight:700;margin-top:4px">MONTH GRADE</div>
        </div>
      </div>
      <div style="margin-top:20px;padding:14px 18px;background:rgba(255,255,255,0.07);border-radius:12px;font-size:14px;color:rgba(255,255,255,0.9);line-height:1.6" id="sum-msg"></div>
    </div>
    <div class="stat-cards">
      <div class="stat-card" style="text-align:center;border:2px solid rgba(107,124,69,0.2)"><div style="font-size:24px;margin-bottom:6px">💵</div><div class="stat-label">Total Income</div><div class="stat-value" style="color:var(--olive)" id="sum-income">R 0.00</div></div>
      <div class="stat-card" style="text-align:center;border:2px solid rgba(201,145,106,0.2)"><div style="font-size:24px;margin-bottom:6px">💸</div><div class="stat-label">Total Expenses</div><div class="stat-value" style="color:var(--peach)" id="sum-exp">R 0.00</div></div>
      <div class="stat-card" style="text-align:center" id="sum-bal-card"><div style="font-size:24px;margin-bottom:6px">💰</div><div class="stat-label">Balance</div><div class="stat-value" id="sum-bal">R 0.00</div></div>
      <div class="stat-card" style="text-align:center" id="sum-nw-card"><div style="font-size:24px;margin-bottom:6px">📊</div><div class="stat-label">Net Worth</div><div class="stat-value" id="sum-nw">R 0.00</div></div>
    </div>
    <div style="background:linear-gradient(135deg,var(--sk-primary),var(--jo-primary));border-radius:16px;padding:22px 24px;text-align:center;margin-top:16px">
      <div style="font-size:30px;margin-bottom:8px" id="sum-emoji">🏆</div>
      <div style="font-family:'Lora',serif;font-weight:700;font-size:17px;color:#fff;margin-bottom:8px" id="sum-quote"></div>
      <div style="font-size:12px;color:rgba(255,255,255,0.75)">Save each month to watch your story change 📈</div>
    </div>
  </div>

</div><!-- /content -->

<script>
// ═══════════════════════════════════════════════════════════
// FIREBASE CONFIG
// ═══════════════════════════════════════════════════════════
const FB_URL = 'https://budget-plan-849f3-default-rtdb.firebaseio.com';

async function fbGet(path) {
  try {
    const res = await fetch(`${FB_URL}/${path}.json`);
    if (!res.ok) return null;
    return await res.json();
  } catch(e) { return null; }
}

async function fbSet(path, value) {
  try {
    const res = await fetch(`${FB_URL}/${path}.json`, {
      method: 'PUT',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify(value)
    });
    return res.ok;
  } catch(e) { return false; }
}

// ═══════════════════════════════════════════════════════════
// STATE
// ═══════════════════════════════════════════════════════════
var state = {
  myName: 'Jordan',
  selectedMonth: '',
  jordan: {
    income: [
      {id:uid(),label:'Income',amount:''},
      {id:uid(),label:'Commission',amount:''}
    ],
    expenses: [
      {id:uid(),label:'Rent',amount:'',type:'recurring'},
      {id:uid(),label:'Petrol',amount:'',type:'recurring'},
      {id:uid(),label:'Savings',amount:'',type:'recurring'},
      {id:uid(),label:'Miscellaneous',amount:'',type:'once-off'},
      {id:uid(),label:'Skye',amount:'',type:'recurring'},
      {id:uid(),label:'Business Expenses',amount:'',type:'once-off'},
      {id:uid(),label:'Parking',amount:'',type:'recurring'},
    ]
  },
  skye: {
    income: [
      {id:uid(),label:'Tips',amount:''},
      {id:uid(),label:'Hourly',amount:''}
    ],
    expenses: [
      {id:uid(),label:'Rent',amount:'',type:'recurring'},
      {id:uid(),label:'Food',amount:'',type:'recurring'},
      {id:uid(),label:'Petrol',amount:'',type:'recurring'},
      {id:uid(),label:'Pep',amount:'',type:'once-off'},
      {id:uid(),label:'Breakages',amount:'',type:'once-off'},
      {id:uid(),label:'Car',amount:'',type:'recurring'},
      {id:uid(),label:'Miscellaneous',amount:'',type:'once-off'},
      {id:uid(),label:'Uni',amount:'',type:'recurring'},
      {id:uid(),label:'Savings',amount:'',type:'recurring'},
      {id:uid(),label:'Car extra',amount:'',type:'once-off'},
    ]
  },
  savings: { jordan: [], skye: [] },
  debts: [],
  assets: [],
  history: [],
  activePot: { jordan: 0, skye: 0 },
  nwTab: 'combined',
};

var charts = {};

// ═══════════════════════════════════════════════════════════
// HELPERS
// ═══════════════════════════════════════════════════════════
function uid() { return Math.random().toString(36).slice(2,8); }
function num(v) { return parseFloat(v) || 0; }
function fmt(v) { return 'R ' + num(v).toLocaleString('en-ZA',{minimumFractionDigits:2}); }
function currShort(v) { var n=num(v); return n>=1000?'R'+(n/1000).toFixed(1)+'k':'R'+n.toFixed(0); }

function getCurrentMonth() {
  var d = new Date();
  return d.getFullYear() + '-' + String(d.getMonth()+1).padStart(2,'0');
}
function monthLabel(m) {
  if (!m) return '';
  var parts = m.split('-');
  var months = ['Jan','Feb','Mar','Apr','May','Jun','Jul','Aug','Sep','Oct','Nov','Dec'];
  return months[parseInt(parts[1])-1] + ' ' + parts[0];
}

var CAT_COLORS_JO = ['#2A5F6E','#3D8A9E','#1E4A5C','#4A9ABF','#5BA3B5','#2E6E8E','#1A3D4A','#6DB8CC','#254E5C','#3A7A8E'];
var CAT_COLORS_SK = ['#B5566A','#C9916A','#D4849A','#8B3A52','#E8A0B0','#9B4060','#CF7A50','#E0B99A','#A0506A','#D4607A'];

function getMotivation(pct, remaining, dream, pot) {
  var dep = num(pot.depositAmount);
  var freq = pot.depositFreq || 'month';
  var left = dep > 0 && remaining > 0 ? Math.ceil(remaining/dep) : null;
  var fw = freq==='week'?'week':freq==='fortnight'?'fortnight':'month';
  var tl = left ? left+' more '+fw+(left!==1?'s':'') : null;
  var d = dream || 'your goal';
  if (pct<=0)  return {e:'🌱',t:'Start your first deposit — every rand counts toward '+d+'!'};
  if (pct<10)  return {e:'🌿',t:'Seed planted! '+(tl?'Just '+tl+' and '+d+' is yours!':'Keep stacking!')};
  if (pct<25)  return {e:'🔥',t:'Building momentum! '+(tl?tl+' left and '+d+' is YOURS.':'Stay consistent!')};
  if (pct<50)  return {e:'💪',t:'Quarter way there! '+(tl?'Only '+tl+' more and '+d+' becomes reality!':'Making waves!')};
  if (pct<65)  return {e:'🚀',t:'Halfway! '+(tl?tl+' left — don\'t stop now!':'Finish line in sight!')};
  if (pct<80)  return {e:'⚡',t:'More than halfway! '+(tl?tl+' — done deal.':'Almost there!')};
  if (pct<95)  return {e:'🌟',t:d+' is SO close! '+(tl?'Just '+tl+' more!':'Final stretch!')};
  if (pct<100) return {e:'🎊',t:'SO close to '+d+'!! Last few rands — this is IT!'};
  return {e:'🎉',t:'YOU DID IT! '+d+' is YOURS! 🥳 What\'s next?'};
}

// ═══════════════════════════════════════════════════════════
// INIT
// ═══════════════════════════════════════════════════════════
window.onload = function() {
  state.selectedMonth = getCurrentMonth();
  document.getElementById('monthPicker').value = state.selectedMonth;
  document.getElementById('monthPicker').addEventListener('change', function(e) {
    state.selectedMonth = e.target.value;
    updateMonthLabels();
  });
  updateMonthLabels();
  loadFromFirebase();
};

function updateMonthLabels() {
  var lbl = monthLabel(state.selectedMonth);
  var el1 = document.getElementById('jo-month-label');
  var el2 = document.getElementById('sk-month-label');
  if(el1) el1.textContent = lbl;
  if(el2) el2.textContent = lbl;
  var title = document.getElementById('sum-month-title');
  if(title) title.textContent = lbl + ' Summary';
}

// ═══════════════════════════════════════════════════════════
// FIREBASE LOAD
// ═══════════════════════════════════════════════════════════
async function loadFromFirebase() {
  var btn = document.getElementById('saveBtn');
  if(btn) btn.textContent = '⏳ Loading…';

  var data = await fbGet('budgetApp');
  if (data && typeof data === 'object') {
    if (Array.isArray(data.profiles) && data.profiles.length >= 2) {
      var sp = data.profiles[0];
      var jp = data.profiles[1];
      if (Array.isArray(sp.incomeRows) && sp.incomeRows.length) state.skye.income = sp.incomeRows;
      if (Array.isArray(sp.expRows) && sp.expRows.length) state.skye.expenses = sp.expRows;
      if (Array.isArray(jp.incomeRows) && jp.incomeRows.length) state.jordan.income = jp.incomeRows;
      if (Array.isArray(jp.expRows) && jp.expRows.length) state.jordan.expenses = jp.expRows;
    }
    if (Array.isArray(data.savings) && data.savings.length >= 2) {
      if (Array.isArray(data.savings[0].pots)) state.savings.skye = data.savings[0].pots;
      if (Array.isArray(data.savings[1].pots)) state.savings.jordan = data.savings[1].pots;
    }
    if (Array.isArray(data.debts)) state.debts = data.debts;
    if (Array.isArray(data.assets)) state.assets = data.assets;
    if (Array.isArray(data.monthHistory)) state.history = data.monthHistory;
  }

  if(btn) btn.textContent = '💾 Save All';
  renderAll();
  document.getElementById('loading-screen').style.display = 'none';
};

// ═══════════════════════════════════════════════════════════
// FIREBASE SAVE
// ═══════════════════════════════════════════════════════════
async function saveAll() {
  var btn = document.getElementById('saveBtn');
  btn.textContent = '⏳ Saving…';

  var payload = {
    profiles: [
      { name: "Skye's Budget", incomeRows: state.skye.income, expRows: state.skye.expenses, notes: '' },
      { name: "Jordan's Budget", incomeRows: state.jordan.income, expRows: state.jordan.expenses, notes: '' }
    ],
    savings: [
      { name: 'Skye', pots: state.savings.skye },
      { name: 'Jordan', pots: state.savings.jordan }
    ],
    debts: state.debts,
    assets: state.assets,
    monthHistory: state.history,
    savedAt: new Date().toISOString(),
    savedBy: state.myName
  };

  var ok = await fbSet('budgetApp', payload);
  btn.textContent = ok ? '✅ Saved!' : '❌ Try again';
  setTimeout(function(){ btn.textContent = '💾 Save All'; }, 3500);
}

// ═══════════════════════════════════════════════════════════
// WHO AM I
// ═══════════════════════════════════════════════════════════
function setMe(name) {
  state.myName = name;
  document.getElementById('btn-jordan').classList.toggle('active', name==='Jordan');
  document.getElementById('btn-skye').classList.toggle('active', name==='Skye');
}

// ═══════════════════════════════════════════════════════════
// TABS
// ═══════════════════════════════════════════════════════════
function showTab(tab) {
  document.querySelectorAll('.page').forEach(function(p){p.classList.remove('active');});
  document.querySelectorAll('.tab').forEach(function(t){t.classList.remove('active');});
  document.getElementById('page-'+tab).classList.add('active');
  document.querySelector('.tab-'+tab).classList.add('active');
  renderAll();
}

// ═══════════════════════════════════════════════════════════
// RENDER ALL
// ═══════════════════════════════════════════════════════════
function renderAll() {
  renderBudget('jordan');
  renderBudget('skye');
  renderSavings('jordan');
  renderSavings('skye');
  renderNetWorth();
  renderHistory();
  renderSummary();
  renderHousehold();
}

// ═══════════════════════════════════════════════════════════
// BUDGET RENDER
// ═══════════════════════════════════════════════════════════
function renderBudget(person) {
  var s = state[person];
  var isJo = person==='jordan';
  var prefix = isJo?'jo':'sk';
  var colors = isJo ? CAT_COLORS_JO : CAT_COLORS_SK;
  var primaryColor = isJo ? 'var(--jo-primary)' : 'var(--sk-primary)';
  var paleClass = isJo ? 'jo' : 'sk';

  var totalInc = s.income.reduce(function(a,r){return a+num(r.amount);},0);
  var totalExp = s.expenses.reduce(function(a,r){return a+num(r.amount);},0);
  var balance = totalInc - totalExp;
  var recurring = s.expenses.filter(function(r){return r.type==='recurring';}).reduce(function(a,r){return a+num(r.amount);},0);
  var once = s.expenses.filter(function(r){return r.type!=='recurring';}).reduce(function(a,r){return a+num(r.amount);},0);
  var pct = totalInc>0?Math.min(100,Math.round(totalExp/totalInc*100)):0;

  var alertEl = document.getElementById(person+'-alert');
  if (alertEl) {
    if (balance < 0) { alertEl.style.display='block'; alertEl.textContent='⚠️ Spending '+fmt(Math.abs(balance))+' more than you earn!'; }
    else alertEl.style.display='none';
  }

  var els = {
    [prefix+'-stat-inc']: fmt(totalInc),
    [prefix+'-stat-exp']: fmt(totalExp),
    [prefix+'-stat-bal']: (balance<0?'-':'')+fmt(Math.abs(balance)),
    [prefix+'-total-inc']: fmt(totalInc),
    [prefix+'-total-exp']: fmt(totalExp),
    [prefix+'-total-bal']: (balance<0?'-':'')+fmt(Math.abs(balance)),
    [prefix+'-recur']: fmt(recurring),
    [prefix+'-once']: fmt(once),
    [prefix+'-pct']: pct+'%',
  };
  Object.keys(els).forEach(function(id) {
    var el = document.getElementById(id);
    if(el) el.textContent = els[id];
  });

  var balEl = document.getElementById(prefix+'-stat-bal');
  if(balEl) balEl.style.color = balance>=0?'var(--green)':'var(--red)';
  var balTotalEl = document.getElementById(prefix+'-total-bal');
  if(balTotalEl) balTotalEl.style.color = balance>=0?'var(--ocean)':'var(--red)';
  var balRowEl = document.getElementById(prefix+'-bal-row');
  if(balRowEl) balRowEl.className = 'total-row '+(balance>=0?'total-balance-pos':'total-balance-neg');
  var pctEl = document.getElementById(prefix+'-pct');
  if(pctEl) pctEl.style.color = pct>=90?'var(--red)':primaryColor;
  var pctBar = document.getElementById(prefix+'-pct-bar');
  if(pctBar) { pctBar.style.width=pct+'%'; pctBar.style.background=pct>=90?'var(--red)':pct>=75?'var(--amber)':(isJo?'linear-gradient(90deg,var(--jo-income),var(--jo-primary))':'linear-gradient(90deg,var(--sk-income),var(--sk-primary))'); }
  var warnEl = document.getElementById(prefix+'-pct-warn');
  if(warnEl) {
    if(pct>=100){warnEl.style.display='block';warnEl.style.color='var(--red)';warnEl.textContent='🚨 Over budget!';}
    else if(pct>=90){warnEl.style.display='block';warnEl.style.color='var(--red)';warnEl.textContent='🔴 90%+ used!';}
    else if(pct>=75){warnEl.style.display='block';warnEl.style.color='var(--amber)';warnEl.textContent='🟡 75%+ used — watch it';}
    else warnEl.style.display='none';
  }

  var incContainer = document.getElementById(person+'-income-rows');
  if(incContainer) { incContainer.innerHTML=''; s.income.forEach(function(row){incContainer.appendChild(makeInputRow(row,person,'income',paleClass));}); }
  var expContainer = document.getElementById(person+'-expense-rows');
  if(expContainer) { expContainer.innerHTML=''; s.expenses.forEach(function(row){expContainer.appendChild(makeInputRow(row,person,'expense',paleClass));}); }

  var expData = s.expenses.filter(function(r){return num(r.amount)>0;});
  updateBarChart(prefix+'-bar', totalInc, totalExp, balance, isJo);
  updatePieChart(prefix+'-pie', expData, colors, prefix+'-legend');
}

function makeInputRow(row, person, type, paleClass) {
  var div = document.createElement('div');
  div.className = 'input-row';
  var labelInput = document.createElement('input');
  labelInput.className = 'input-label';
  labelInput.value = row.label || '';
  labelInput.placeholder = type==='income'?'Income source':'Expense name';
  labelInput.addEventListener('input', function(e){ row.label=e.target.value; scheduleUpdate(); });
  var amountWrap = document.createElement('div');
  amountWrap.className = 'input-amount-wrap';
  var prefix = document.createElement('span');
  prefix.className = 'input-amount-prefix '+paleClass;
  prefix.textContent = 'R';
  var amountInput = document.createElement('input');
  amountInput.type='number'; amountInput.min='0'; amountInput.value=row.amount||''; amountInput.placeholder='0.00';
  amountInput.addEventListener('input', function(e){ row.amount=e.target.value; scheduleUpdate(); });
  amountWrap.appendChild(prefix); amountWrap.appendChild(amountInput);
  div.appendChild(labelInput); div.appendChild(amountWrap);
  if (type==='expense') {
    var badge = document.createElement('button');
    badge.className='type-badge '+(row.type==='recurring'?'type-recurring':'type-once');
    badge.textContent=row.type==='recurring'?'🔁':'1×';
    badge.addEventListener('click', function(){
      row.type=row.type==='recurring'?'once-off':'recurring';
      badge.className='type-badge '+(row.type==='recurring'?'type-recurring':'type-once');
      badge.textContent=row.type==='recurring'?'🔁':'1×';
      scheduleUpdate();
    });
    div.appendChild(badge);
  }
  var del = document.createElement('button');
  del.className='btn-delete'; del.textContent='×';
  del.addEventListener('click', function(){
    if(type==='income') state[person].income=state[person].income.filter(function(r){return r.id!==row.id;});
    else state[person].expenses=state[person].expenses.filter(function(r){return r.id!==row.id;});
    renderAll();
  });
  div.appendChild(del);
  return div;
}

var updateTimer=null;
function scheduleUpdate(){ clearTimeout(updateTimer); updateTimer=setTimeout(function(){renderAll();},150); }

function addRow(person,type){
  if(type==='income') state[person].income.push({id:uid(),label:'',amount:''});
  else state[person].expenses.push({id:uid(),label:'',amount:'',type:'recurring'});
  renderAll();
}

// ═══════════════════════════════════════════════════════════
// CHARTS
// ═══════════════════════════════════════════════════════════
function destroyChart(id){ if(charts[id]){charts[id].destroy();delete charts[id];} }

function updateBarChart(id, income, expenses, balance, isJo) {
  destroyChart(id);
  var canvas=document.getElementById('chart-'+id);
  if(!canvas)return;
  charts[id]=new Chart(canvas,{type:'bar',data:{labels:['Income','Expenses','Balance'],datasets:[{data:[income,expenses,Math.abs(balance)],backgroundColor:[isJo?'#2A5F6E':'#B5566A',isJo?'#4A9ABF':'#C9916A',balance>=0?'#27AE60':'#C0392B'],borderRadius:6}]},options:{responsive:true,maintainAspectRatio:false,plugins:{legend:{display:false}},scales:{y:{ticks:{callback:function(v){return 'R'+(v/1000).toFixed(0)+'k';}},grid:{color:'#D4DDB822'}},x:{grid:{display:false}}}}});
}

function updatePieChart(id,expData,colors,legendId){
  destroyChart(id);
  var canvas=document.getElementById('chart-'+id);
  if(!canvas||!expData.length)return;
  charts[id]=new Chart(canvas,{type:'doughnut',data:{labels:expData.map(function(r){return r.label;}),datasets:[{data:expData.map(function(r){return num(r.amount);}),backgroundColor:colors.slice(0,expData.length),borderWidth:2,borderColor:'#fff'}]},options:{responsive:true,maintainAspectRatio:false,cutout:'65%',plugins:{legend:{display:false}}}});
  var legend=document.getElementById(legendId);
  if(legend){legend.innerHTML='';expData.forEach(function(r,i){var item=document.createElement('div');item.className='legend-item';item.innerHTML='<div class="legend-dot" style="background:'+colors[i%colors.length]+'"></div><span>'+r.label+'</span>';legend.appendChild(item);});}
}

// ═══════════════════════════════════════════════════════════
// HOUSEHOLD
// ═══════════════════════════════════════════════════════════
function renderHousehold(){
  var joInc=state.jordan.income.reduce(function(a,r){return a+num(r.amount);},0);
  var joExp=state.jordan.expenses.reduce(function(a,r){return a+num(r.amount);},0);
  var skInc=state.skye.income.reduce(function(a,r){return a+num(r.amount);},0);
  var skExp=state.skye.expenses.reduce(function(a,r){return a+num(r.amount);},0);
  var totalInc=joInc+skInc,totalExp=joExp+skExp,totalBal=totalInc-totalExp;
  var skSav=(state.savings.skye||[]).reduce(function(a,p){return a+num(p.saved);},0);
  var joSav=(state.savings.jordan||[]).reduce(function(a,p){return a+num(p.saved);},0);
  var totAssets=state.assets.reduce(function(a,x){return a+num(x.value);},0)+skSav+joSav;
  var totDebt=state.debts.reduce(function(a,d){return a+num(d.balance);},0);
  var nw=totAssets-totDebt;
  var skyePct=totalInc>0?Math.round(skInc/totalInc*100):50;
  var setEl=function(id,v){var el=document.getElementById(id);if(el)el.textContent=v;};
  setEl('hh-income',fmt(totalInc));setEl('hh-exp',fmt(totalExp));
  setEl('hh-bal',(totalBal<0?'-':'')+fmt(Math.abs(totalBal)));
  setEl('hh-nw',(nw<0?'-':'')+fmt(Math.abs(nw)));
  setEl('hh-split-label','Income split — Skye '+skyePct+'% / Jordan '+(100-skyePct)+'%');
  setEl('hh-skye-amt','Skye '+fmt(skInc));setEl('hh-jordan-amt','Jordan '+fmt(joInc));
  setEl('hh-sk-inc',fmt(skInc));setEl('hh-sk-exp',fmt(skExp));setEl('hh-sk-bal',(skInc-skExp<0?'-':'')+fmt(Math.abs(skInc-skExp)));
  setEl('hh-jo-inc',fmt(joInc));setEl('hh-jo-exp',fmt(joExp));setEl('hh-jo-bal',(joInc-joExp<0?'-':'')+fmt(Math.abs(joInc-joExp)));
  var bar=document.getElementById('hh-split-bar');if(bar)bar.style.width=skyePct+'%';
  destroyChart('household');
  var canvas=document.getElementById('chart-household');
  if(canvas){charts['household']=new Chart(canvas,{type:'bar',data:{labels:['Skye Inc','Jordan Inc','Skye Exp','Jordan Exp','Balance'],datasets:[{data:[skInc,joInc,skExp,joExp,Math.abs(totalBal)],backgroundColor:['#B5566A','#2A5F6E','#C9916A','#4A9ABF',totalBal>=0?'#27AE60':'#C0392B'],borderRadius:6}]},options:{responsive:true,maintainAspectRatio:false,plugins:{legend:{display:false}},scales:{y:{ticks:{callback:function(v){return 'R'+(v/1000).toFixed(0)+'k';}},grid:{color:'#D4DDB822'}},x:{grid:{display:false}}}}});}
}

// ═══════════════════════════════════════════════════════════
// SAVINGS
// ═══════════════════════════════════════════════════════════
function addPot(person){
  var prefix=person==='jordan'?'jo':'sk';
  var dream=document.getElementById(prefix+'-new-dream').value.trim();
  var goal=document.getElementById(prefix+'-new-goal').value;
  if(!dream||!goal){alert('Please enter a dream name and goal amount');return;}
  state.savings[person].push({id:uid(),potName:dream,goal:goal,saved:'0',depositAmount:'',depositFreq:'month'});
  state.activePot[person]=state.savings[person].length-1;
  document.getElementById(prefix+'-new-dream').value='';
  document.getElementById(prefix+'-new-goal').value='';
  renderSavings(person);
}

function renderSavings(person){
  var isJo=person==='jordan';
  var prefix=isJo?'jo':'sk';
  var pots=state.savings[person]||[];
  var tabsEl=document.getElementById(prefix+'-pot-tabs');
  var contentEl=document.getElementById(prefix+'-pot-content');
  if(!tabsEl||!contentEl)return;
  tabsEl.innerHTML='';
  pots.forEach(function(pot,i){
    var btn=document.createElement('button');
    btn.className='pot-tab'+(state.activePot[person]===i?' active-'+(isJo?'jo':'sk'):'');
    btn.textContent='🎯 '+(pot.potName||'Pot '+(i+1));
    btn.addEventListener('click',function(){state.activePot[person]=i;renderSavings(person);});
    tabsEl.appendChild(btn);
  });
  contentEl.innerHTML='';
  if(!pots.length){
    contentEl.innerHTML='<div class="card" style="text-align:center;padding:40px 20px;color:var(--mid)"><div style="font-size:40px;margin-bottom:12px">🎯</div><div style="font-family:\'Lora\',serif;font-size:18px;margin-bottom:8px">No savings pots yet</div><div style="font-size:13px">Type a dream name + goal above and click Add Pot</div></div>';
    return;
  }
  var pot=pots[state.activePot[person]];
  if(!pot)return;
  var saved=num(pot.saved),goal=num(pot.goal);
  var pct=goal>0?Math.min(100,Math.round(saved/goal*100)):0;
  var remaining=Math.max(0,goal-saved);
  var motiv=getMotivation(pct,remaining,pot.potName,pot);
  var heroIncome=isJo?'var(--jo-income)':'var(--sk-income)';
  var heroColor=isJo?'var(--jo-primary)':'var(--sk-primary)';
  var html='<div class="hero" style="background:linear-gradient(135deg,'+heroIncome+','+heroColor+')">';
  html+='<div style="position:relative;z-index:1">';
  html+='<div style="display:flex;justify-content:space-between;align-items:flex-start;flex-wrap:wrap;gap:8px;margin-bottom:8px">';
  html+='<div style="font-family:\'Lora\',serif;font-weight:700;font-size:26px;color:#fff">'+(pot.potName||'My Pot')+' ✨</div>';
  html+='<button onclick="removePot(\''+person+'\','+state.activePot[person]+')" style="background:rgba(255,255,255,0.15);border:1px solid rgba(255,255,255,0.3);border-radius:8px;padding:4px 10px;color:#fff;cursor:pointer;font-size:11px">🗑️ Remove</button>';
  html+='</div>';
  html+='<div style="display:flex;justify-content:space-between;font-size:12px;color:rgba(255,255,255,0.8);margin-bottom:6px"><span>'+fmt(saved)+' saved</span><span>'+pct+'% — '+fmt(remaining)+' to go</span></div>';
  html+='<div class="prog-bar-wrap"><div class="prog-bar" style="width:'+pct+'%"></div></div>';
  html+='<div class="prog-labels"><span>R0</span><span>Goal: '+fmt(goal)+'</span></div>';
  html+='<div class="hero-motiv"><span style="font-size:18px;margin-right:8px">'+motiv.e+'</span>'+motiv.t+'</div>';
  html+='</div></div>';
  html+='<div class="grid-2" style="margin-top:16px">';
  html+='<div class="card" style="border-color:'+(isJo?'var(--jo-pale)':'var(--sk-pale)')+'"><div class="card-title" style="color:'+heroColor+'">⚙️ Pot Settings</div>';
  html+='<div style="margin-bottom:12px"><div style="font-size:11px;font-weight:700;color:var(--mid);text-transform:uppercase;margin-bottom:5px">Dream name</div><input type="text" value="'+(pot.potName||'')+'" onchange="updatePot(\''+person+'\','+state.activePot[person]+',\'potName\',this.value)" style="width:100%;border:1.5px solid '+(isJo?'var(--jo-pale)':'var(--sk-pale)')+';border-radius:8px;padding:9px 12px;font-size:13px;outline:none"></div>';
  html+='<div style="margin-bottom:12px"><div style="font-size:11px;font-weight:700;color:var(--mid);text-transform:uppercase;margin-bottom:5px">Goal (R)</div><input type="number" value="'+(pot.goal||'')+'" onchange="updatePot(\''+person+'\','+state.activePot[person]+',\'goal\',this.value)" style="width:100%;border:1.5px solid '+(isJo?'var(--jo-pale)':'var(--sk-pale)')+';border-radius:8px;padding:9px 12px;font-size:13px;outline:none"></div>';
  html+='<div><div style="font-size:11px;font-weight:700;color:var(--mid);text-transform:uppercase;margin-bottom:5px">I save</div><div style="display:flex;gap:6px"><input type="number" value="'+(pot.depositAmount||'')+'" placeholder="500" onchange="updatePot(\''+person+'\','+state.activePot[person]+',\'depositAmount\',this.value)" style="flex:1;border:1.5px solid '+(isJo?'var(--jo-pale)':'var(--sk-pale)')+';border-radius:8px;padding:9px 12px;font-size:13px;outline:none"><select onchange="updatePot(\''+person+'\','+state.activePot[person]+',\'depositFreq\',this.value)" style="border:1.5px solid '+(isJo?'var(--jo-pale)':'var(--sk-pale)')+';border-radius:8px;padding:9px;font-size:12px;outline:none"><option value="week"'+(pot.depositFreq==='week'?' selected':'')+'>per week</option><option value="fortnight"'+(pot.depositFreq==='fortnight'?' selected':'')+'>per fortnight</option><option value="month"'+(!pot.depositFreq||pot.depositFreq==='month'?' selected':'')+'>per month</option></select></div></div></div>';
  html+='<div class="card" style="border-color:'+(isJo?'var(--jo-pale)':'var(--sk-pale)')+'"><div class="card-title" style="color:'+heroColor+'">💸 Update Savings</div>';
  html+='<div class="update-toggle"><button id="sav-add-btn-'+person+'" class="add-active" onclick="setSavType(\''+person+'\',\'add\')">➕ Add</button><button id="sav-take-btn-'+person+'" class="inactive" onclick="setSavType(\''+person+'\',\'take\')">➖ Take</button></div>';
  html+='<div style="margin-bottom:10px"><div style="font-size:11px;font-weight:700;color:var(--mid);text-transform:uppercase;margin-bottom:5px">Amount (R)</div><div class="amount-box"><span class="amount-prefix '+(isJo?'jo':'sk')+'">R</span><input type="number" id="sav-amt-'+person+'" min="0" placeholder="1000"></div></div>';
  html+='<div style="margin-bottom:12px"><div style="font-size:11px;font-weight:700;color:var(--mid);text-transform:uppercase;margin-bottom:5px">Note (optional)</div><input type="text" id="sav-note-'+person+'" placeholder="e.g. Birthday money..." style="width:100%;border:1.5px solid '+(isJo?'var(--jo-pale)':'var(--sk-pale)')+';border-radius:8px;padding:9px 12px;font-size:13px;outline:none"></div>';
  html+='<button onclick="doSavTransaction(\''+person+'\')" style="width:100%;padding:13px;border-radius:12px;border:none;cursor:pointer;background:linear-gradient(135deg,'+heroIncome+','+heroColor+');color:#fff;font-weight:700;font-size:14px;font-family:\'DM Sans\',sans-serif">💰 Update savings</button>';
  html+='<div class="balance-pill" style="background:'+(isJo?'var(--jo-pale)':'var(--sk-pale)')+'"><span class="bal-label" style="color:'+heroColor+'">Balance</span><span class="bal-value" style="color:'+heroColor+'">'+fmt(saved)+'</span></div></div>';
  html+='</div>';
  contentEl.innerHTML=html;
}

function setSavType(person,type){
  var addBtn=document.getElementById('sav-add-btn-'+person);
  var takeBtn=document.getElementById('sav-take-btn-'+person);
  if(!addBtn)return;
  var pageEl=document.getElementById('page-'+(person==='jordan'?'josav':'sksav'));
  if(pageEl)pageEl._savType=type;
  if(type==='add'){addBtn.className='add-active';takeBtn.className='inactive';}
  else{addBtn.className='inactive';takeBtn.className='take-active';}
}

function doSavTransaction(person){
  var amtEl=document.getElementById('sav-amt-'+person);
  if(!amtEl)return;
  var amt=num(amtEl.value);
  if(amt<=0){alert('Please enter an amount');return;}
  var pageEl=document.getElementById('page-'+(person==='jordan'?'josav':'sksav'));
  var type=pageEl&&pageEl._savType==='take'?'take':'add';
  var pot=state.savings[person][state.activePot[person]];
  if(!pot)return;
  pot.saved=String(type==='add'?num(pot.saved)+amt:Math.max(0,num(pot.saved)-amt));
  amtEl.value='';
  renderSavings(person);
}

function updatePot(person,idx,field,value){
  if(state.savings[person][idx]){state.savings[person][idx][field]=value;renderSavings(person);}
}
function removePot(person,idx){
  state.savings[person].splice(idx,1);
  state.activePot[person]=Math.max(0,state.activePot[person]-1);
  renderSavings(person);
}

// ═══════════════════════════════════════════════════════════
// NET WORTH
// ═══════════════════════════════════════════════════════════
function setNwTab(tab){
  state.nwTab=tab;
  document.getElementById('nwt-combined').className='sub-tab'+(tab==='combined'?' active-combined':'');
  document.getElementById('nwt-skye').className='sub-tab'+(tab==='skye'?' active-skye':'');
  document.getElementById('nwt-jordan').className='sub-tab'+(tab==='jordan'?' active-jordan':'');
  renderNetWorth();
}

function calcNW(owner){
  var skSav=(state.savings.skye||[]).reduce(function(a,p){return a+num(p.saved);},0);
  var joSav=(state.savings.jordan||[]).reduce(function(a,p){return a+num(p.saved);},0);
  var fa=function(o){return state.assets.filter(function(a){return a.owner===o||a.owner==='Both';}).reduce(function(a,x){return a+num(x.value);},0);};
  var fd=function(o){return state.debts.filter(function(d){return d.owner===o||d.owner==='Both';}).reduce(function(a,x){return a+num(x.balance);},0);};
  if(owner==='Skye') return{assets:fa('Skye')+skSav,debts:fd('Skye'),savings:skSav};
  if(owner==='Jordan') return{assets:fa('Jordan')+joSav,debts:fd('Jordan'),savings:joSav};
  var totSav=skSav+joSav;
  return{assets:state.assets.reduce(function(a,x){return a+num(x.value);},0)+totSav,debts:state.debts.reduce(function(a,d){return a+num(d.balance);},0),savings:totSav};
}

function renderNetWorth(){
  var skSav=(state.savings.skye||[]).reduce(function(a,p){return a+num(p.saved);},0);
  var joSav=(state.savings.jordan||[]).reduce(function(a,p){return a+num(p.saved);},0);
  var setEl=function(id,v){var el=document.getElementById(id);if(el)el.textContent=v;};
  setEl('nw-sk-sav',fmt(skSav));setEl('nw-jo-sav',fmt(joSav));
  var skDebt=state.debts.filter(function(d){return d.owner==='Skye'||d.owner==='Both';}).reduce(function(a,d){return a+num(d.balance);},0);
  var joDebt=state.debts.filter(function(d){return d.owner==='Jordan'||d.owner==='Both';}).reduce(function(a,d){return a+num(d.balance);},0);
  setEl('nw-sk-debt',fmt(skDebt));setEl('nw-jo-debt',fmt(joDebt));
  var tab=state.nwTab;
  var nwData=calcNW(tab==='skye'?'Skye':tab==='jordan'?'Jordan':'combined');
  var nw=nwData.assets-nwData.debts;
  var heroLabel=tab==='skye'?'👩 Skye\'s Net Worth':tab==='jordan'?'👨 Jordan\'s Net Worth':'🏠 Combined Net Worth';
  var heroClass=nw>=0?'hero-nw-pos':'hero-nw-neg';
  var html='<div class="hero '+heroClass+'" style="margin-bottom:16px">';
  html+='<div class="hero-label">'+heroLabel+'</div>';
  html+='<div style="font-family:\'Lora\',serif;font-weight:800;font-size:38px;color:#fff;margin-bottom:12px">'+(nw<0?'-':'')+fmt(Math.abs(nw))+'</div>';
  html+='<div class="hero-grid">';
  html+='<div class="hero-item"><div class="hero-item-label">Assets</div><div class="hero-item-value">'+fmt(nwData.assets)+'</div></div>';
  html+='<div class="hero-item"><div class="hero-item-label">Liabilities</div><div class="hero-item-value" style="color:#ffcccc">'+fmt(nwData.debts)+'</div></div>';
  html+='<div class="hero-item"><div class="hero-item-label">In Savings</div><div class="hero-item-value" style="color:rgba(255,255,255,0.85)">'+fmt(nwData.savings)+'</div></div>';
  if(tab==='combined'){
    var skN=calcNW('Skye'),joN=calcNW('Jordan');
    var skNW=skN.assets-skN.debts,joNW=joN.assets-joN.debts;
    html+='</div><div style="display:flex;gap:12px;flex-wrap:wrap;margin-top:10px">';
    html+='<div style="background:rgba(255,255,255,0.12);border-radius:10px;padding:10px 16px"><div style="font-size:10px;color:rgba(255,255,255,0.65)">👩 Skye</div><div style="font-family:\'Lora\',serif;font-weight:700;font-size:16px;color:'+(skNW>=0?'#fff':'#ffaaaa')+'">'+(skNW<0?'-':'')+fmt(Math.abs(skNW))+'</div></div>';
    html+='<div style="background:rgba(255,255,255,0.12);border-radius:10px;padding:10px 16px"><div style="font-size:10px;color:rgba(255,255,255,0.65)">👨 Jordan</div><div style="font-family:\'Lora\',serif;font-weight:700;font-size:16px;color:'+(joNW>=0?'#fff':'#ffaaaa')+'">'+(joNW<0?'-':'')+fmt(Math.abs(joNW))+'</div></div>';
  }
  html+='</div></div>';
  document.getElementById('nw-hero').innerHTML=html;
  var assetsEl=document.getElementById('assets-rows');
  if(assetsEl){assetsEl.innerHTML='';state.assets.forEach(function(a,i){assetsEl.appendChild(makeAssetRow(a,i,'asset'));});}
  var debtsEl=document.getElementById('debts-rows');
  if(debtsEl){debtsEl.innerHTML='';state.debts.forEach(function(d,i){debtsEl.appendChild(makeAssetRow(d,i,'debt'));});}
}

function makeAssetRow(item,idx,type){
  var div=document.createElement('div');div.className='asset-row';
  var fields=document.createElement('div');fields.className='asset-row-fields';
  var makeField=function(labelText,inputType,value,onchangeFn,style){
    var f=document.createElement('div');f.className='asset-field grow';if(style)f.style.cssText=style;
    var lbl=document.createElement('label');lbl.textContent=labelText;
    var inp;
    if(inputType==='select'){inp=document.createElement('select');['Skye','Jordan','Both'].forEach(function(opt){var o=document.createElement('option');o.value=opt;o.textContent=opt;if(value===opt)o.selected=true;inp.appendChild(o);});}
    else{inp=document.createElement('input');inp.type=inputType;inp.value=value||'';inp.placeholder=labelText;}
    inp.addEventListener('change',function(e){onchangeFn(e.target.value);});
    f.appendChild(lbl);f.appendChild(inp);return f;
  };
  if(type==='asset'){
    fields.appendChild(makeField('Asset','text',item.label,function(v){item.label=v;renderNetWorth();},'flex:2;min-width:100px'));
    fields.appendChild(makeField('Value R','number',item.value,function(v){item.value=v;renderNetWorth();},'flex:1;min-width:70px'));
    fields.appendChild(makeField('Owner','select',item.owner,function(v){item.owner=v;renderNetWorth();},'width:80px;flex:none'));
  }else{
    fields.appendChild(makeField('Debt','text',item.label,function(v){item.label=v;renderNetWorth();},'flex:2;min-width:100px'));
    fields.appendChild(makeField('Balance','number',item.balance,function(v){item.balance=v;renderNetWorth();},'flex:1;min-width:70px'));
    fields.appendChild(makeField('Rate %','number',item.rate,function(v){item.rate=v;renderNetWorth();},'width:55px;flex:none'));
    fields.appendChild(makeField('Min Pay','number',item.minPayment,function(v){item.minPayment=v;renderNetWorth();},'width:65px;flex:none'));
    fields.appendChild(makeField('Owner','select',item.owner,function(v){item.owner=v;renderNetWorth();},'width:80px;flex:none'));
    if(num(item.balance)>0&&num(item.minPayment)>0){var est=document.createElement('div');est.style.cssText='font-size:11px;color:var(--peach);margin-top:6px;width:100%';est.textContent='⏱ ~'+Math.ceil(num(item.balance)/num(item.minPayment))+' months at min payment'+(num(item.rate)>0?' ('+item.rate+'% p.a.)':'');div.appendChild(fields);div.appendChild(est);var del2=makeDelBtn(function(){state.debts.splice(idx,1);renderNetWorth();});fields.appendChild(del2);return div;}
  }
  var del=makeDelBtn(type==='asset'?function(){state.assets.splice(idx,1);renderNetWorth();}:function(){state.debts.splice(idx,1);renderNetWorth();});
  fields.appendChild(del);div.appendChild(fields);return div;
}

function makeDelBtn(fn){var b=document.createElement('button');b.className='btn-delete';b.textContent='×';b.style.marginTop='18px';b.addEventListener('click',fn);return b;}
function addAsset(){state.assets.push({id:uid(),owner:'Both',label:'',value:''});renderNetWorth();}
function addDebt(){state.debts.push({id:uid(),owner:'Both',label:'',balance:'',rate:'',minPayment:''});renderNetWorth();}

// ═══════════════════════════════════════════════════════════
// HISTORY
// ═══════════════════════════════════════════════════════════
function saveMonthSnapshot(person){
  var profile=person==='Jordan'?state.jordan:state.skye;
  var inc=profile.income.reduce(function(a,r){return a+num(r.amount);},0);
  var exp=profile.expenses.reduce(function(a,r){return a+num(r.amount);},0);
  state.history=state.history.filter(function(h){return!(h.month===state.selectedMonth&&h.person===person);});
  state.history.push({month:state.selectedMonth,person:person,income:inc,expenses:exp,balance:inc-exp});
  state.history.sort(function(a,b){return a.month.localeCompare(b.month);});
  renderHistory();
  alert('✅ '+person+'\'s '+monthLabel(state.selectedMonth)+' saved!');
}

function renderHistory(){
  var hist=state.history;
  if(!hist.length){
    var emptyEl=document.getElementById('hist-empty');var tableEl=document.getElementById('hist-table');var chartCard=document.getElementById('hist-chart-card');
    if(emptyEl)emptyEl.style.display='block';if(tableEl)tableEl.style.display='none';if(chartCard)chartCard.style.display='none';return;
  }
  var emptyEl=document.getElementById('hist-empty');var tableEl=document.getElementById('hist-table');
  if(emptyEl)emptyEl.style.display='none';if(tableEl)tableEl.style.display='table';
  var months={};
  hist.forEach(function(h){if(!months[h.month])months[h.month]={month:h.month,skye:{income:0,expenses:0},jordan:{income:0,expenses:0}};var key=h.person==='Skye'?'skye':'jordan';months[h.month][key].income=h.income;months[h.month][key].expenses=h.expenses;});
  var sortedMonths=Object.values(months).sort(function(a,b){return b.month.localeCompare(a.month);});
  var tbody=document.getElementById('hist-tbody');
  if(tbody){tbody.innerHTML='';sortedMonths.forEach(function(m,i){var bal=(m.skye.income-m.skye.expenses)+(m.jordan.income-m.jordan.expenses);var tr=document.createElement('tr');tr.style.background=i%2===0?'#fff':'#fafaf7';tr.innerHTML='<td style="font-weight:700;color:var(--dark)">'+monthLabel(m.month)+'</td><td style="color:var(--sk-primary)">'+fmt(m.skye.income)+'</td><td style="color:var(--peach)">'+fmt(m.skye.expenses)+'</td><td style="color:var(--jo-primary)">'+fmt(m.jordan.income)+'</td><td style="color:var(--peach)">'+fmt(m.jordan.expenses)+'</td><td style="font-weight:700;color:'+(bal>=0?'var(--green)':'var(--red)')+'">'+( bal>=0?'':'-')+fmt(Math.abs(bal))+'</td>';tbody.appendChild(tr);});}
}

// ═══════════════════════════════════════════════════════════
// SUMMARY
// ═══════════════════════════════════════════════════════════
function renderSummary(){
  var joInc=state.jordan.income.reduce(function(a,r){return a+num(r.amount);},0);
  var joExp=state.jordan.expenses.reduce(function(a,r){return a+num(r.amount);},0);
  var skInc=state.skye.income.reduce(function(a,r){return a+num(r.amount);},0);
  var skExp=state.skye.expenses.reduce(function(a,r){return a+num(r.amount);},0);
  var totalInc=joInc+skInc,totalExp=joExp+skExp,totalBal=totalInc-totalExp;
  var totSav=(state.savings.skye||[]).concat(state.savings.jordan||[]).reduce(function(a,p){return a+num(p.saved);},0);
  var totDebt=state.debts.reduce(function(a,d){return a+num(d.balance);},0);
  var nw=state.assets.reduce(function(a,x){return a+num(x.value);},0)+totSav-totDebt;
  var grade=totalBal>=0&&totSav>0?'A':totalBal>=0?'B':totalBal>-1000?'C':'D';
  var gradeColors={A:'#27AE60',B:'#6B7C45',C:'#E67E22',D:'#C0392B'};
  var gradeMsgs={A:'🌟 Incredible! Saving AND in the black. Keep it up!',B:'💪 Solid month! Cover costs — now grow those savings.',C:'⚠️ Tight month. Small cuts now = big wins later.',D:'🚨 Spending more than you earn. Review one category.'};
  var quotes={A:'Building wealth — one month at a time.',B:'Consistency is the secret. On the right track.',C:'Every great story had a turning point. This could be yours.',D:'Awareness is step one. The comeback starts now.'};
  var emojis={A:'🏆',B:'💪',C:'🌱',D:'🔄'};
  var gc=gradeColors[grade];
  var setEl=function(id,v){var el=document.getElementById(id);if(el)el.textContent=v;};
  setEl('sum-grade',grade);setEl('sum-msg',gradeMsgs[grade]);
  setEl('sum-income',fmt(totalInc));setEl('sum-exp',fmt(totalExp));
  setEl('sum-bal',(totalBal<0?'-':'')+fmt(Math.abs(totalBal)));
  setEl('sum-nw',(nw<0?'-':'')+fmt(Math.abs(nw)));
  setEl('sum-emoji',emojis[grade]);setEl('sum-quote',quotes[grade]);
  var gradeEl=document.getElementById('sum-grade');if(gradeEl)gradeEl.style.color=gc;
  var gradeBox=document.getElementById('sum-grade-box');if(gradeBox){gradeBox.style.border='2px solid '+gc;gradeBox.style.background=gc+'22';}
  var balEl=document.getElementById('sum-bal');if(balEl)balEl.style.color=totalBal>=0?'var(--green)':'var(--red)';
  var nwEl=document.getElementById('sum-nw');if(nwEl)nwEl.style.color=nw>=0?'var(--ocean)':'var(--red)';
}

// ═══════════════════════════════════════════════════════════
// CSV
// ═══════════════════════════════════════════════════════════
function downloadCSV(){
  var joInc=state.jordan.income.reduce(function(a,r){return a+num(r.amount);},0);
  var joExp=state.jordan.expenses.reduce(function(a,r){return a+num(r.amount);},0);
  var skInc=state.skye.income.reduce(function(a,r){return a+num(r.amount);},0);
  var skExp=state.skye.expenses.reduce(function(a,r){return a+num(r.amount);},0);
  var rows=[['Skye & Jordan Budget',monthLabel(state.selectedMonth)],[''],['JORDAN'],['Income',joInc],['Expenses',joExp],['Balance',joInc-joExp],[''],['SKYE'],['Income',skInc],['Expenses',skExp],['Balance',skInc-skExp],[''],['COMBINED'],['Income',joInc+skInc],['Expenses',joExp+skExp],['Balance',(joInc-joExp)+(skInc-skExp)]];
  var csv=rows.map(function(r){return r.join(',');}).join('\n');
  var a=document.createElement('a');a.href=URL.createObjectURL(new Blob([csv],{type:'text/csv'}));a.download='Budget_'+state.selectedMonth+'.csv';a.click();URL.revokeObjectURL(a.href);
}

</script>
</body>
</html>
