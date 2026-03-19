[index.html](https://github.com/user-attachments/files/26119518/index.html)
<!DOCTYPE html>
<html lang="zh-TW">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>食品成本計算系統</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans+TC:wght@300;400;500;700;900&family=DM+Mono:wght@400;500&display=swap');
*{box-sizing:border-box;margin:0;padding:0}
:root{
  --bg:#f4f1ea;
  --surface:#fff;
  --s2:#faf8f3;
  --s3:#f2ede2;
  --border:#ddd5c0;
  --border2:#c8bfa8;
  --ink:#1a1814;
  --ink2:#3a3530;
  --ink3:#7a7060;
  --ink4:#b0a898;
  --gold:#8a6500;
  --gold2:#b88a00;
  --gold-bg:#fdf8e8;
  --gold-bd:#e8d080;
  --red:#a82020;
  --green:#1a5c30;
  --blue:#183060;
  --r:3px;
  --sh:0 1px 4px rgba(0,0,0,.08),0 4px 16px rgba(0,0,0,.05);
}
body{background:var(--bg);color:var(--ink);font-family:'Noto Sans TC',sans-serif;font-size:13px;min-height:100vh}

/* ─── TOPBAR ─── */
header{
  background:linear-gradient(135deg,#1e1708 0%,#3a2e10 60%,#1e1708 100%);
  border-bottom:2px solid var(--gold2);
  display:flex;align-items:center;height:50px;padding:0 0 0 18px;
  position:sticky;top:0;z-index:400;
  box-shadow:0 2px 16px rgba(0,0,0,.4);
}
.logo{color:#f0e0a0;font-weight:900;font-size:15px;letter-spacing:.05em;
  padding-right:18px;border-right:1px solid rgba(255,255,255,.12);display:flex;align-items:center;gap:8px}
.logo-icon{font-size:18px}
.nav{display:flex;height:100%}
.nav-btn{background:none;border:none;border-bottom:3px solid transparent;
  color:rgba(240,224,160,.5);cursor:pointer;font-family:inherit;font-size:12px;
  font-weight:600;height:100%;padding:0 16px;letter-spacing:.04em;transition:all .15s;white-space:nowrap}
.nav-btn:hover{color:rgba(240,224,160,.85);background:rgba(255,255,255,.04)}
.nav-btn.on{color:#f0e0a0;border-bottom-color:var(--gold2)}
.hdr-right{margin-left:auto;display:flex;align-items:center;gap:8px;padding:0 16px}
.hdr-save{font-size:10px;color:rgba(240,224,160,.35);font-family:'DM Mono',monospace;letter-spacing:.04em}
.hdr-save.ok{color:#80c880}

/* ─── LAYOUT ─── */
.wrap{display:grid;grid-template-columns:240px 1fr;height:calc(100vh - 50px)}

/* ─── SIDEBAR ─── */
.sidebar{background:var(--surface);border-right:1px solid var(--border);display:flex;flex-direction:column;overflow:hidden}
.sb-hd{padding:12px 12px 10px;background:linear-gradient(160deg,var(--gold-bg),var(--surface));border-bottom:1px solid var(--gold-bd)}
.sb-hd-lbl{font-size:9px;font-weight:700;letter-spacing:.12em;text-transform:uppercase;color:var(--ink3);margin-bottom:7px}
.sb-search{width:100%;background:var(--bg);border:1px solid var(--border2);border-radius:var(--r);
  color:var(--ink);font-family:inherit;font-size:12px;padding:5px 9px;outline:none;transition:border-color .15s}
.sb-search:focus{border-color:var(--gold)}
.sb-body{flex:1;overflow-y:auto;padding:7px}
.prod-card{border:1px solid var(--border);border-radius:var(--r);cursor:pointer;
  margin-bottom:5px;padding:8px 10px;background:var(--surface);transition:all .15s}
.prod-card:hover{border-color:var(--gold-bd);background:var(--gold-bg)}
.prod-card.on{border-color:var(--gold);background:var(--gold-bg);box-shadow:0 0 0 2px rgba(138,101,0,.1)}
.pc-name{font-weight:700;font-size:12px}
.pc-spec{font-size:10px;color:var(--ink3);margin-top:1px}
.pc-cost{font-family:'DM Mono',monospace;font-size:11px;color:var(--gold);margin-top:3px}
.sb-ft{padding:9px;border-top:1px solid var(--border)}
.btn-add-prod{width:100%;background:var(--gold);border:none;border-radius:var(--r);
  color:#fff;cursor:pointer;font-family:inherit;font-size:12px;font-weight:700;
  padding:8px;letter-spacing:.04em;transition:background .15s}
.btn-add-prod:hover{background:var(--gold2)}

/* ─── MAIN SCROLL ─── */
.main-area{overflow-y:auto;background:var(--bg)}
.page{display:none}
.page.on{display:block}
.inner{padding:22px 26px;max-width:1200px}

/* ─── SECTION HEADER ─── */
.sec{font-size:9px;font-weight:700;letter-spacing:.12em;text-transform:uppercase;
  color:var(--ink3);display:flex;align-items:center;gap:8px;margin:0 0 10px}
.sec::after{content:'';flex:1;height:1px;background:var(--border)}

/* ─── PRODUCT HEADER ─── */
.prod-hd{background:linear-gradient(135deg,#fdf8e8,#fffef8);border:1px solid var(--gold-bd);
  border-radius:5px;padding:16px 18px;margin-bottom:18px;box-shadow:var(--sh)}
.prod-hd-top{display:flex;align-items:center;gap:12px;margin-bottom:12px;flex-wrap:wrap}
.pname-field{display:flex;flex-direction:column;gap:4px;flex:1;min-width:200px}
.pname-label{font-size:9px;font-weight:700;letter-spacing:.1em;text-transform:uppercase;color:var(--ink3)}
.pname-input{background:var(--surface);border:1px solid var(--border2);border-radius:var(--r);
  color:var(--ink);font-family:inherit;font-size:16px;font-weight:700;padding:7px 10px;outline:none;
  transition:border-color .15s}
.pname-input:focus{border-color:var(--gold)}
.prod-hd-row{display:flex;gap:10px;flex-wrap:wrap}
.fld{display:flex;flex-direction:column;gap:3px}
.fld label{font-size:9px;font-weight:700;letter-spacing:.08em;text-transform:uppercase;color:var(--ink3)}
.fld input,.fld select{background:var(--surface);border:1px solid var(--border2);border-radius:var(--r);
  color:var(--ink);font-family:inherit;font-size:12px;padding:5px 8px;outline:none;transition:border-color .15s}
.fld input:focus,.fld select:focus{border-color:var(--gold)}

/* ─── COST SUMMARY ─── */
.cost-bar{display:grid;grid-template-columns:repeat(5,1fr);gap:9px;margin-bottom:18px}
.cb{background:var(--surface);border:1px solid var(--border);border-radius:var(--r);
  padding:11px 12px;position:relative;overflow:hidden;box-shadow:var(--sh)}
.cb::before{content:'';position:absolute;top:0;left:0;right:0;height:3px}
.cb.ing::before{background:#8a4010}.cb.pkg::before{background:#183060}
.cb.lab::before{background:#1a5c30}.cb.fee::before{background:#5a2a7a}
.cb.tot::before{background:linear-gradient(90deg,var(--gold),var(--gold2))}
.cb-lbl{font-size:9px;font-weight:700;letter-spacing:.1em;text-transform:uppercase;color:var(--ink3);margin-bottom:5px}
.cb-val{font-family:'DM Mono',monospace;font-size:17px;font-weight:500}
.cb.tot .cb-val{font-size:20px;color:var(--gold)}
.cb-pct{font-size:10px;color:var(--ink3);margin-top:3px}
.ratio-bar{height:3px;background:#e8e0d0;border-radius:2px;margin-top:7px;display:flex;overflow:hidden;gap:1px}
.rb{height:100%;transition:width .3s ease}

/* ─── TABLE CARD ─── */
.tcard{background:var(--surface);border:1px solid var(--border);border-radius:var(--r);
  overflow:hidden;margin-bottom:16px;box-shadow:var(--sh)}
.tcard-hd{background:linear-gradient(135deg,var(--s2),var(--surface));border-bottom:1px solid var(--border);
  padding:9px 14px;display:flex;align-items:center;justify-content:space-between}
.tcard-title{font-size:11px;font-weight:700;letter-spacing:.06em;color:var(--ink2)}
.tcard-sub{font-size:10px;color:var(--ink3)}

/* ─── THE MAIN TABLE ─── */
.T{width:100%;border-collapse:collapse;font-size:12px}
.T th{background:var(--s2);color:var(--ink3);font-size:9px;font-weight:700;
  letter-spacing:.08em;text-transform:uppercase;padding:7px 8px;text-align:left;
  border-bottom:1px solid var(--border);white-space:nowrap;position:sticky;top:0;z-index:1}
.T td{padding:0;border-bottom:1px solid var(--s3);vertical-align:middle}
.T tr:last-child td{border-bottom:none}
.T tr:hover td{background:var(--gold-bg)}
/* cell inner */
.ci{padding:6px 8px;display:block}
.mono{font-family:'DM Mono',monospace}
.tr{text-align:right}
.muted{color:var(--ink3)}
.bold{font-weight:600}
/* inline cell input */
.ci-inp{
  background:transparent;border:none;color:var(--ink);font-family:inherit;font-size:12px;
  padding:6px 8px;outline:none;width:100%;display:block;
}
.ci-inp:focus{background:var(--gold-bg);outline:2px solid var(--gold);outline-offset:-1px;border-radius:2px}
.ci-inp.mono{font-family:'DM Mono',monospace}
.ci-inp.tr{text-align:right}
.ci-inp::placeholder{color:var(--ink4)}
/* the cost cell */
.cost-cell{font-family:'DM Mono',monospace;font-weight:600;padding:6px 8px;display:block;text-align:right}

/* ─── AUTOCOMPLETE ─── */
.ac-wrap{position:relative;display:block}
.ac-dd{position:absolute;top:100%;left:0;right:0;z-index:300;
  background:var(--surface);border:1px solid var(--gold-bd);border-top:none;
  border-radius:0 0 var(--r) var(--r);box-shadow:0 8px 24px rgba(0,0,0,.18);
  max-height:240px;overflow-y:auto;display:none}
.ac-dd.open{display:block}
.ac-row{padding:7px 10px;cursor:pointer;border-bottom:1px solid var(--border);transition:background .1s}
.ac-row:last-child{border-bottom:none}
.ac-row:hover,.ac-row.hi{background:var(--gold-bg)}
.ac-row-name{font-weight:600;font-size:12px}
.ac-row-meta{font-size:10px;color:var(--ink3);font-family:'DM Mono',monospace;margin-top:1px}
.ac-create{padding:7px 10px;cursor:pointer;color:var(--gold);font-size:11px;font-weight:700;
  border-top:1px solid var(--border);display:flex;align-items:center;gap:5px}
.ac-create:hover{background:var(--gold-bg)}

/* ─── ADD ROW ─── */
.add-trigger-row td{background:var(--s2)!important}
.add-trigger-row:hover td{background:var(--gold-bg)!important}
.add-trigger-btn{width:100%;background:none;border:none;color:var(--ink3);cursor:pointer;
  font-family:inherit;font-size:11px;font-weight:600;padding:7px 14px;text-align:left;
  letter-spacing:.04em;transition:color .15s}
.add-trigger-btn:hover{color:var(--gold)}

/* ─── SUBTOTAL ROW ─── */
.sub-row td{background:var(--s2)!important;border-top:1px solid var(--border)}
.sub-row:hover td{background:var(--gold-bg)!important}

/* ─── PRICING TABLE ─── */
.price-tbl{width:100%;border-collapse:collapse;font-size:12px}
.price-tbl th{background:var(--s2);color:var(--ink3);font-size:9px;font-weight:700;
  letter-spacing:.08em;text-transform:uppercase;padding:7px 10px;border-bottom:1px solid var(--border)}
.price-tbl td{padding:0;border-bottom:1px solid var(--s3)}
.price-tbl tr:hover td{background:var(--gold-bg)}
.price-tbl tr:last-child td{border-bottom:none}
.profit-pos{color:var(--green);font-weight:600}
.profit-neg{color:var(--red);font-weight:600}

/* ─── LIBRARY PAGES ─── */
.lib-hd{display:flex;align-items:center;justify-content:space-between;flex-wrap:wrap;gap:10px;margin-bottom:16px}
.lib-title{font-size:18px;font-weight:900}
.lib-sub{font-size:11px;color:var(--ink3);margin-top:2px}
.lib-actions{display:flex;gap:8px;flex-wrap:wrap}
.search-inp{background:var(--surface);border:1px solid var(--border2);border-radius:var(--r);
  color:var(--ink);font-family:inherit;font-size:12px;padding:7px 10px;outline:none;
  transition:border-color .15s;min-width:220px}
.search-inp:focus{border-color:var(--gold)}
.lib-count{font-size:11px;color:var(--ink3);margin-top:-8px;margin-bottom:12px}

/* ─── BUTTONS ─── */
.btn{border:none;border-radius:var(--r);cursor:pointer;font-family:inherit;font-size:11px;
  font-weight:700;letter-spacing:.04em;padding:6px 13px;transition:all .15s}
.btn:hover{opacity:.82}.btn:active{transform:scale(.97)}
.btn-gold{background:var(--gold);color:#fff}
.btn-blue{background:var(--blue);color:#fff}
.btn-red{background:var(--red);color:#fff}
.btn-ghost{background:transparent;border:1px solid var(--border2);color:var(--ink3)}
.btn-ghost:hover{border-color:var(--ink);color:var(--ink);opacity:1}
.btn-ink{background:var(--ink);color:#f0e0a0}
.btn-sm{padding:4px 9px;font-size:10px}
.btn-del{background:none;border:none;color:var(--ink4);cursor:pointer;font-size:13px;
  padding:4px 7px;border-radius:2px;line-height:1;transition:all .12s}
.btn-del:hover{background:#fee8e8;color:var(--red)}

/* ─── MODAL ─── */
.modal-bg{position:fixed;inset:0;background:rgba(0,0,0,.55);z-index:600;
  display:none;align-items:center;justify-content:center}
.modal-bg.open{display:flex}
.modal{background:var(--surface);border-radius:5px;width:560px;max-width:96vw;
  box-shadow:0 24px 64px rgba(0,0,0,.35);border-top:3px solid var(--gold2)}
.modal-hd{padding:16px 18px 12px;border-bottom:1px solid var(--border);
  display:flex;justify-content:space-between;align-items:center}
.modal-title{font-weight:700;font-size:14px}
.modal-x{background:none;border:none;color:var(--ink3);cursor:pointer;font-size:18px;padding:2px 6px;border-radius:3px}
.modal-x:hover{background:var(--s2)}
.modal-body{padding:16px 18px;display:flex;flex-direction:column;gap:10px}
.modal-ft{padding:12px 18px;border-top:1px solid var(--border);display:flex;justify-content:flex-end;gap:8px}
.frow{display:grid;gap:9px}
.frow.c2{grid-template-columns:1fr 1fr}
.frow.c3{grid-template-columns:1fr 1fr 1fr}
.frow.c4{grid-template-columns:1fr 1fr 1fr 1fr}
.frow.c1{grid-template-columns:1fr}
.fi{display:flex;flex-direction:column;gap:3px}
.fi label{font-size:9px;font-weight:700;letter-spacing:.08em;text-transform:uppercase;color:var(--ink3)}
.fi input,.fi select{background:var(--bg);border:1px solid var(--border2);border-radius:var(--r);
  color:var(--ink);font-family:inherit;font-size:13px;padding:6px 9px;outline:none;
  transition:border-color .15s;width:100%}
.fi input:focus,.fi select:focus{border-color:var(--gold)}
.fi input::placeholder{color:var(--ink4)}
.calc-hint{font-size:11px;color:var(--gold);font-family:'DM Mono',monospace;min-height:15px}

/* scrollbar */
::-webkit-scrollbar{width:5px;height:5px}
::-webkit-scrollbar-track{background:transparent}
::-webkit-scrollbar-thumb{background:#d8d0c0;border-radius:3px}

/* empty */
.empty-state{display:flex;align-items:center;justify-content:center;height:65vh;flex-direction:column;gap:10px;color:var(--ink3)}
.empty-icon{font-size:48px;opacity:.35}

/* overflow-x scroll for wide tables */
.tbl-scroll{overflow-x:auto}

@media print{header,.sidebar,.btn,.btn-del,.modal-bg{display:none!important}
  .wrap{display:block}.main-area{overflow:visible}.page.on{display:block!important;padding:8px}}

/* ─── DB MANAGEMENT PAGE ─── */
.db-page{padding:22px 26px;max-width:1400px}
.db-toolbar{display:flex;align-items:center;gap:8px;flex-wrap:wrap;margin-bottom:14px}
.db-toolbar .search-inp{flex:1;min-width:180px;max-width:280px}
.db-tab-row{display:flex;gap:0;border-bottom:2px solid var(--border);margin-bottom:16px}
.db-tab{background:none;border:none;border-bottom:3px solid transparent;color:var(--ink3);
  cursor:pointer;font-family:inherit;font-size:12px;font-weight:700;padding:9px 18px;
  letter-spacing:.04em;transition:all .15s;margin-bottom:-2px;white-space:nowrap}
.db-tab:hover{color:var(--ink);background:var(--gold-bg)}
.db-tab.on{color:var(--gold);border-bottom-color:var(--gold)}
.db-stats{display:grid;grid-template-columns:repeat(4,1fr);gap:10px;margin-bottom:18px}
.stat-card{background:var(--surface);border:1px solid var(--border);border-radius:var(--r);
  padding:12px 14px;box-shadow:var(--sh)}
.stat-num{font-family:'DM Mono',monospace;font-size:22px;font-weight:700;color:var(--gold)}
.stat-lbl{font-size:10px;color:var(--ink3);margin-top:3px;font-weight:600;letter-spacing:.04em}

/* ─── PASTE IMPORT MODAL ─── */
.paste-modal .modal{width:780px;max-width:97vw}
.paste-area{width:100%;min-height:180px;background:var(--bg);border:2px dashed var(--border2);
  border-radius:var(--r);color:var(--ink);font-family:'DM Mono',monospace;font-size:12px;
  padding:12px;outline:none;resize:vertical;transition:border-color .15s;line-height:1.6}
.paste-area:focus{border-color:var(--gold);border-style:solid}
.paste-area::placeholder{color:var(--ink4);font-family:'Noto Sans TC',sans-serif;font-size:12px}
.preview-table{width:100%;border-collapse:collapse;font-size:11px;max-height:280px;overflow-y:auto;display:block}
.preview-table th{background:var(--ink);color:#f0e0a0;padding:5px 8px;text-align:left;
  font-size:9px;font-weight:700;letter-spacing:.06em;white-space:nowrap;position:sticky;top:0}
.preview-table td{padding:4px 8px;border-bottom:1px solid var(--s3);white-space:nowrap}
.preview-table tr:nth-child(even) td{background:var(--s2)}
.preview-table tr.err td{background:#fff0f0;color:var(--red)}
.preview-table tr.ok td{background:#f0fff4}
.col-map{display:grid;grid-template-columns:repeat(auto-fill,minmax(160px,1fr));gap:8px;margin-bottom:10px}
.col-map-item{display:flex;flex-direction:column;gap:3px}
.col-map-item label{font-size:9px;font-weight:700;letter-spacing:.06em;color:var(--ink3);text-transform:uppercase}
.col-map-item select{background:var(--bg);border:1px solid var(--border2);border-radius:var(--r);
  color:var(--ink);font-family:inherit;font-size:11px;padding:4px 6px;outline:none}
.col-map-item select:focus{border-color:var(--gold)}
.import-result{padding:10px 12px;border-radius:var(--r);font-size:12px;font-weight:600;margin-top:4px}
.import-result.ok{background:#e8f8ec;color:var(--green);border:1px solid #b8e8c8}
.import-result.warn{background:#fff8e0;color:#7a5a00;border:1px solid var(--gold-bd)}
.import-result.err{background:#fee;color:var(--red);border:1px solid #f0c0c0}
.step-badge{display:inline-flex;align-items:center;justify-content:center;width:20px;height:20px;
  border-radius:50%;background:var(--gold);color:#fff;font-size:10px;font-weight:700;margin-right:6px;flex-shrink:0}
.step-row{display:flex;align-items:flex-start;gap:8px;margin-bottom:12px}
.step-body{flex:1}

/* ─── NL IMPORT ─── */
.nl-modal .modal{width:760px;max-width:97vw}
.nl-textarea{
  width:100%;min-height:160px;background:var(--bg);
  border:2px solid var(--border2);border-radius:var(--r);
  color:var(--ink);font-family:'Noto Sans TC',sans-serif;font-size:14px;
  line-height:1.8;padding:12px 14px;outline:none;resize:vertical;
  transition:border-color .15s;
}
.nl-textarea:focus{border-color:var(--gold);border-style:solid}
.nl-textarea::placeholder{color:var(--ink4);font-size:13px}
.nl-result-row{
  display:flex;align-items:center;gap:8px;padding:8px 10px;
  border-bottom:1px solid var(--s3);transition:background .1s;
}
.nl-result-row:last-child{border-bottom:none}
.nl-result-row:hover{background:var(--gold-bg)}
.nl-badge{
  font-size:10px;font-weight:700;padding:2px 8px;border-radius:10px;
  white-space:nowrap;flex-shrink:0;
}
.nl-badge.match{background:#e8f8ec;color:var(--green)}
.nl-badge.fuzzy{background:#fff8e0;color:#7a5a00}
.nl-badge.new{background:#e8eeff;color:var(--blue)}
.nl-badge.skip{background:#f0f0f0;color:var(--ink3)}
.nl-name{font-weight:600;font-size:13px;flex:1}
.nl-qty{font-family:'DM Mono',monospace;font-size:12px;color:var(--ink2);white-space:nowrap}
.nl-match-name{font-size:11px;color:var(--ink3);white-space:nowrap}
.nl-cost{font-family:'DM Mono',monospace;font-size:12px;color:var(--gold);white-space:nowrap;min-width:80px;text-align:right}
.nl-thinking{display:flex;align-items:center;gap:10px;padding:20px;color:var(--ink3);font-size:13px}
.nl-spinner{width:20px;height:20px;border:2px solid var(--border);border-top-color:var(--gold);border-radius:50%;animation:spin .8s linear infinite}
@keyframes spin{to{transform:rotate(360deg)}}
</style>
<script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>
</head>
<body>
<header>
  <div class="logo"><span class="logo-icon">🏷️</span>食品成本計算系統</div>
  <nav class="nav">
    <button class="nav-btn on"  onclick="showPage('pg-prod',this)">📋 產品成本</button>
    <button class="nav-btn"     onclick="showPage('pg-raw',this)">🌾 原料資料庫</button>
    <button class="nav-btn"     onclick="showPage('pg-pkg',this)">📦 物料包材庫</button>
    <button class="nav-btn"     onclick="showPage('pg-lab',this)">👷 人工費率</button>
    <button class="nav-btn"     onclick="showPage('pg-db',this)">🗄️ 資料庫管理</button>
  </nav>
  <div class="hdr-right">
    <span class="hdr-save ok" id="save-status">● 已儲存</span>
    <button class="btn btn-sm" style="background:#1a6e3a;color:#fff;border:none" onclick="exportExcel()">⬇ 匯出 Excel</button>
    <button class="btn btn-sm btn-ghost" style="color:#aaa;border-color:#444;font-size:10px" onclick="exportJSON()" title="匯出 JSON 備份">JSON備份</button>
    <label class="btn btn-sm btn-ghost" style="color:#aaa;border-color:#444;cursor:pointer;font-size:10px" title="從 JSON 還原">還原<input type="file" accept=".json" style="display:none" onchange="importJSON(this)"></label>
  </div>
</header>

<div class="wrap">
  <!-- SIDEBAR -->
  <aside class="sidebar">
    <div class="sb-hd">
      <div class="sb-hd-lbl">產品列表</div>
      <input class="sb-search" id="sb-search" placeholder="搜尋產品…" oninput="renderSidebar()">
    </div>
    <div class="sb-body" id="sb-body"></div>
    <div class="sb-ft">
      <button class="btn-add-prod" onclick="openNewProd()">＋ 新增產品</button>
    </div>
  </aside>

  <div class="main-area">

    <!-- ════ PAGE: 產品成本 ════ -->
    <div class="page on" id="pg-prod">
      <div id="no-prod" class="empty-state">
        <div class="empty-icon">📦</div>
        <div style="font-size:14px;font-weight:700">請選擇或新增產品</div>
        <div style="font-size:11px">點選左側「新增產品」開始建立配方</div>
      </div>
      <div id="prod-editor" style="display:none">
        <div class="inner">

          <!-- 品名 / 規格 -->
          <div class="prod-hd">
            <div class="prod-hd-top">
              <div class="pname-field">
                <div class="pname-label">品名</div>
                <input class="pname-input" id="pe-name" placeholder="輸入品名…" oninput="autosave()">
              </div>
              <div class="fld" style="flex:1;min-width:160px">
                <label>規格 / 內容物</label>
                <input id="pe-spec" placeholder="例：1300g/包" oninput="autosave()">
              </div>
              <div class="fld" style="flex:0 0 80px">
                <label>每批產出數</label>
                <input type="number" id="pe-oq" placeholder="1" min="0.001" step="any" oninput="autosave();recalc()">
              </div>
              <div class="fld" style="flex:0 0 70px">
                <label>產出單位</label>
                <select id="pe-ou" onchange="autosave();recalc()">
                  <option>包</option><option>個</option><option>盒</option><option>份</option>
                  <option>斤</option><option>公斤</option><option>g</option><option>支</option>
                </select>
              </div>
              <div style="display:flex;gap:6px;margin-top:18px">
                <button class="btn btn-ghost btn-sm" onclick="deleteProd()">刪除</button>
                <button class="btn btn-ink btn-sm" onclick="exportCSV()">CSV</button>
                <button class="btn btn-ink btn-sm" onclick="window.print()">列印</button>
              </div>
            </div>
          </div>

          <!-- COST BAR -->
          <div class="cost-bar">
            <div class="cb ing"><div class="cb-lbl">料｜食材</div><div class="cb-val">$<span id="cv-ing">0.00</span></div><div class="cb-pct" id="cp-ing">0%</div></div>
            <div class="cb pkg"><div class="cb-lbl">料｜包材</div><div class="cb-val">$<span id="cv-pkg">0.00</span></div><div class="cb-pct" id="cp-pkg">0%</div></div>
            <div class="cb lab"><div class="cb-lbl">工｜人工</div><div class="cb-val">$<span id="cv-lab">0.00</span></div><div class="cb-pct" id="cp-lab">0%</div></div>
            <div class="cb fee"><div class="cb-lbl">費｜管銷</div><div class="cb-val">$<span id="cv-fee">0.00</span></div><div class="cb-pct" id="cp-fee">0%</div></div>
            <div class="cb tot">
              <div class="cb-lbl">每<span id="cv-unit">包</span>總成本</div>
              <div class="cb-val">$<span id="cv-tot">0.00</span></div>
              <div class="ratio-bar">
                <div class="rb" id="rb-ing" style="background:#8a4010"></div>
                <div class="rb" id="rb-pkg" style="background:#183060"></div>
                <div class="rb" id="rb-lab" style="background:#1a5c30"></div>
                <div class="rb" id="rb-fee" style="background:#5a2a7a"></div>
              </div>
            </div>
          </div>

          <!-- ① 食材原料 -->
          <div class="tcard">
            <div class="tcard-hd">
              <span class="tcard-title">① 食材原料成本</span>
              <div style="display:flex;align-items:center;gap:8px">
                <span class="tcard-sub" id="ing-subtotal-hd">小計：$0.00</span>
                <button class="btn btn-ink btn-sm" style="font-size:10px" onclick="openNLImport('ing')" title="自然語言快速輸入">✨ 自然語言輸入</button>
              </div>
            </div>
            <div class="tbl-scroll">
              <table class="T">
                <thead><tr>
                  <th style="width:90px">編碼</th>
                  <th style="min-width:150px">品名</th>
                  <th class="tr" style="width:90px">進價(含稅)</th>
                  <th style="width:70px">進貨單位</th>
                  <th class="tr" style="width:90px">單價(含稅)</th>
                  <th style="width:60px">單價單位</th>
                  <th class="tr" style="width:70px">用量</th>
                  <th style="width:60px">用量單位</th>
                  <th class="tr" style="width:90px">製造成本</th>
                  <th style="width:32px"></th>
                </tr></thead>
                <tbody id="ing-body"></tbody>
              </table>
            </div>
          </div>

          <!-- ② 包材物料 -->
          <div class="tcard">
            <div class="tcard-hd">
              <span class="tcard-title">② 包材物料成本</span>
              <span class="tcard-sub" id="pkg-subtotal-hd">小計：$0.00</span>
            </div>
            <div class="tbl-scroll">
              <table class="T">
                <thead><tr>
                  <th style="width:90px">編碼</th>
                  <th style="min-width:150px">品名</th>
                  <th class="tr" style="width:90px">進價(含稅)</th>
                  <th style="width:70px">進貨單位</th>
                  <th class="tr" style="width:90px">單價(含稅)</th>
                  <th style="width:60px">單價單位</th>
                  <th class="tr" style="width:70px">用量</th>
                  <th style="width:60px">用量單位</th>
                  <th class="tr" style="width:90px">製造成本</th>
                  <th style="width:32px"></th>
                </tr></thead>
                <tbody id="pkg-body"></tbody>
              </table>
            </div>
          </div>

          <!-- ③ 人工費 -->
          <div class="tcard">
            <div class="tcard-hd">
              <span class="tcard-title">③ 工資 / 人工費</span>
              <span class="tcard-sub" id="lab-subtotal-hd">小計：$0.00</span>
            </div>
            <div class="tbl-scroll">
              <table class="T">
                <thead><tr>
                  <th style="width:90px">編碼</th>
                  <th style="min-width:150px">工項名稱</th>
                  <th class="tr" style="width:90px">時薪</th>
                  <th style="width:70px">時薪單位</th>
                  <th class="tr" style="width:90px">單價(含稅)</th>
                  <th style="width:60px">單價單位</th>
                  <th class="tr" style="width:70px">用量</th>
                  <th style="width:60px">用量單位</th>
                  <th class="tr" style="width:90px">製造成本</th>
                  <th style="width:32px"></th>
                </tr></thead>
                <tbody id="lab-body"></tbody>
              </table>
            </div>
          </div>

          <!-- ④ 管銷費用 -->
          <div class="tcard">
            <div class="tcard-hd">
              <span class="tcard-title">④ 管銷費用攤提</span>
              <span class="tcard-sub" id="fee-subtotal-hd">小計：$0.00</span>
            </div>
            <div class="tbl-scroll">
              <table class="T">
                <thead><tr>
                  <th style="min-width:160px">費用項目</th>
                  <th class="tr" style="width:110px">金額（元）</th>
                  <th style="min-width:180px">備註</th>
                  <th style="width:32px"></th>
                </tr></thead>
                <tbody id="fee-body"></tbody>
              </table>
            </div>
          </div>

          <!-- ⑤ 客戶定價 -->
          <div class="tcard">
            <div class="tcard-hd">
              <span class="tcard-title">⑤ 客戶定價</span>
              <span class="tcard-sub">填入末端售價，自動計算毛利與毛利率</span>
            </div>
            <div class="tbl-scroll">
              <table class="price-tbl">
                <thead><tr>
                  <th style="min-width:160px">客戶名稱</th>
                  <th class="tr" style="width:120px">產品成本</th>
                  <th class="tr" style="width:140px">末端售價（自填）</th>
                  <th class="tr" style="width:120px">毛利</th>
                  <th class="tr" style="width:110px">毛利率</th>
                  <th style="width:32px"></th>
                </tr></thead>
                <tbody id="price-body"></tbody>
              </table>
            </div>
          </div>

        </div>
      </div>
    </div>

    <!-- ════ PAGE: 原料資料庫 ════ -->
    <div class="page" id="pg-raw">
      <div class="inner">
        <div class="lib-hd">
          <div><div class="lib-title">🌾 原料資料庫</div><div class="lib-sub">建立後，在產品配方輸入品名可自動帶入所有欄位</div></div>
          <div class="lib-actions">
            <input class="search-inp" id="raw-search" placeholder="搜尋編碼或品名…" oninput="renderRawLib()">
            <button class="btn btn-gold" onclick="openMatModal('raw',null)">＋ 新增食材</button>
          </div>
        </div>
        <div class="lib-count" id="raw-count">共 0 筆</div>
        <div class="tcard tbl-scroll">
          <table class="T">
            <thead><tr>
              <th style="width:90px">編碼</th><th style="min-width:140px">品名</th>
              <th style="min-width:120px">包裝規格</th>
              <th class="tr" style="width:90px">進價(含稅)</th>
              <th style="width:70px">進貨單位</th>
              <th class="tr" style="width:90px">單價(含稅)</th>
              <th style="width:60px">單價單位</th>
              <th class="tr" style="width:60px">用量</th>
              <th style="width:60px">用量單位</th>
              <th style="min-width:100px">備註</th>
              <th style="width:60px">規格</th>
              <th style="width:60px"></th>
            </tr></thead>
            <tbody id="raw-tbody"></tbody>
          </table>
        </div>
      </div>
    </div>

    <!-- ════ PAGE: 物料包材庫 ════ -->
    <div class="page" id="pg-pkg">
      <div class="inner">
        <div class="lib-hd">
          <div><div class="lib-title">📦 物料包材庫</div><div class="lib-sub">包材資料庫，在配方包材欄位輸入品名可自動帶入</div></div>
          <div class="lib-actions">
            <input class="search-inp" id="pkg-search" placeholder="搜尋編碼或品名…" oninput="renderPkgLib()">
            <button class="btn btn-blue" onclick="openMatModal('pkg',null)">＋ 新增包材</button>
          </div>
        </div>
        <div class="lib-count" id="pkg-count">共 0 筆</div>
        <div class="tcard tbl-scroll">
          <table class="T">
            <thead><tr>
              <th style="width:90px">編碼</th><th style="min-width:140px">品名</th>
              <th style="min-width:120px">包裝規格</th>
              <th class="tr" style="width:90px">進價(含稅)</th>
              <th style="width:70px">進貨單位</th>
              <th class="tr" style="width:90px">單價(含稅)</th>
              <th style="width:60px">單價單位</th>
              <th class="tr" style="width:60px">用量</th>
              <th style="width:60px">用量單位</th>
              <th style="min-width:100px">備註</th>
              <th style="width:60px">規格</th>
              <th style="width:60px"></th>
            </tr></thead>
            <tbody id="pkg-tbody"></tbody>
          </table>
        </div>
      </div>
    </div>

    <!-- ════ PAGE: 人工費率 ════ -->
    <div class="page" id="pg-lab">
      <div class="inner">
        <div class="lib-hd">
          <div><div class="lib-title">👷 人工費率</div><div class="lib-sub">設定各工種時薪或計件費率</div></div>
          <button class="btn btn-gold" onclick="openLabModal(null)">＋ 新增工項</button>
        </div>
        <div class="tcard tbl-scroll">
          <table class="T">
            <thead><tr>
              <th style="width:90px">編碼</th>
              <th style="min-width:160px">品名</th>
              <th style="min-width:100px">包裝規格</th>
              <th class="tr" style="width:80px">時薪</th>
              <th style="width:70px">時薪單位</th>
              <th class="tr" style="width:80px">單價(含稅)</th>
              <th style="width:60px">單價單位</th>
              <th class="tr" style="width:70px">用量</th>
              <th style="width:60px">用量單位</th>
              <th style="min-width:120px">備註</th>
              <th style="width:60px"></th>
            </tr></thead>
            <tbody id="lab-lib-tbody"></tbody>
          </table>
        </div>
      </div>
    </div>

    <!-- ════ PAGE: 資料庫管理 ════ -->
    <div class="page" id="pg-db">
      <div class="db-page">

        <!-- 統計卡片 -->
        <div class="db-stats">
          <div class="stat-card"><div class="stat-num" id="db-cnt-raw">0</div><div class="stat-lbl">🌾 食材原料筆數</div></div>
          <div class="stat-card"><div class="stat-num" id="db-cnt-pkg">0</div><div class="stat-lbl">📦 包材物料筆數</div></div>
          <div class="stat-card"><div class="stat-num" id="db-cnt-lab">0</div><div class="stat-lbl">👷 人工工項筆數</div></div>
          <div class="stat-card"><div class="stat-num" id="db-cnt-prod">0</div><div class="stat-lbl">📋 產品配方筆數</div></div>
        </div>

        <!-- 分頁 tabs -->
        <div class="db-tab-row">
          <button class="db-tab on" onclick="dbSwitchTab('dbt-raw',this)">🌾 食材原料</button>
          <button class="db-tab"    onclick="dbSwitchTab('dbt-pkg',this)">📦 包材物料</button>
          <button class="db-tab"    onclick="dbSwitchTab('dbt-lab',this)">👷 人工費率</button>
          <button class="db-tab"    onclick="dbSwitchTab('dbt-prod',this)">📋 產品配方</button>
        </div>

        <!-- 食材原料 tab -->
        <div id="dbt-raw">
          <div class="db-toolbar">
            <input class="search-inp" id="db-raw-search" placeholder="🔍 搜尋編碼或品名…" oninput="dbRenderRaw()">
            <button class="btn btn-gold" onclick="openMatModal('raw',null)">＋ 新增食材</button>
            <button class="btn btn-ink" onclick="openPasteModal('raw')">📋 貼上匯入</button>
            <button class="btn btn-ghost btn-sm" onclick="dbExportCSV('raw')">⬇ 匯出CSV</button>
            <button class="btn btn-red btn-sm" onclick="dbClearConfirm('raw')" style="margin-left:auto">清空食材庫</button>
          </div>
          <div class="tcard tbl-scroll">
            <table class="T">
              <thead><tr>
                <th style="width:90px">編碼</th><th style="min-width:150px">品名</th>
                <th style="min-width:110px">包裝規格</th>
                <th class="tr" style="width:85px">進價(含稅)</th>
                <th style="width:68px">進貨單位</th>
                <th class="tr" style="width:100px">單價(含稅)</th>
                <th style="width:58px">單價單位</th>
                <th style="min-width:90px">備註</th>
                <th style="width:68px">操作</th>
              </tr></thead>
              <tbody id="db-raw-tbody"></tbody>
            </table>
          </div>
        </div>

        <!-- 包材物料 tab -->
        <div id="dbt-pkg" style="display:none">
          <div class="db-toolbar">
            <input class="search-inp" id="db-pkg-search" placeholder="🔍 搜尋編碼或品名…" oninput="dbRenderPkg()">
            <button class="btn btn-blue" onclick="openMatModal('pkg',null)">＋ 新增包材</button>
            <button class="btn btn-ink" onclick="openPasteModal('pkg')">📋 貼上匯入</button>
            <button class="btn btn-ghost btn-sm" onclick="dbExportCSV('pkg')">⬇ 匯出CSV</button>
            <button class="btn btn-red btn-sm" onclick="dbClearConfirm('pkg')" style="margin-left:auto">清空包材庫</button>
          </div>
          <div class="tcard tbl-scroll">
            <table class="T">
              <thead><tr>
                <th style="width:90px">編碼</th><th style="min-width:150px">品名</th>
                <th style="min-width:110px">包裝規格</th>
                <th class="tr" style="width:85px">進價(含稅)</th>
                <th style="width:68px">進貨單位</th>
                <th class="tr" style="width:100px">單價(含稅)</th>
                <th style="width:58px">單價單位</th>
                <th style="min-width:90px">備註</th>
                <th style="width:68px">操作</th>
              </tr></thead>
              <tbody id="db-pkg-tbody"></tbody>
            </table>
          </div>
        </div>

        <!-- 人工費率 tab -->
        <div id="dbt-lab" style="display:none">
          <div class="db-toolbar">
            <button class="btn btn-gold" onclick="openLabModal(null)">＋ 新增工項</button>
            <button class="btn btn-ink" onclick="openPasteModal('lab')">📋 貼上匯入</button>
            <button class="btn btn-ghost btn-sm" onclick="dbExportCSV('lab')">⬇ 匯出CSV</button>
          </div>
          <div class="tcard tbl-scroll">
            <table class="T">
              <thead><tr>
                <th style="width:90px">編碼</th><th style="min-width:160px">品名</th>
                <th class="tr" style="width:80px">時薪</th>
                <th style="width:68px">時薪單位</th>
                <th class="tr" style="width:80px">單價(含稅)</th>
                <th style="width:58px">單價單位</th>
                <th style="min-width:100px">備註</th>
                <th style="width:68px">操作</th>
              </tr></thead>
              <tbody id="db-lab-tbody"></tbody>
            </table>
          </div>
        </div>

        <!-- 產品配方 tab -->
        <div id="dbt-prod" style="display:none">
          <div class="db-toolbar">
            <input class="search-inp" id="db-prod-search" placeholder="🔍 搜尋產品名稱…" oninput="dbRenderProd()">
            <button class="btn btn-gold" onclick="openNewProd()">＋ 新增產品</button>
            <button class="btn btn-ghost btn-sm" onclick="dbExportCSV('prod')">⬇ 匯出CSV</button>
          </div>
          <div class="tcard tbl-scroll">
            <table class="T">
              <thead><tr>
                <th style="min-width:160px">品名</th>
                <th style="min-width:120px">規格</th>
                <th class="tr" style="width:90px">每批產出</th>
                <th style="width:60px">單位</th>
                <th class="tr" style="width:90px">每單位成本</th>
                <th style="width:60px">食材行數</th>
                <th style="width:60px">包材行數</th>
                <th style="width:68px">操作</th>
              </tr></thead>
              <tbody id="db-prod-tbody"></tbody>
            </table>
          </div>
        </div>

      </div>
    </div>

  </div><!-- main-area -->
</div><!-- wrap -->

<!-- ════ MODAL: 新增產品 ════ -->
<div class="modal-bg" id="modal-new-prod">
  <div class="modal">
    <div class="modal-hd"><div class="modal-title">新增產品</div><button class="modal-x" onclick="CM('modal-new-prod')">✕</button></div>
    <div class="modal-body">
      <div class="frow c2">
        <div class="fi"><label>品名 *</label><input id="np-name" placeholder="例：蟲草藥膳湯"></div>
        <div class="fi"><label>規格 / 內容物</label><input id="np-spec" placeholder="例：1300g/包"></div>
      </div>
      <div class="frow c4">
        <div class="fi"><label>每批產出數</label><input type="number" id="np-oq" placeholder="1" min="0.001" step="any"></div>
        <div class="fi"><label>產出單位</label>
          <select id="np-ou"><option>包</option><option>個</option><option>盒</option><option>份</option>
            <option>斤</option><option>公斤</option><option>g</option><option>支</option></select></div>
        <div class="fi"><label>客戶售價（選填）</label><input type="number" id="np-p1" placeholder="0" min="0" step="any"></div>
        <div class="fi"><label>零售售價（選填）</label><input type="number" id="np-p2" placeholder="0" min="0" step="any"></div>
      </div>
    </div>
    <div class="modal-ft">
      <button class="btn btn-ghost btn-sm" onclick="CM('modal-new-prod')">取消</button>
      <button class="btn btn-gold btn-sm" onclick="createProd()">建立產品</button>
    </div>
  </div>
</div>

<!-- ════ MODAL: 原料 / 包材 ════ -->
<div class="modal-bg" id="modal-mat">
  <div class="modal">
    <div class="modal-hd"><div class="modal-title" id="mat-modal-title">新增食材</div><button class="modal-x" onclick="CM('modal-mat')">✕</button></div>
    <div class="modal-body">
      <div class="frow c2">
        <div class="fi"><label>編碼</label><input id="mm-code" placeholder="例：DEA04"></div>
        <div class="fi"><label>品名 *</label><input id="mm-name" placeholder=""></div>
      </div>
      <div class="frow c1">
        <div class="fi"><label>包裝規格</label><input id="mm-spec" placeholder="例：1kg/25包/袋"></div>
      </div>
      <div class="frow c3">
        <div class="fi"><label>進價(含稅)</label><input type="number" id="mm-buyprice" placeholder="0" min="0" step="any" oninput="calcMM()"></div>
        <div class="fi"><label>採購數量</label><input type="number" id="mm-buyqty" placeholder="1" min="0.001" step="any" oninput="calcMM()"></div>
        <div class="fi"><label>進貨單位</label><input id="mm-buyunit" placeholder="袋"></div>
      </div>
      <div class="frow c3">
        <div class="fi"><label>單價(含稅)</label><input type="number" id="mm-unitprice" placeholder="自動計算" step="any" oninput="calcMM2()"></div>
        <div class="fi"><label>單價單位</label><input id="mm-priceunit" placeholder="g"></div>
        <div class="fi"><label>規格換算</label><input type="number" id="mm-spec2" placeholder="1000" step="any" oninput="calcMM()"></div>
      </div>
      <div class="calc-hint" id="mm-hint"></div>
      <div class="frow c2">
        <div class="fi"><label>備註</label><input id="mm-note" placeholder=""></div>
        <div class="fi"><label>規格欄</label><input id="mm-spec3" placeholder=""></div>
      </div>
    </div>
    <div class="modal-ft">
      <button class="btn btn-ghost btn-sm" onclick="CM('modal-mat')">取消</button>
      <button class="btn btn-gold btn-sm" id="mm-save-btn" onclick="saveMat()">儲存</button>
    </div>
  </div>
</div>

<!-- ════ MODAL: 人工 ════ -->
<div class="modal-bg" id="modal-lab">
  <div class="modal">
    <div class="modal-hd"><div class="modal-title" id="lab-modal-title">新增工項</div><button class="modal-x" onclick="CM('modal-lab')">✕</button></div>
    <div class="modal-body">
      <div class="frow c2">
        <div class="fi"><label>編碼</label><input id="lm-code" placeholder="例：B0001"></div>
        <div class="fi"><label>品名 *</label><input id="lm-name" placeholder="例：人力成本(主廚)"></div>
      </div>
      <div class="frow c1">
        <div class="fi"><label>包裝規格</label><input id="lm-spec" placeholder="例：hr"></div>
      </div>
      <div class="frow c4">
        <div class="fi"><label>時薪</label><input type="number" id="lm-rate" placeholder="0" min="0" step="any"></div>
        <div class="fi"><label>時薪單位</label><input id="lm-rateunit" placeholder="1hr"></div>
        <div class="fi"><label>單價(含稅)</label><input type="number" id="lm-unitprice" placeholder="同時薪" step="any"></div>
        <div class="fi"><label>單價單位</label><input id="lm-priceunit" placeholder="hr"></div>
      </div>
      <div class="frow c1">
        <div class="fi"><label>備註</label><input id="lm-note" placeholder=""></div>
      </div>
    </div>
    <div class="modal-ft">
      <button class="btn btn-ghost btn-sm" onclick="CM('modal-lab')">取消</button>
      <button class="btn btn-gold btn-sm" id="lm-save-btn" onclick="saveLab()">儲存</button>
    </div>
  </div>
</div>

<!-- ════ MODAL: 自然語言輸入 ════ -->
<div class="modal-bg nl-modal" id="modal-nl">
  <div class="modal">
    <div class="modal-hd">
      <div class="modal-title">✨ 自然語言快速建檔</div>
      <button class="modal-x" onclick="CM('modal-nl')">✕</button>
    </div>
    <div class="modal-body" style="max-height:82vh;overflow-y:auto">

      <!-- 輸入區 -->
      <div style="margin-bottom:12px">
        <div style="font-size:11px;color:var(--ink3);margin-bottom:8px;line-height:1.6">
          直接輸入食材清單，每行一項，格式自由。系統會自動比對資料庫，找到的直接帶入單價，找不到的標記為待補建。
        </div>
        <textarea class="nl-textarea" id="nl-input" placeholder="範例：&#10;杏鮑菇200斤&#10;麥片絲20斤（干）&#10;鹽44兩&#10;控肉精72兩&#10;素肉醬36兩&#10;香油48兩&#10;&#10;格式支援：品名+數量+單位、中文數字、括號備註等"></textarea>
        <div style="display:flex;gap:8px;margin-top:8px;align-items:center">
          <button class="btn btn-gold" id="nl-parse-btn" onclick="runNLParse()">✨ AI 解析</button>
          <button class="btn btn-ghost btn-sm" onclick="document.getElementById('nl-input').value=''">清除</button>
          <span style="font-size:11px;color:var(--ink3)" id="nl-api-status"></span>
        </div>
      </div>

      <!-- 解析結果 -->
      <div id="nl-result-wrap" style="display:none">
        <div style="font-size:10px;font-weight:700;letter-spacing:.08em;text-transform:uppercase;color:var(--ink3);margin-bottom:8px;display:flex;align-items:center;gap:10px">
          解析結果
          <span style="flex:1;height:1px;background:var(--border)"></span>
          <span id="nl-legend" style="display:flex;gap:10px;font-weight:400;text-transform:none;letter-spacing:0">
            <span><span class="nl-badge match">●</span> 完全比對</span>
            <span><span class="nl-badge fuzzy">●</span> 模糊比對</span>
            <span><span class="nl-badge new">●</span> 新品項</span>
          </span>
        </div>
        <div style="border:1px solid var(--border);border-radius:var(--r);overflow:hidden;background:var(--surface)">
          <div id="nl-result-list"></div>
        </div>
        <div style="margin-top:8px;font-size:11px;color:var(--ink3)" id="nl-result-summary"></div>
      </div>

      <!-- 思考中 -->
      <div id="nl-thinking" style="display:none">
        <div class="nl-thinking">
          <div class="nl-spinner"></div>
          <span>AI 正在解析您的食材清單並比對資料庫…</span>
        </div>
      </div>

    </div>
    <div class="modal-ft">
      <button class="btn btn-ghost btn-sm" onclick="CM('modal-nl')">取消</button>
      <button class="btn btn-gold btn-sm" id="nl-import-btn" style="display:none" onclick="executeNLImport()">✓ 加入配方</button>
    </div>
  </div>
</div>

<!-- ════ MODAL: 貼上匯入 ════ -->
<div class="modal-bg paste-modal" id="modal-paste">
  <div class="modal" style="width:820px;max-width:97vw">
    <div class="modal-hd">
      <div class="modal-title">📋 貼上匯入 — <span id="paste-modal-type">食材原料</span></div>
      <button class="modal-x" onclick="CM('modal-paste')">✕</button>
    </div>
    <div class="modal-body" style="max-height:80vh;overflow-y:auto">

      <!-- Step 1 -->
      <div class="step-row">
        <span class="step-badge">1</span>
        <div class="step-body">
          <div style="font-weight:700;font-size:12px;margin-bottom:6px">從 Excel 複製資料，貼到下方框</div>
          <div style="font-size:11px;color:var(--ink3);margin-bottom:8px">
            支援直接從 Excel / Google Sheets 複製整欄貼上。系統會自動辨識欄位順序。<br>
            <strong>建議欄位順序：</strong> 編碼 | 品名 | 包裝規格 | 進價(含稅) | 進貨單位 | 單價(含稅) | 單價單位 | 備註
          </div>
          <textarea class="paste-area" id="paste-textarea" placeholder="在此貼上從 Excel 複製的資料（Ctrl+V / Cmd+V）&#10;&#10;範例：&#10;DEA04	高級精鹽	1kg/25包/袋	199.5	袋	0.00798	g	&#10;DEA05	鮮味多	1kg/包	241.5	包	0.2415	g	" oninput="parsePaste()"></textarea>
        </div>
      </div>

      <!-- Step 2: 欄位對應 -->
      <div class="step-row" id="paste-step2" style="display:none">
        <span class="step-badge">2</span>
        <div class="step-body">
          <div style="font-weight:700;font-size:12px;margin-bottom:8px">確認欄位對應 <span style="font-size:10px;color:var(--ink3);font-weight:400">（系統已自動辨識，可手動調整）</span></div>
          <div class="col-map" id="paste-col-map"></div>
        </div>
      </div>

      <!-- Step 3: 預覽 -->
      <div class="step-row" id="paste-step3" style="display:none">
        <span class="step-badge">3</span>
        <div class="step-body">
          <div style="font-weight:700;font-size:12px;margin-bottom:8px">預覽 <span style="font-size:10px;color:var(--ink3);font-weight:400" id="paste-preview-count"></span></div>
          <div style="overflow-x:auto;max-height:240px;border:1px solid var(--border);border-radius:var(--r)">
            <table class="preview-table" id="paste-preview-tbl">
              <thead><tr id="paste-preview-head"></tr></thead>
              <tbody id="paste-preview-body"></tbody>
            </table>
          </div>
          <div id="paste-result-msg" style="margin-top:8px"></div>
        </div>
      </div>

      <!-- 重複處理選項 -->
      <div id="paste-dup-opt" style="display:none;margin-top:4px">
        <div style="font-size:11px;font-weight:700;margin-bottom:6px;color:var(--ink2)">遇到相同編碼時：</div>
        <div style="display:flex;gap:12px;flex-wrap:wrap">
          <label style="font-size:12px;cursor:pointer;display:flex;align-items:center;gap:5px">
            <input type="radio" name="dup-mode" value="skip" checked> 跳過（保留原有）</label>
          <label style="font-size:12px;cursor:pointer;display:flex;align-items:center;gap:5px">
            <input type="radio" name="dup-mode" value="overwrite"> 覆蓋（更新數值）</label>
          <label style="font-size:12px;cursor:pointer;display:flex;align-items:center;gap:5px">
            <input type="radio" name="dup-mode" value="both"> 全部新增（允許重複）</label>
        </div>
      </div>

    </div>
    <div class="modal-ft">
      <button class="btn btn-ghost btn-sm" onclick="CM('modal-paste')">取消</button>
      <button class="btn btn-ghost btn-sm" onclick="clearPaste()">清除</button>
      <button class="btn btn-gold btn-sm" id="paste-import-btn" style="display:none" onclick="executePasteImport()">✓ 匯入</button>
    </div>
  </div>
</div>

<script>
// ═══════════════════════════════════════════════════════
// DB & STORAGE
// ═══════════════════════════════════════════════════════
const SK = 'fcs_v4';
let DB = { raw:[], pkg:[], lab:[], prods:[], _id:1 };

function loadDB(){ try{ const s=localStorage.getItem(SK); if(s) Object.assign(DB,JSON.parse(s)); }catch(e){} }
function saveDB(){ try{ localStorage.setItem(SK,JSON.stringify(DB)); setSave(true); }catch(e){} }
function setSave(ok){
  const el=document.getElementById('save-status');
  el.textContent = ok ? '● 已儲存' : '● 儲存中…';
  el.className = 'hdr-save' + (ok?' ok':'');
}
function uid(){ return DB._id++; }
function f2(n,d=2){ return typeof n==='number'&&isFinite(n) ? n.toFixed(d) : '—'; }

// ═══════════════════════════════════════════════════════
// SEED DATA (from Excel)
// ═══════════════════════════════════════════════════════
const RAW_SEED = [
  {code:'BAA01',name:'木耳',spec:'3斤/包',buyPrice:133.3,buyQty:1800,buyUnit:'包',unitPrice:0.0741,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:''},
  {code:'BAA02',name:'炒香菇頭(2斤)',spec:'2斤/包',buyPrice:310,buyQty:2,buyUnit:'包',unitPrice:155,priceUnit:'斤',useQty:'',useUnit:'斤',note:'',spec2:''},
  {code:'DAA02',name:'紅蘿蔔',spec:'1公斤',buyPrice:21,buyQty:1000,buyUnit:'公斤',unitPrice:0.021,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:'1000'},
  {code:'DAA04',name:'九層塔',spec:'1斤',buyPrice:120.75,buyQty:600,buyUnit:'斤',unitPrice:0.20125,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:'600'},
  {code:'DAA09',name:'大辣椒',spec:'1斤',buyPrice:78.75,buyQty:600,buyUnit:'斤',unitPrice:0.13125,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:''},
  {code:'DAA10',name:'鮮香菇(下菇)',spec:'5斤',buyPrice:85.05,buyQty:600,buyUnit:'斤',unitPrice:0.14175,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:'600'},
  {code:'DAA11',name:'杏鮑菇(D級)',spec:'3kg/包',buyPrice:189,buyQty:3,buyUnit:'包',unitPrice:63,priceUnit:'公斤',useQty:'',useUnit:'公斤',note:'20斤',spec2:''},
  {code:'DAA14',name:'薑片',spec:'1斤',buyPrice:73.5,buyQty:600,buyUnit:'斤',unitPrice:0.1225,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:''},
  {code:'DAA15',name:'菜脯',spec:'12kg/箱',buyPrice:262.5,buyQty:20,buyUnit:'箱',unitPrice:13.125,priceUnit:'斤',useQty:'',useUnit:'斤',note:'',spec2:''},
  {code:'DAA19',name:'金針菇A級',spec:'1公斤',buyPrice:78.75,buyQty:1000,buyUnit:'公斤',unitPrice:0.07875,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:''},
  {code:'DAA20',name:'溼木耳(小耳)',spec:'1斤',buyPrice:78.75,buyQty:600,buyUnit:'斤',unitPrice:0.13125,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:''},
  {code:'DAA20-1',name:'大耳',spec:'1斤',buyPrice:73.5,buyQty:600,buyUnit:'斤',unitPrice:0.1225,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:''},
  {code:'DAA26',name:'髮菜',spec:'1斤',buyPrice:787.5,buyQty:600,buyUnit:'斤',unitPrice:1.3125,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:''},
  {code:'DAA28',name:'杏鮑菇(B級)',spec:'3kg/包',buyPrice:94.5,buyQty:1000,buyUnit:'公斤',unitPrice:0.0945,priceUnit:'g',useQty:'',useUnit:'g',note:'80斤',spec2:'1000'},
  {code:'DAA29',name:'台式大白菜',spec:'1斤',buyPrice:31.5,buyQty:600,buyUnit:'斤',unitPrice:0.0525,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:''},
  {code:'DAA30',name:'白蘿蔔',spec:'1斤',buyPrice:21.7,buyQty:160,buyUnit:'斤',unitPrice:0.1362,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:''},
  {code:'DAA33',name:'玉米筍',spec:'1斤',buyPrice:94.5,buyQty:600,buyUnit:'斤',unitPrice:0.1575,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:''},
  {code:'DAA34',name:'青椒',spec:'1斤',buyPrice:44.1,buyQty:600,buyUnit:'斤',unitPrice:0.0735,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:''},
  {code:'DAA35',name:'水蓮',spec:'1斤',buyPrice:117.6,buyQty:600,buyUnit:'斤',unitPrice:0.196,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:''},
  {code:'DBA01',name:'糯米',spec:'50斤/包',buyPrice:33.6,buyQty:0.6,buyUnit:'斤',unitPrice:56.01,priceUnit:'公斤',useQty:'',useUnit:'公斤',note:'',spec2:'1.667'},
  {code:'DBA03',name:'扣子菇(鈕扣菇)',spec:'1公斤',buyPrice:1008,buyQty:1000,buyUnit:'公斤',unitPrice:1.008,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:''},
  {code:'DBA04',name:'香菇頭(乾)',spec:'1公斤',buyPrice:262.5,buyQty:0.6,buyUnit:'公斤',unitPrice:151.2,priceUnit:'斤',useQty:'',useUnit:'斤',note:'',spec2:''},
  {code:'DBA05',name:'木耳(乾)',spec:'15斤/箱',buyPrice:183.75,buyQty:600,buyUnit:'斤',unitPrice:0.30625,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:''},
  {code:'DBA06',name:'松子',spec:'1公斤',buyPrice:1332,buyQty:1000,buyUnit:'公斤',unitPrice:1.332,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:''},
  {code:'DBA08',name:'碎肉(大豆蛋白GN-37)',spec:'20kg/袋',buyPrice:63,buyQty:1.67,buyUnit:'公斤',unitPrice:37.72,priceUnit:'斤',useQty:'',useUnit:'斤',note:'',spec2:'1.67'},
  {code:'DBA10',name:'素肉片(V-600片)',spec:'5kg/箱',buyPrice:90,buyQty:1000,buyUnit:'公斤',unitPrice:0.09,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:''},
  {code:'DBA11',name:'小麥肉片(V-G790)',spec:'5kg/包',buyPrice:135,buyQty:5,buyUnit:'包',unitPrice:27,priceUnit:'公斤',useQty:'',useUnit:'公斤',note:'',spec2:'5'},
  {code:'DBA18',name:'筍絲',spec:'1公斤',buyPrice:30.7,buyQty:1000,buyUnit:'公斤',unitPrice:0.0307,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:''},
  {code:'DBA24',name:'香菇絲',spec:'1公斤',buyPrice:892.5,buyQty:1000,buyUnit:'公斤',unitPrice:0.8925,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:''},
  {code:'DBA26',name:'巴西蘑菇',spec:'斤',buyPrice:750,buyQty:1,buyUnit:'斤',unitPrice:750,priceUnit:'斤',useQty:'',useUnit:'斤',note:'',spec2:''},
  {code:'DCA01',name:'冷凍栗子',spec:'1kg/包',buyPrice:157.5,buyQty:1000,buyUnit:'包',unitPrice:0.1575,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:''},
  {code:'DCA03-1',name:'黃金十全藥膳包',spec:'300g/包',buyPrice:72,buyQty:1,buyUnit:'包',unitPrice:72,priceUnit:'包',useQty:'',useUnit:'包',note:'加猴菇及腰果',spec2:''},
  {code:'DCA37',name:'黃豆皮(四角皮)',spec:'100張/包',buyPrice:240,buyQty:100,buyUnit:'包',unitPrice:2.4,priceUnit:'張',useQty:'',useUnit:'張',note:'千張-非基改',spec2:'100'},
  {code:'DCA37-1',name:'黃豆皮(已裁切)',spec:'800張/包',buyPrice:504,buyQty:800,buyUnit:'包',unitPrice:0.63,priceUnit:'張',useQty:'',useUnit:'張',note:'12cm*22cm',spec2:'800'},
  {code:'DCA38',name:'猴頭菇(純素)',spec:'3斤/包',buyPrice:450,buyQty:1800,buyUnit:'包',unitPrice:0.25,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:'1800'},
  {code:'DCA39',name:'芋頭角',spec:'5斤/箱',buyPrice:60,buyQty:600,buyUnit:'斤',unitPrice:0.1,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:''},
  {code:'DCA41',name:'豆包扁魚',spec:'300g/8片/包',buyPrice:94.5,buyQty:1,buyUnit:'包',unitPrice:94.5,priceUnit:'包',useQty:'',useUnit:'包',note:'',spec2:''},
  {code:'DCA42',name:'火腿切片',spec:'3kg/約150片/包',buyPrice:425.25,buyQty:150,buyUnit:'包',unitPrice:2.835,priceUnit:'片',useQty:'',useUnit:'片',note:'',spec2:''},
  {code:'DDA01',name:'太白粉(三朵花)',spec:'33.33斤/包',buyPrice:483,buyQty:20000,buyUnit:'包',unitPrice:0.02415,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:'20000'},
  {code:'DDA01-1',name:'太白粉(片力粉)',spec:'25kg/包',buyPrice:1365,buyQty:25,buyUnit:'包',unitPrice:54.6,priceUnit:'kg',useQty:'',useUnit:'kg',note:'',spec2:'25'},
  {code:'DDA02',name:'玉米粉',spec:'25公斤/包',buyPrice:580,buyQty:25000,buyUnit:'包',unitPrice:0.0232,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:'25000'},
  {code:'DDA03',name:'起司脆酥粉',spec:'1000g/包',buyPrice:89,buyQty:1000,buyUnit:'包',unitPrice:0.089,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:'1000'},
  {code:'DDA04',name:'酥脆粉WD-L006',spec:'1公斤',buyPrice:262.5,buyQty:1000,buyUnit:'公斤',unitPrice:0.2625,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:'1000'},
  {code:'DDB01',name:'中筋麵粉(泰和)',spec:'22kg/包',buyPrice:556.5,buyQty:22,buyUnit:'包',unitPrice:25.3,priceUnit:'公斤',useQty:'',useUnit:'公斤',note:'',spec2:'22'},
  {code:'DDD11',name:'小麥蛋白',spec:'25Kg/包',buyPrice:3600,buyQty:25000,buyUnit:'包',unitPrice:0.144,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:'25000'},
  {code:'DEA01',name:'黑胡椒粉(小磨坊)',spec:'600g/包',buyPrice:315,buyQty:600,buyUnit:'包',unitPrice:0.525,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:'600'},
  {code:'DEA03',name:'二砂糖',spec:'1斤/包',buyPrice:17.0625,buyQty:600,buyUnit:'包',unitPrice:0.028438,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:'600'},
  {code:'DEA04',name:'高級精鹽',spec:'1kg/25包/袋',buyPrice:199.5,buyQty:25000,buyUnit:'袋',unitPrice:0.00798,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:'25000'},
  {code:'DEA05',name:'鮮味多',spec:'1kg/包',buyPrice:241.5,buyQty:1000,buyUnit:'包',unitPrice:0.2415,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:'1000'},
  {code:'DEA06',name:'五香粉(小磨坊)',spec:'600g/盒',buyPrice:183.75,buyQty:600,buyUnit:'盒',unitPrice:0.30625,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:'600'},
  {code:'DEA07',name:'甘草粉(小磨坊)',spec:'300g/盒',buyPrice:136.5,buyQty:300,buyUnit:'盒',unitPrice:0.455,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:'300'},
  {code:'DEA17',name:'糖粉',spec:'1斤/包',buyPrice:36.75,buyQty:600,buyUnit:'包',unitPrice:0.16125,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:''},
  {code:'DEA20',name:'大豆蛋白粉',spec:'20kg/袋',buyPrice:105,buyQty:1000,buyUnit:'公斤',unitPrice:0.105,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:''},
  {code:'DEA23',name:'海藻糖',spec:'1000g/包',buyPrice:180,buyQty:1000,buyUnit:'包',unitPrice:0.18,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:''},
  {code:'DEA24',name:'白冰糖',spec:'1斤/包',buyPrice:55,buyQty:600,buyUnit:'包',unitPrice:0.0917,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:''},
  {code:'DEA27',name:'素黏膠',spec:'1公斤',buyPrice:682.5,buyQty:1000,buyUnit:'公斤',unitPrice:0.6825,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:'1000'},
  {code:'DFA01',name:'香椿原醬',spec:'30斤/桶',buyPrice:2047.5,buyQty:30,buyUnit:'桶',unitPrice:68.25,priceUnit:'斤',useQty:'',useUnit:'斤',note:'',spec2:'30'},
  {code:'DFA02',name:'紅糟',spec:'5斤/箱',buyPrice:210,buyQty:3000,buyUnit:'箱',unitPrice:0.07,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:''},
  {code:'DFB01',name:'香油',spec:'4.5斤/桶',buyPrice:298.34,buyQty:2700,buyUnit:'桶',unitPrice:0.1105,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:'2700'},
  {code:'DFB02',name:'沙拉油',spec:'18公升/桶',buyPrice:1018.5,buyQty:14400,buyUnit:'桶',unitPrice:0.07073,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:'14400'},
  {code:'DFB05',name:'仲味麻油3L',spec:'3L/桶',buyPrice:415,buyQty:2400,buyUnit:'桶',unitPrice:0.173,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:''},
  {code:'DFC02',name:'素蠔油',spec:'6kg/桶',buyPrice:254.625,buyQty:6000,buyUnit:'桶',unitPrice:0.042438,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:'6000'},
  {code:'DFC03',name:'素肉醬',spec:'1kg/罐',buyPrice:651,buyQty:1000,buyUnit:'罐',unitPrice:0.651,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:'1000'},
  {code:'DFC05',name:'爌肉精-大罐',spec:'1400g/罐',buyPrice:766.5,buyQty:1400,buyUnit:'罐',unitPrice:0.5475,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:'1400'},
  {code:'DFC06',name:'素沙茶(愛之味)',spec:'18kg/桶',buyPrice:2850,buyQty:1800,buyUnit:'桶',unitPrice:1.5833,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:'1800'},
  {code:'DFC08',name:'番茄醬(可果美)',spec:'3.15kg/桶',buyPrice:192.5,buyQty:3150,buyUnit:'桶',unitPrice:0.06111,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:'3150'},
  {code:'DFC10',name:'味醂',spec:'1.8L/罐',buyPrice:145,buyQty:1584,buyUnit:'罐',unitPrice:0.09167,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:''},
  {code:'DFC11',name:'素烏醋(工研)',spec:'5L/桶',buyPrice:210,buyQty:5000,buyUnit:'桶',unitPrice:0.042,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:''},
  {code:'DFC14',name:'萬家香醬油',spec:'5公升/桶',buyPrice:278.25,buyQty:5000,buyUnit:'桶',unitPrice:0.05565,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:'5000'},
  {code:'DFC16',name:'紅麴養生醬',spec:'3kg/桶',buyPrice:525,buyQty:3000,buyUnit:'桶',unitPrice:0.175,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:'3000'},
  {code:'DGA01',name:'乳瑪琳(遠東)',spec:'2.6kg/罐',buyPrice:521.5,buyQty:2600,buyUnit:'罐',unitPrice:0.20058,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:'2600'},
  {code:'DGA02',name:'鮮奶油(無糖)',spec:'1000g/罐',buyPrice:168,buyQty:1000,buyUnit:'罐',unitPrice:0.168,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:'1000'},
  {code:'DHA01',name:'紅棗',spec:'600g/包',buyPrice:65,buyQty:600,buyUnit:'包',unitPrice:0.10833,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:'600'},
  {code:'DHA02',name:'黑棗',spec:'600g/包',buyPrice:110,buyQty:709,buyUnit:'包',unitPrice:0.1417,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:''},
  {code:'DHA03',name:'桂枝',spec:'600g/包',buyPrice:55,buyQty:600,buyUnit:'包',unitPrice:0.0917,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:''},
  {code:'DHA04',name:'枸杞',spec:'600g/包',buyPrice:168,buyQty:600,buyUnit:'包',unitPrice:0.28,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:'600'},
  {code:'DHA08',name:'肉桂粉(油桂粉)',spec:'600g/包',buyPrice:204.75,buyQty:600,buyUnit:'包',unitPrice:0.34125,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:''},
  {code:'DHA10',name:'肉桂片',spec:'600g/包',buyPrice:210,buyQty:600,buyUnit:'包',unitPrice:0.35,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:''},
  {code:'DHA11',name:'甘草片',spec:'600g/盒',buyPrice:158,buyQty:600,buyUnit:'盒',unitPrice:0.2634,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:''},
  {code:'DHA12',name:'當歸片',spec:'600g/包',buyPrice:600,buyQty:600,buyUnit:'包',unitPrice:1,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:'600'},
  {code:'DHA13',name:'黨參片',spec:'600g/包',buyPrice:550,buyQty:600,buyUnit:'包',unitPrice:0.91667,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:'600'},
  {code:'DHA14',name:'熟地片',spec:'600g/包',buyPrice:190,buyQty:600,buyUnit:'包',unitPrice:0.3167,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:''},
  {code:'DHA15',name:'川芎片',spec:'600g/包',buyPrice:210,buyQty:600,buyUnit:'包',unitPrice:0.35,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:''},
  {code:'DHA16',name:'黃耆片',spec:'600g/包',buyPrice:168,buyQty:600,buyUnit:'包',unitPrice:0.28,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:'600'},
  {code:'DHA18',name:'北蟲草',spec:'斤',buyPrice:430,buyQty:1,buyUnit:'斤',unitPrice:430,priceUnit:'斤',useQty:'',useUnit:'斤',note:'',spec2:''},
  {code:'EZA04',name:'荷葉',spec:'1斤',buyPrice:157.5,buyQty:600,buyUnit:'斤',unitPrice:0.2625,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:''},
  {code:'未建8',name:'腰果',spec:'18.9斤/箱',buyPrice:3497,buyQty:11340,buyUnit:'箱',unitPrice:0.3084,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:''},
  {code:'未建21',name:'白木耳',spec:'10斤/箱',buyPrice:230,buyQty:600,buyUnit:'斤',unitPrice:0.3834,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:''},
  {code:'未建22',name:'鳳眼果(真空包)',spec:'1斤/包',buyPrice:330,buyQty:600,buyUnit:'斤',unitPrice:0.55,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:''},
  {code:'未建25',name:'冬菜',spec:'1斤',buyPrice:157.5,buyQty:600,buyUnit:'斤',unitPrice:0.2625,priceUnit:'g',useQty:'',useUnit:'g',note:'',spec2:''},
  {code:'A0001',name:'水',spec:'1噸(1000kg)',buyPrice:15,buyQty:1000000,buyUnit:'噸',unitPrice:0.000015,priceUnit:'cc',useQty:'',useUnit:'cc',note:'',spec2:''},
  {code:'A0002',name:'麻油爆薑(自配)',spec:'600g/包',buyPrice:156,buyQty:1000,buyUnit:'包',unitPrice:0.26,priceUnit:'g',useQty:'',useUnit:'g',note:'自行調配',spec2:''},
  {code:'A0003',name:'胡椒鹽-調配',spec:'6g/包',buyPrice:2.5085,buyQty:1,buyUnit:'包',unitPrice:2.5085,priceUnit:'包',useQty:'',useUnit:'包',note:'自行調配',spec2:''},
  {code:'A0004',name:'水餃漿',spec:'1g',buyPrice:0.0534,buyQty:1,buyUnit:'g',unitPrice:0.0534,priceUnit:'g',useQty:'',useUnit:'g',note:'自行調配',spec2:''},
  {code:'A0005',name:'餛飩漿',spec:'1g',buyPrice:0.125,buyQty:1,buyUnit:'g',unitPrice:0.125,priceUnit:'g',useQty:'',useUnit:'g',note:'自行調配',spec2:''},
];
const PKG_SEED = [
  {code:'EAB01',name:'餛飩3H盒(白)',spec:'100入/箱',buyPrice:0.7035,buyQty:1,buyUnit:'個',unitPrice:0.7035,priceUnit:'個',useQty:'',useUnit:'個',note:'',spec2:'1'},
  {code:'EBA01',name:'無標袋(PE袋/水餃袋)',spec:'1kg/袋(100個)',buyPrice:69.3,buyQty:100,buyUnit:'KG',unitPrice:0.693,priceUnit:'個',useQty:'',useUnit:'個',note:'',spec2:''},
  {code:'EBA01-1',name:'無標袋-真空22cm*32cm',spec:'100入*25包',buyPrice:190,buyQty:100,buyUnit:'包',unitPrice:1.9,priceUnit:'個',useQty:'',useUnit:'個',note:'',spec2:''},
  {code:'EBA01-3',name:'無標袋-真空20cm*27cm',spec:'100入*25包',buyPrice:170,buyQty:100,buyUnit:'包',unitPrice:1.7,priceUnit:'個',useQty:'',useUnit:'個',note:'',spec2:''},
  {code:'EBA02',name:'無標袋-真空17cm*27cm',spec:'100入*30包',buyPrice:130,buyQty:100,buyUnit:'包',unitPrice:1.3,priceUnit:'個',useQty:'',useUnit:'個',note:'',spec2:''},
  {code:'EBC21',name:'有標袋-卡脆G腿包裝袋',spec:'230*270mm',buyPrice:2.96,buyQty:1,buyUnit:'個',unitPrice:2.96,priceUnit:'個',useQty:'',useUnit:'個',note:'',spec2:''},
  {code:'EBB01',name:'PE透明平口袋-素螺',spec:'1kg約500個',buyPrice:73.5,buyQty:500,buyUnit:'KG',unitPrice:0.147,priceUnit:'個',useQty:'',useUnit:'個',note:'',spec2:''},
  {code:'EBD01',name:'通用袋-得來素',spec:'190*265mm',buyPrice:2.4,buyQty:1,buyUnit:'個',unitPrice:2.4,priceUnit:'個',useQty:'',useUnit:'個',note:'',spec2:''},
  {code:'ECB01',name:'胡椒鹽封膜(鋁膜)',spec:'1捲6500包',buyPrice:1105,buyQty:6500,buyUnit:'捲',unitPrice:0.17,priceUnit:'包',useQty:'',useUnit:'包',note:'',spec2:'6500'},
  {code:'EEA01',name:'空白紙箱(2才)',spec:'448*298*402mm',buyPrice:26.25,buyQty:1,buyUnit:'個',unitPrice:26.25,priceUnit:'個',useQty:'',useUnit:'個',note:'',spec2:''},
  {code:'EEB01',name:'DLS紙箱(尺寸90)',spec:'408*280*210mm',buyPrice:12.6,buyQty:1,buyUnit:'個',unitPrice:12.6,priceUnit:'個',useQty:'',useUnit:'個',note:'有印刷',spec2:''},
  {code:'EEB02',name:'DLS紙箱(尺寸60)',spec:'285*205*130mm',buyPrice:6.3,buyQty:1,buyUnit:'個',unitPrice:6.3,priceUnit:'個',useQty:'',useUnit:'個',note:'有印刷',spec2:''},
  {code:'EEB03',name:'DLS紙箱(團購)',spec:'330*240*130mm',buyPrice:7.875,buyQty:1,buyUnit:'個',unitPrice:7.875,priceUnit:'個',useQty:'',useUnit:'個',note:'有印刷',spec2:''},
  {code:'EEB04',name:'DLS紙箱(尺寸90加厚)',spec:'408*290*210mm',buyPrice:21,buyQty:1,buyUnit:'個',unitPrice:21,priceUnit:'個',useQty:'',useUnit:'個',note:'外銷',spec2:''},
  {code:'EZA05',name:'冰棒棍',spec:'20000入/包',buyPrice:2287,buyQty:2000,buyUnit:'包',unitPrice:1.1435,priceUnit:'支',useQty:'',useUnit:'支',note:'淘寶買',spec2:'2000'},
  {code:'YAC02-1',name:'食品膜(南亞)',spec:'400cm*500米/支',buyPrice:556.5,buyQty:1000,buyUnit:'支',unitPrice:0.5565,priceUnit:'個',useQty:'',useUnit:'個',note:'',spec2:'1000'},
  {code:'C0001',name:'珠光亮標籤貼紙(10*5cm)',spec:'500張/卷',buyPrice:346.5,buyQty:500,buyUnit:'卷',unitPrice:0.693,priceUnit:'張',useQty:'',useUnit:'張',note:'',spec2:''},
  {code:'C0002',name:'碳帶-標籤貼紙(10cm)',spec:'300m/卷',buyPrice:997.5,buyQty:2500,buyUnit:'卷',unitPrice:0.399,priceUnit:'張',useQty:'',useUnit:'張',note:'',spec2:''},
  {code:'未建c2',name:'鋁泊袋',spec:'',buyPrice:4,buyQty:1,buyUnit:'個',unitPrice:4,priceUnit:'個',useQty:'',useUnit:'個',note:'髮菜、佛跳牆',spec2:''},
  {code:'未建c3',name:'青龍耐熱袋(半斤)',spec:'200個/袋',buyPrice:31,buyQty:200,buyUnit:'袋',unitPrice:0.155,priceUnit:'個',useQty:'',useUnit:'個',note:'',spec2:''},
  {code:'未建c6',name:'麻油猴菇貼紙',spec:'1000張',buyPrice:1701,buyQty:1000,buyUnit:'包',unitPrice:1.701,priceUnit:'張',useQty:'',useUnit:'張',note:'',spec2:''},
  {code:'未建c7',name:'夾鍊袋4號',spec:'100個',buyPrice:27,buyQty:100,buyUnit:'包',unitPrice:0.27,priceUnit:'個',useQty:'',useUnit:'個',note:'香酥G腿用',spec2:''},
];
const LAB_SEED = [
  {code:'B0001',name:'人力成本(主廚)',spec:'hr',rate:258,rateUnit:'1hr',unitPrice:258,priceUnit:'hr',useQty:'',useUnit:'hr',note:''},
  {code:'B0002',name:'人力成本(備料)',spec:'hr',rate:196,rateUnit:'1hr',unitPrice:196,priceUnit:'hr',useQty:'',useUnit:'hr',note:''},
  {code:'B0003',name:'人力成本(包裝)',spec:'hr',rate:196,rateUnit:'1hr',unitPrice:196,priceUnit:'hr',useQty:'',useUnit:'hr',note:''},
  {code:'B0004',name:'論件計酬-三角圓',spec:'斤',rate:18,rateUnit:'斤',unitPrice:18,priceUnit:'斤',useQty:'',useUnit:'斤',note:''},
];

function seedIfEmpty(){
  if(!DB.raw.length){ RAW_SEED.forEach(d=>{ d.id=uid(); DB.raw.push(d); }); }
  if(!DB.pkg.length){ PKG_SEED.forEach(d=>{ d.id=uid(); DB.pkg.push(d); }); }
  if(!DB.lab.length){ LAB_SEED.forEach(d=>{ d.id=uid(); DB.lab.push(d); }); }
  saveDB();
}

// ═══════════════════════════════════════════════════════
// SIDEBAR
// ═══════════════════════════════════════════════════════
let activeProd = null;

function renderSidebar(){
  const q=(document.getElementById('sb-search').value||'').toLowerCase();
  const el=document.getElementById('sb-body');
  const list=DB.prods.filter(p=>!q||p.name.toLowerCase().includes(q));
  if(!list.length){ el.innerHTML=`<div style="padding:14px;text-align:center;font-size:11px;color:var(--ink3)">${q?'找不到':'尚無產品'}</div>`; return; }
  el.innerHTML=list.map(p=>{
    const t=prodTotal(p);
    return `<div class="prod-card${p.id===activeProd?' on':''}" onclick="loadProd(${p.id})">
      <div class="pc-name">${p.name||'未命名'}</div>
      <div class="pc-spec">${p.spec||'—'}</div>
      <div class="pc-cost">$${f2(t)} / ${p.ou||'包'}</div>
    </div>`;
  }).join('');
}

function prodTotal(p){
  const oq=parseFloat(p.oq)||1;
  const s=arr=>arr.reduce((a,r)=>a+(parseFloat(r.cost)||0),0);
  return (s(p.ing)+s(p.pkg)+s(p.lab)+s(p.fee))/oq;
}

// ═══════════════════════════════════════════════════════
// LOAD PRODUCT
// ═══════════════════════════════════════════════════════
function loadProd(id){
  activeProd=id;
  const p=DB.prods.find(x=>x.id===id);
  if(!p) return;
  document.getElementById('no-prod').style.display='none';
  document.getElementById('prod-editor').style.display='block';
  document.getElementById('pe-name').value=p.name||'';
  document.getElementById('pe-spec').value=p.spec||'';
  document.getElementById('pe-oq').value=p.oq||1;
  document.getElementById('pe-ou').value=p.ou||'包';
  renderSidebar();
  renderIngTable(p);
  renderPkgTable(p);
  renderLabTable(p);
  renderFeeTable(p);
  renderPriceTable(p);
  recalc();
}

function autosave(){
  const p=DB.prods.find(x=>x.id===activeProd); if(!p) return;
  p.name=document.getElementById('pe-name').value;
  p.spec=document.getElementById('pe-spec').value;
  p.oq=parseFloat(document.getElementById('pe-oq').value)||1;
  p.ou=document.getElementById('pe-ou').value;
  saveDB(); renderSidebar();
}

// ═══════════════════════════════════════════════════════
// RECALC
// ═══════════════════════════════════════════════════════
function recalc(){
  const p=DB.prods.find(x=>x.id===activeProd); if(!p) return;
  autosave();
  const oq=parseFloat(p.oq)||1;
  const sum=arr=>arr.reduce((a,r)=>a+(parseFloat(r.cost)||0),0);
  const ing=sum(p.ing), pkg=sum(p.pkg), lab=sum(p.lab), fee=sum(p.fee);
  const batch=ing+pkg+lab+fee;
  const per=batch/oq;
  const pct=v=>batch>0?((v/batch)*100).toFixed(1)+'%':'0%';
  const w  =v=>batch>0?((v/batch)*100).toFixed(1)+'%':'0%';

  set('cv-ing',f2(ing/oq)); set('cv-pkg',f2(pkg/oq));
  set('cv-lab',f2(lab/oq)); set('cv-fee',f2(fee/oq));
  set('cv-tot',f2(per)); set('cv-unit',p.ou||'包');
  set('cp-ing',pct(ing)); set('cp-pkg',pct(pkg));
  set('cp-lab',pct(lab)); set('cp-fee',pct(fee));
  document.getElementById('rb-ing').style.width=w(ing);
  document.getElementById('rb-pkg').style.width=w(pkg);
  document.getElementById('rb-lab').style.width=w(lab);
  document.getElementById('rb-fee').style.width=w(fee);
  set('ing-subtotal-hd','小計：$'+f2(ing/oq));
  set('pkg-subtotal-hd','小計：$'+f2(pkg/oq));
  set('lab-subtotal-hd','小計：$'+f2(lab/oq));
  set('fee-subtotal-hd','小計：$'+f2(fee/oq));
  // 客戶定價表：成本變動後重新計算定價
  renderPriceTable(p);
  renderSidebar();
}
function set(id,v){ const e=document.getElementById(id); if(e) e.textContent=v; }

// ═══════════════════════════════════════════════════════
// TABLE RENDERERS
// Code cell AND Name cell both trigger autocomplete lookup
// ═══════════════════════════════════════════════════════
function makeRow(type, r, idx){
  const isLab = type==='lab';
  const col3lbl = isLab?'時薪':'進價(含稅)';
  const col4lbl = isLab?'時薪單位':'進貨單位';
  const hid = `row-${type}-${r.id}`;
  const cost = parseFloat(r.cost)||0;
  // filled = row already has data from DB (show lighter bg on non-editable fields)
  const filled = !!(r.name);
  const roStyle = filled ? 'background:#fdfbf5;color:var(--ink2)' : 'color:var(--ink4)';
  return `<tr id="${hid}">
    <!-- ① 編碼：輸入後 Tab/Enter 觸發查詢帶入 -->
    <td style="position:relative">
      <input class="ci-inp mono" id="code-inp-${type}-${r.id}" style="width:88px;font-weight:600"
        value="${r.code||''}" placeholder="輸入編碼"
        oninput="showCodeAC('${type}',${r.id},this.value)"
        onkeydown="codeKey(event,'${type}',${r.id})"
        onblur="codeBlur('${type}',${r.id})">
      <div class="ac-dd" id="code-dd-${type}-${r.id}"></div>
    </td>
    <!-- ② 品名：輸入後也可模糊搜尋帶入 -->
    <td>
      <div class="ac-wrap">
        <input class="ci-inp" id="ac-inp-${type}-${r.id}" value="${r.name||''}" placeholder="或輸入品名搜尋…"
          oninput="showAC('${type}',${r.id},this.value)"
          onkeydown="acKey(event,'${type}',${r.id})"
          onblur="delayHideAC('${type}',${r.id})"
          onchange="rowChange('${type}',${r.id},'name',this.value)">
        <div class="ac-dd" id="ac-dd-${type}-${r.id}"></div>
      </div>
    </td>
    <!-- ③④⑤⑥ 帶入後唯讀顯示，但仍可手動修改 -->
    <td><input class="ci-inp mono tr" style="width:88px;${roStyle}" type="number" value="${r.buyPrice||''}" step="any"
      placeholder="${col3lbl}" onchange="rowChange('${type}',${r.id},'buyPrice',this.value)" oninput="recalcRow('${type}',${r.id})"></td>
    <td><input class="ci-inp" style="width:68px;${roStyle}" value="${r.buyUnit||''}" placeholder="${col4lbl}" onchange="rowChange('${type}',${r.id},'buyUnit',this.value)"></td>
    <td><input class="ci-inp mono tr" style="width:88px;${roStyle}" type="number" value="${r.unitPrice||''}" step="any"
      placeholder="單價" onchange="rowChange('${type}',${r.id},'unitPrice',this.value)" oninput="recalcRow('${type}',${r.id})"></td>
    <td><input class="ci-inp" style="width:58px;${roStyle}" value="${r.priceUnit||''}" placeholder="單位" onchange="rowChange('${type}',${r.id},'priceUnit',this.value)"></td>
    <!-- ⑦⑧ 用量：重點輸入欄，帶入後游標自動跳到這裡 -->
    <td><input class="ci-inp mono tr" style="width:68px;font-weight:700" id="qty-inp-${type}-${r.id}" type="number" value="${r.qty||''}" step="any"
      placeholder="用量" onchange="rowChange('${type}',${r.id},'qty',this.value)" oninput="recalcRow('${type}',${r.id})"></td>
    <td><input class="ci-inp" style="width:58px;${roStyle}" value="${r.qtyUnit||''}" placeholder="單位" onchange="rowChange('${type}',${r.id},'qtyUnit',this.value)"></td>
    <!-- ⑨ 製造成本自動計算 -->
    <td><span class="cost-cell" id="cost-${type}-${r.id}">${cost>0?'$'+f2(cost):''}</span></td>
    <td style="text-align:center"><button class="btn-del" onclick="delRow('${type}',${r.id})">✕</button></td>
  </tr>`;
}

function addTriggerRow(type, label){
  return `<tr class="add-trigger-row"><td colspan="10">
    <button class="add-trigger-btn" onclick="addRow('${type}')">＋ ${label}</button>
  </td></tr>`;
}

function renderIngTable(p){
  const body=document.getElementById('ing-body');
  body.innerHTML = p.ing.map((r,i)=>makeRow('ing',r,i)).join('') + addTriggerRow('ing','新增食材原料');
}
function renderPkgTable(p){
  const body=document.getElementById('pkg-body');
  body.innerHTML = p.pkg.map((r,i)=>makeRow('pkg',r,i)).join('') + addTriggerRow('pkg','新增包材物料');
}
function renderLabTable(p){
  const body=document.getElementById('lab-body');
  body.innerHTML = p.lab.map((r,i)=>makeRow('lab',r,i)).join('') + addTriggerRow('lab','新增人工費');
}
function renderFeeTable(p){
  const body=document.getElementById('fee-body');
  const rows=p.fee.map(r=>`<tr>
    <td><input class="ci-inp" value="${r.name||''}" placeholder="費用項目（例：管銷費用）" style="width:100%" onchange="feeChange(${r.id},'name',this.value)"></td>
    <td><input class="ci-inp mono tr" type="number" value="${r.cost||''}" placeholder="0" step="any" style="width:108px" onchange="feeChange(${r.id},'cost',this.value)" oninput="recalc()"></td>
    <td><input class="ci-inp" value="${r.note||''}" placeholder="備註" style="width:100%" onchange="feeChange(${r.id},'note',this.value)"></td>
    <td style="text-align:center"><button class="btn-del" onclick="delFee(${r.id})">✕</button></td>
  </tr>`).join('');
  body.innerHTML=rows+`<tr class="add-trigger-row"><td colspan="4">
    <button class="add-trigger-btn" onclick="addFee()">＋ 新增管銷費用</button></td></tr>`;
}
function renderPriceTable(p){
  const body=document.getElementById('price-body');
  const cost=prodTotal(p);  // 每單位產品成本

  const rows=(p.prices||[]).map(r=>{
    const sp=parseFloat(r.sellPrice)||0;   // 末端售價（使用者填入）
    const profit=sp>0 ? sp-cost : null;
    const margin=sp>0 ? (profit/sp)*100 : null;

    const profitStr  = profit!==null ? (profit>=0?'+':'')+f2(profit) : '—';
    const marginStr  = margin!==null ? f2(margin,1)+'%' : '—';
    const profitCls  = profit!==null ? (profit>=0?'profit-pos':'profit-neg') : '';
    const marginCls  = margin!==null ? (margin>=0?'profit-pos':'profit-neg') : '';

    return `<tr>
      <td>
        <input class="ci-inp" value="${esc(r.channel)}" placeholder="輸入客戶名稱…" style="width:100%"
          onchange="priceChange(${r.id},'channel',this.value)">
      </td>
      <td class="mono tr" style="padding:6px 10px;font-weight:600;color:var(--gold)">
        $${f2(cost)}
      </td>
      <td style="padding:2px 4px">
        <div style="display:flex;align-items:center;gap:4px">
          <span style="font-size:12px;color:var(--ink3);padding-left:4px">$</span>
          <input class="ci-inp mono" type="number" value="${r.sellPrice||''}" placeholder="0"
            min="0" step="any" style="width:100px;font-weight:700;font-size:13px;text-align:right"
            oninput="priceChange(${r.id},'sellPrice',this.value);renderPriceTable(DB.prods.find(x=>x.id===activeProd))"
            onchange="priceChange(${r.id},'sellPrice',this.value)">
        </div>
      </td>
      <td class="mono tr" style="padding:6px 10px;font-size:14px;font-weight:700">
        <span class="${profitCls}">${profitStr}</span>
      </td>
      <td style="padding:6px 10px;text-align:right">
        <span class="mono ${marginCls}" style="font-size:13px;font-weight:700">${marginStr}</span>
      </td>
      <td style="text-align:center;padding:4px">
        <button class="btn-del" onclick="delPrice(${r.id})">✕</button>
      </td>
    </tr>`;
  }).join('');

  body.innerHTML=rows+`<tr class="add-trigger-row"><td colspan="6">
    <button class="add-trigger-btn" onclick="addPrice()">＋ 新增客戶</button></td></tr>`;
}

function esc(s){ return (s||'').replace(/"/g,'&quot;').replace(/'/g,'&#39;'); }

// ═══════════════════════════════════════════════════════
// ROW OPERATIONS
// ═══════════════════════════════════════════════════════
function addRow(type){
  const p=DB.prods.find(x=>x.id===activeProd); if(!p) return;
  const r={id:uid(),code:'',name:'',buyPrice:'',buyUnit:'',unitPrice:'',priceUnit:'',qty:'',qtyUnit:'',cost:0};
  p[type].push(r); saveDB();
  if(type==='ing') renderIngTable(p);
  else if(type==='pkg') renderPkgTable(p);
  else renderLabTable(p);
}
function addFee(){
  const p=DB.prods.find(x=>x.id===activeProd); if(!p) return;
  p.fee.push({id:uid(),name:'',cost:0,note:''});
  saveDB(); renderFeeTable(p);
}
function addPrice(){
  const p=DB.prods.find(x=>x.id===activeProd); if(!p) return;
  if(!p.prices) p.prices=[];
  p.prices.push({id:uid(),channel:'',sellPrice:''});
  saveDB(); renderPriceTable(p);
}

function rowChange(type,id,field,val){
  const p=DB.prods.find(x=>x.id===activeProd); if(!p) return;
  const r=p[type].find(x=>x.id===id); if(!r) return;
  r[field]=val; saveDB();
}
function feeChange(id,field,val){
  const p=DB.prods.find(x=>x.id===activeProd); if(!p) return;
  const r=p.fee.find(x=>x.id===id); if(!r) return;
  r[field]=val; if(field==='cost') recalc(); else saveDB();
}
function priceChange(id,field,val){
  const p=DB.prods.find(x=>x.id===activeProd); if(!p) return;
  const r=p.prices.find(x=>x.id===id); if(!r) return;
  r[field]=val;
  saveDB();
}
function recalcRow(type,id){
  const p=DB.prods.find(x=>x.id===activeProd); if(!p) return;
  const r=p[type].find(x=>x.id===id); if(!r) return;
  const up=parseFloat(document.querySelector(`#row-${type}-${id} input[type=number]:nth-of-type(2)`)||r.unitPrice)||parseFloat(r.unitPrice)||0;
  const qty=parseFloat(r.qty)||0;
  // re-read from inputs
  const tds=document.getElementById(`row-${type}-${id}`);
  if(tds){
    const inps=tds.querySelectorAll('input[type=number]');
    r.buyPrice=inps[0]?inps[0].value:'';
    r.unitPrice=inps[1]?inps[1].value:'';
    r.qty=inps[2]?inps[2].value:'';
  }
  const uPrice=parseFloat(r.unitPrice)||0;
  const uQty=parseFloat(r.qty)||0;
  r.cost=uPrice*uQty;
  const cel=document.getElementById(`cost-${type}-${id}`);
  if(cel) cel.textContent=r.cost>0?'$'+f2(r.cost):'';
  saveDB(); recalc();
}

function delRow(type,id){
  const p=DB.prods.find(x=>x.id===activeProd); if(!p) return;
  p[type]=p[type].filter(x=>x.id!==id);
  saveDB();
  if(type==='ing') renderIngTable(p);
  else if(type==='pkg') renderPkgTable(p);
  else renderLabTable(p);
  recalc();
}
function delFee(id){ const p=DB.prods.find(x=>x.id===activeProd); if(!p) return; p.fee=p.fee.filter(x=>x.id!==id); saveDB(); renderFeeTable(p); recalc(); }
function delPrice(id){ const p=DB.prods.find(x=>x.id===activeProd); if(!p) return; p.prices=p.prices.filter(x=>x.id!==id); saveDB(); renderPriceTable(p); }

// ═══════════════════════════════════════════════════════
// AUTOCOMPLETE ── 編碼欄 (精確/前綴優先)
// ═══════════════════════════════════════════════════════
function showCodeAC(type, rowId, q){
  const qL=q.toLowerCase().trim();
  const dd=document.getElementById(`code-dd-${type}-${rowId}`);
  if(!qL){dd.classList.remove('open');return;}
  const db=type==='ing'?DB.raw:type==='pkg'?DB.pkg:DB.lab;
  const hits=db.filter(m=>(m.code||'').toLowerCase().startsWith(qL)||(m.code||'').toLowerCase().includes(qL)||m.name.toLowerCase().includes(qL)).slice(0,8);
  if(!hits.length){dd.classList.remove('open');return;}
  dd.innerHTML=hits.map(m=>`<div class="ac-row" onmousedown="applyByCode('${type}',${rowId},${m.id})">
    <div class="ac-row-name" style="display:flex;align-items:center;gap:8px">
      <span class="mono" style="font-weight:700;color:var(--gold);font-size:11px;min-width:64px">${m.code||''}</span>
      <span>${m.name}</span>
    </div>
    <div class="ac-row-meta">$${f2(m.unitPrice,4)}/${m.priceUnit} · ${m.spec||''}</div>
  </div>`).join('');
  dd.classList.add('open');
}

function codeKey(e, type, rowId){
  const dd=document.getElementById(`code-dd-${type}-${rowId}`);
  const items=dd.querySelectorAll('.ac-row');
  let cur=[...items].findIndex(el=>el.classList.contains('hi'));
  if(e.key==='ArrowDown'){e.preventDefault();items.forEach(el=>el.classList.remove('hi'));cur=Math.min(cur+1,items.length-1);if(items[cur])items[cur].classList.add('hi');}
  else if(e.key==='ArrowUp'){e.preventDefault();items.forEach(el=>el.classList.remove('hi'));cur=Math.max(cur-1,0);if(items[cur])items[cur].classList.add('hi');}
  else if(e.key==='Enter'||e.key==='Tab'){
    const hi=dd.querySelector('.ac-row.hi');
    if(hi){e.preventDefault();hi.dispatchEvent(new Event('mousedown'));}
    else if(items.length===1){e.preventDefault();items[0].dispatchEvent(new Event('mousedown'));}
    else{
      const inp=document.getElementById(`code-inp-${type}-${rowId}`);
      const q=(inp?inp.value:'').trim().toUpperCase();
      const db=type==='ing'?DB.raw:type==='pkg'?DB.pkg:DB.lab;
      const exact=db.find(m=>(m.code||'').toUpperCase()===q);
      if(exact){e.preventDefault();applyByCode(type,rowId,exact.id);}
    }
  }
  else if(e.key==='Escape'){dd.classList.remove('open');}
}

function codeBlur(type, rowId){
  setTimeout(()=>{
    const dd=document.getElementById(`code-dd-${type}-${rowId}`);
    if(dd) dd.classList.remove('open');
    const inp=document.getElementById(`code-inp-${type}-${rowId}`);
    if(!inp) return;
    const q=inp.value.trim().toUpperCase();
    if(!q) return;
    const p=DB.prods.find(x=>x.id===activeProd); if(!p) return;
    const r=p[type].find(x=>x.id===rowId); if(!r) return;
    if(r.name) return;
    const db=type==='ing'?DB.raw:type==='pkg'?DB.pkg:DB.lab;
    const exact=db.find(m=>(m.code||'').toUpperCase()===q);
    if(exact) applyByCode(type,rowId,exact.id);
  },180);
}

function applyByCode(type, rowId, matId){
  const p=DB.prods.find(x=>x.id===activeProd); if(!p) return;
  const r=p[type].find(x=>x.id===rowId); if(!r) return;
  const db=type==='ing'?DB.raw:type==='pkg'?DB.pkg:DB.lab;
  const m=db.find(x=>x.id===matId); if(!m) return;
  r.code=m.code||''; r.name=m.name;
  r.buyPrice=m.buyPrice; r.buyUnit=m.buyUnit;
  r.unitPrice=m.unitPrice; r.priceUnit=m.priceUnit;
  r.qtyUnit=m.useUnit||m.priceUnit;
  r.qty=''; r.cost=0;
  saveDB();
  const tr=document.getElementById(`row-${type}-${rowId}`);
  if(tr){
    const tmp=document.createElement('tbody');
    tmp.innerHTML=makeRow(type,r,0);
    tr.parentNode.replaceChild(tmp.firstChild,tr);
  }
  const dd1=document.getElementById(`code-dd-${type}-${rowId}`);
  const dd2=document.getElementById(`ac-dd-${type}-${rowId}`);
  if(dd1) dd1.classList.remove('open');
  if(dd2) dd2.classList.remove('open');
  setTimeout(()=>{
    const qtyInp=document.getElementById(`qty-inp-${type}-${rowId}`);
    if(qtyInp){qtyInp.focus();qtyInp.select();}
  },40);
}

// ═══════════════════════════════════════════════════════
// AUTOCOMPLETE ── 品名欄 (模糊搜尋)
// ═══════════════════════════════════════════════════════
let _acTimer={};
function showAC(type, rowId, q){
  const qL=q.toLowerCase().trim();
  const dd=document.getElementById(`ac-dd-${type}-${rowId}`);
  if(!qL){dd.classList.remove('open');return;}
  const db=type==='ing'?DB.raw:type==='pkg'?DB.pkg:DB.lab;
  const hits=db.filter(m=>m.name.toLowerCase().includes(qL)||(m.code||'').toLowerCase().includes(qL)).slice(0,10);
  let html=hits.map(m=>`<div class="ac-row" onmousedown="applyAC('${type}',${rowId},${m.id})">
    <div class="ac-row-name">${m.name}</div>
    <div class="ac-row-meta">${m.code||''} | $${f2(m.unitPrice,4)}/${m.priceUnit}</div>
  </div>`).join('');
  html+=`<div class="ac-create" onmousedown="quickCreate('${type}','${q.replace(/'/g,"\\'")}')">＋ 「${q}」新增至資料庫並帶入</div>`;
  if(!hits.length) html=`<div style="padding:7px 10px;font-size:11px;color:var(--ink3)">找不到「${q}」</div>`+html;
  dd.innerHTML=html; dd.classList.add('open');
}

function applyAC(type, rowId, matId){
  const p=DB.prods.find(x=>x.id===activeProd); if(!p) return;
  const r=p[type].find(x=>x.id===rowId); if(!r) return;
  const db=type==='ing'?DB.raw:type==='pkg'?DB.pkg:DB.lab;
  const m=db.find(x=>x.id===matId); if(!m) return;
  // fill all fields
  r.code=m.code||''; r.name=m.name;
  r.buyPrice=m.buyPrice; r.buyUnit=m.buyUnit;
  r.unitPrice=m.unitPrice; r.priceUnit=m.priceUnit;
  r.qtyUnit=m.useUnit||m.priceUnit;
  r.qty=''; r.cost=0;
  saveDB();
  // re-render just this row
  const tr=document.getElementById(`row-${type}-${rowId}`);
  if(tr){
    const tmp=document.createElement('tbody');
    tmp.innerHTML=makeRow(type,r,0);
    tr.parentNode.replaceChild(tmp.firstChild,tr);
  }
  const dd1=document.getElementById(`code-dd-${type}-${rowId}`);
  const dd2=document.getElementById(`ac-dd-${type}-${rowId}`);
  if(dd1) dd1.classList.remove('open');
  if(dd2) dd2.classList.remove('open');
  // focus qty
  setTimeout(()=>{
    const qtyInp=document.getElementById(`qty-inp-${type}-${rowId}`);
    if(qtyInp){qtyInp.focus();qtyInp.select();}
  },40);
}

function acKey(e,type,rowId){
  const dd=document.getElementById(`ac-dd-${type}-${rowId}`);
  const items=dd.querySelectorAll('.ac-row');
  let cur=[...items].findIndex(el=>el.classList.contains('hi'));
  if(e.key==='ArrowDown'){e.preventDefault();items.forEach(el=>el.classList.remove('hi'));cur=Math.min(cur+1,items.length-1);if(items[cur])items[cur].classList.add('hi');}
  else if(e.key==='ArrowUp'){e.preventDefault();items.forEach(el=>el.classList.remove('hi'));cur=Math.max(cur-1,0);if(items[cur])items[cur].classList.add('hi');}
  else if(e.key==='Enter'){e.preventDefault();const hi=dd.querySelector('.ac-row.hi');if(hi)hi.dispatchEvent(new Event('mousedown'));}
  else if(e.key==='Escape'){dd.classList.remove('open');}
}
function delayHideAC(type,rowId){ setTimeout(()=>{ const dd=document.getElementById(`ac-dd-${type}-${rowId}`); if(dd) dd.classList.remove('open'); },200); }

// Close all dropdowns on outside click
document.addEventListener('click',e=>{
  document.querySelectorAll('.ac-dd.open').forEach(dd=>{
    if(!dd.contains(e.target)){
      const inp=dd.previousElementSibling||dd.parentElement.querySelector('input');
      if(inp&&inp!==e.target) dd.classList.remove('open');
    }
  });
});

function quickCreate(type,name){
  const dbType=type==='ing'?'raw':type==='pkg'?'pkg':'lab';
  openMatModal(dbType,null,name,type);
}

// ═══════════════════════════════════════════════════════
// PRODUCT CRUD
// ═══════════════════════════════════════════════════════
function openNewProd(){ openM('modal-new-prod'); ['np-name','np-spec','np-oq','np-p1','np-p2'].forEach(id=>document.getElementById(id).value=''); }
function createProd(){
  const name=document.getElementById('np-name').value.trim();
  if(!name){alert('請輸入品名');return;}
  const prices=[];
  const p1=parseFloat(document.getElementById('np-p1').value); if(p1>0) prices.push({id:uid(),channel:'客戶售價',price:p1});
  const p2=parseFloat(document.getElementById('np-p2').value); if(p2>0) prices.push({id:uid(),channel:'零售售價',price:p2});
  const p={id:uid(),name,spec:document.getElementById('np-spec').value,
    oq:parseFloat(document.getElementById('np-oq').value)||1,
    ou:document.getElementById('np-ou').value,
    ing:[],pkg:[],lab:[],fee:[],prices};
  DB.prods.push(p); saveDB(); CM('modal-new-prod'); loadProd(p.id); renderSidebar();
}
function deleteProd(){
  if(!activeProd||!confirm('確定刪除此產品？')) return;
  DB.prods=DB.prods.filter(p=>p.id!==activeProd);
  activeProd=null; saveDB(); renderSidebar();
  document.getElementById('no-prod').style.display='flex';
  document.getElementById('prod-editor').style.display='none';
}

// ═══════════════════════════════════════════════════════
// LIBRARY RENDERERS
// ═══════════════════════════════════════════════════════
function renderRawLib(){
  const q=(document.getElementById('raw-search').value||'').toLowerCase();
  const list=DB.raw.filter(m=>!q||m.name.toLowerCase().includes(q)||(m.code||'').toLowerCase().includes(q));
  document.getElementById('raw-count').textContent=`共 ${DB.raw.length} 筆食材原料`;
  document.getElementById('raw-tbody').innerHTML=list.map(m=>libRow(m,'raw')).join('');
}
function renderPkgLib(){
  const q=(document.getElementById('pkg-search').value||'').toLowerCase();
  const list=DB.pkg.filter(m=>!q||m.name.toLowerCase().includes(q)||(m.code||'').toLowerCase().includes(q));
  document.getElementById('pkg-count').textContent=`共 ${DB.pkg.length} 筆包材物料`;
  document.getElementById('pkg-tbody').innerHTML=list.map(m=>libRow(m,'pkg')).join('');
}
function libRow(m,dbType){
  return `<tr>
    <td><span class="ci mono muted" style="font-size:10px">${m.code||''}</span></td>
    <td><span class="ci bold">${m.name}</span></td>
    <td><span class="ci muted" style="font-size:11px">${m.spec||''}</span></td>
    <td><span class="ci mono tr">$${f2(m.buyPrice)}</span></td>
    <td><span class="ci muted">${m.buyUnit||''}</span></td>
    <td><span class="ci mono tr bold" style="color:var(--gold)">$${f2(m.unitPrice,4)}</span></td>
    <td><span class="ci muted">${m.priceUnit||''}</span></td>
    <td><span class="ci mono tr">${m.useQty||''}</span></td>
    <td><span class="ci muted">${m.useUnit||''}</span></td>
    <td><span class="ci muted" style="font-size:11px">${m.note||''}</span></td>
    <td><span class="ci muted" style="font-size:11px">${m.spec2||''}</span></td>
    <td style="display:flex;gap:4px;padding:5px">
      <button class="btn btn-ghost btn-sm" onclick="openMatModal('${dbType}',${m.id})">✏️</button>
      <button class="btn-del" onclick="deleteMat('${dbType}',${m.id})">✕</button>
    </td>
  </tr>`;
}
function renderLabLib(){
  document.getElementById('lab-lib-tbody').innerHTML=DB.lab.map(m=>`<tr>
    <td><span class="ci mono muted" style="font-size:10px">${m.code||''}</span></td>
    <td><span class="ci bold">${m.name}</span></td>
    <td><span class="ci muted" style="font-size:11px">${m.spec||''}</span></td>
    <td><span class="ci mono tr">$${f2(m.rate)}</span></td>
    <td><span class="ci muted">${m.rateUnit||''}</span></td>
    <td><span class="ci mono tr bold" style="color:var(--gold)">$${f2(m.unitPrice)}</span></td>
    <td><span class="ci muted">${m.priceUnit||''}</span></td>
    <td><span class="ci mono tr">${m.useQty||''}</span></td>
    <td><span class="ci muted">${m.useUnit||''}</span></td>
    <td><span class="ci muted" style="font-size:11px">${m.note||''}</span></td>
    <td style="display:flex;gap:4px;padding:5px">
      <button class="btn btn-ghost btn-sm" onclick="openLabModal(${m.id})">✏️</button>
      <button class="btn-del" onclick="deleteLab(${m.id})">✕</button>
    </td>
  </tr>`).join('');
}

// ═══════════════════════════════════════════════════════
// MAT MODAL
// ═══════════════════════════════════════════════════════
let _mmType='raw', _mmEdit=null, _mmBackType=null;
function openMatModal(dbType, id, prefillName, backType){
  _mmType=dbType; _mmEdit=id; _mmBackType=backType||null;
  const isLab=dbType==='lab';
  document.getElementById('mat-modal-title').textContent = id?'編輯':'新增 '+(dbType==='raw'?'食材':dbType==='pkg'?'包材':'工項');
  document.getElementById('mm-save-btn').textContent = id?'更新':'儲存';
  const fields=['mm-code','mm-name','mm-spec','mm-buyprice','mm-buyqty','mm-buyunit','mm-unitprice','mm-priceunit','mm-spec2','mm-note','mm-spec3'];
  fields.forEach(f=>document.getElementById(f).value='');
  document.getElementById('mm-hint').textContent='';
  if(id){
    const arr=dbType==='raw'?DB.raw:dbType==='pkg'?DB.pkg:DB.lab;
    const m=arr.find(x=>x.id===id); if(!m) return;
    document.getElementById('mm-code').value=m.code||'';
    document.getElementById('mm-name').value=m.name||'';
    document.getElementById('mm-spec').value=m.spec||'';
    document.getElementById('mm-buyprice').value=m.buyPrice||'';
    document.getElementById('mm-buyqty').value=m.buyQty||'';
    document.getElementById('mm-buyunit').value=m.buyUnit||'';
    document.getElementById('mm-unitprice').value=m.unitPrice||'';
    document.getElementById('mm-priceunit').value=m.priceUnit||'';
    document.getElementById('mm-spec2').value=m.spec2||m.buyQty||'';
    document.getElementById('mm-note').value=m.note||'';
    document.getElementById('mm-spec3').value=m.spec3||'';
  } else if(prefillName){
    document.getElementById('mm-name').value=prefillName;
  }
  openM('modal-mat');
}
function calcMM(){
  const bp=parseFloat(document.getElementById('mm-buyprice').value);
  const bq=parseFloat(document.getElementById('mm-buyqty').value);
  const pu=document.getElementById('mm-priceunit').value||'單位';
  if(bp>=0&&bq>0){
    const up=bp/bq;
    document.getElementById('mm-unitprice').value=f2(up,6);
    document.getElementById('mm-hint').textContent=`單位成本 = $${f2(up,6)} / ${pu}`;
  } else { document.getElementById('mm-hint').textContent=''; }
}
function calcMM2(){ document.getElementById('mm-hint').textContent=''; }
function saveMat(){
  const name=document.getElementById('mm-name').value.trim(); if(!name){alert('請輸入品名');return;}
  const obj={
    code:document.getElementById('mm-code').value.trim(),
    name,
    spec:document.getElementById('mm-spec').value.trim(),
    buyPrice:parseFloat(document.getElementById('mm-buyprice').value)||0,
    buyQty:parseFloat(document.getElementById('mm-buyqty').value)||1,
    buyUnit:document.getElementById('mm-buyunit').value.trim(),
    unitPrice:parseFloat(document.getElementById('mm-unitprice').value)||0,
    priceUnit:document.getElementById('mm-priceunit').value.trim(),
    spec2:document.getElementById('mm-spec2').value.trim(),
    note:document.getElementById('mm-note').value.trim(),
    spec3:document.getElementById('mm-spec3').value.trim(),
    useQty:'', useUnit:document.getElementById('mm-priceunit').value.trim(),
  };
  const arr=_mmType==='raw'?DB.raw:_mmType==='pkg'?DB.pkg:DB.lab;
  if(_mmEdit){
    const m=arr.find(x=>x.id===_mmEdit); if(m) Object.assign(m,obj);
  } else {
    obj.id=uid(); arr.push(obj);
    // if quick-create from product row, apply to current row
    if(_mmBackType){
      const p=DB.prods.find(x=>x.id===activeProd);
      if(p){
        const rowArr=_mmBackType==='ing'?p.ing:_mmBackType==='pkg'?p.pkg:p.lab;
        // find last empty row or add
        let emptyRow=rowArr.find(r=>!r.name);
        if(!emptyRow){emptyRow={id:uid(),code:'',name:'',buyPrice:'',buyUnit:'',unitPrice:'',priceUnit:'',qty:'',qtyUnit:'',cost:0};rowArr.push(emptyRow);}
        applyACObj(_mmBackType,emptyRow.id,obj.id,arr);
      }
    }
  }
  saveDB(); CM('modal-mat');
  if(_mmType==='raw') renderRawLib();
  else if(_mmType==='pkg') renderPkgLib();
  else renderLabLib();
}
function applyACObj(type,rowId,matId,arr){
  const p=DB.prods.find(x=>x.id===activeProd); if(!p) return;
  const r=p[type].find(x=>x.id===rowId); if(!r) return;
  const m=arr.find(x=>x.id===matId); if(!m) return;
  r.code=m.code||''; r.name=m.name;
  r.buyPrice=m.buyPrice; r.buyUnit=m.buyUnit;
  r.unitPrice=m.unitPrice; r.priceUnit=m.priceUnit;
  r.qtyUnit=m.useUnit||m.priceUnit; r.qty=''; r.cost=0;
  saveDB();
  if(type==='ing') renderIngTable(p);
  else if(type==='pkg') renderPkgTable(p);
  else renderLabTable(p);
}
function deleteMat(dbType,id){
  if(!confirm('確定刪除？')) return;
  if(dbType==='raw') DB.raw=DB.raw.filter(x=>x.id!==id);
  else DB.pkg=DB.pkg.filter(x=>x.id!==id);
  saveDB();
  if(dbType==='raw') renderRawLib(); else renderPkgLib();
}

// ═══════════════════════════════════════════════════════
// LAB MODAL
// ═══════════════════════════════════════════════════════
let _lmEdit=null;
function openLabModal(id){
  _lmEdit=id;
  document.getElementById('lab-modal-title').textContent=id?'編輯工項':'新增工項';
  document.getElementById('lm-save-btn').textContent=id?'更新':'儲存';
  ['lm-code','lm-name','lm-spec','lm-rate','lm-rateunit','lm-unitprice','lm-priceunit','lm-note'].forEach(f=>document.getElementById(f).value='');
  if(id){
    const m=DB.lab.find(x=>x.id===id); if(!m) return;
    document.getElementById('lm-code').value=m.code||'';
    document.getElementById('lm-name').value=m.name||'';
    document.getElementById('lm-spec').value=m.spec||'';
    document.getElementById('lm-rate').value=m.rate||'';
    document.getElementById('lm-rateunit').value=m.rateUnit||'';
    document.getElementById('lm-unitprice').value=m.unitPrice||'';
    document.getElementById('lm-priceunit').value=m.priceUnit||'';
    document.getElementById('lm-note').value=m.note||'';
  }
  openM('modal-lab');
}
function saveLab(){
  const name=document.getElementById('lm-name').value.trim(); if(!name){alert('請輸入工項名稱');return;}
  const rate=parseFloat(document.getElementById('lm-rate').value)||0;
  const obj={
    code:document.getElementById('lm-code').value.trim(), name,
    spec:document.getElementById('lm-spec').value.trim(),
    rate, rateUnit:document.getElementById('lm-rateunit').value.trim()||'1hr',
    unitPrice:parseFloat(document.getElementById('lm-unitprice').value)||rate,
    priceUnit:document.getElementById('lm-priceunit').value.trim()||'hr',
    useQty:'', useUnit:document.getElementById('lm-priceunit').value.trim()||'hr',
    note:document.getElementById('lm-note').value.trim(),
  };
  if(_lmEdit){ const m=DB.lab.find(x=>x.id===_lmEdit); if(m) Object.assign(m,obj); }
  else { obj.id=uid(); DB.lab.push(obj); }
  saveDB(); CM('modal-lab'); renderLabLib();
}
function deleteLab(id){ if(!confirm('確定刪除？')) return; DB.lab=DB.lab.filter(x=>x.id!==id); saveDB(); renderLabLib(); }

// ═══════════════════════════════════════════════════════
// NAV & UTILS
// ═══════════════════════════════════════════════════════
function showPage(id,btn){
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('on'));
  document.querySelectorAll('.nav-btn').forEach(b=>b.classList.remove('on'));
  document.getElementById(id).classList.add('on');
  btn.classList.add('on');
  if(id==='pg-raw') renderRawLib();
  if(id==='pg-pkg') renderPkgLib();
  if(id==='pg-lab') renderLabLib();
  if(id==='pg-db') renderDBPage();
}
function openM(id){ document.getElementById(id).classList.add('open'); }
function CM(id){ document.getElementById(id).classList.remove('open'); }

// ═══════════════════════════════════════════════════════
// DB MANAGEMENT PAGE
// ═══════════════════════════════════════════════════════
function renderDBPage(){
  // stats
  document.getElementById('db-cnt-raw').textContent=DB.raw.length;
  document.getElementById('db-cnt-pkg').textContent=DB.pkg.length;
  document.getElementById('db-cnt-lab').textContent=DB.lab.length;
  document.getElementById('db-cnt-prod').textContent=DB.prods.length;
  dbRenderRaw(); dbRenderPkg(); dbRenderLab(); dbRenderProd();
}

function dbSwitchTab(id,btn){
  ['dbt-raw','dbt-pkg','dbt-lab','dbt-prod'].forEach(t=>document.getElementById(t).style.display=t===id?'':'none');
  document.querySelectorAll('.db-tab').forEach(b=>b.classList.remove('on'));
  btn.classList.add('on');
}

function dbMatRow(m, dbType){
  return `<tr>
    <td><span class="ci mono" style="font-size:10px;font-weight:700;color:var(--gold)">${m.code||''}</span></td>
    <td><span class="ci bold">${m.name}</span></td>
    <td><span class="ci muted" style="font-size:11px">${m.spec||''}</span></td>
    <td><span class="ci mono tr">$${f2(m.buyPrice)}</span></td>
    <td><span class="ci muted">${m.buyUnit||''}</span></td>
    <td><span class="ci mono tr bold" style="color:var(--gold)">$${f2(m.unitPrice,5)}</span></td>
    <td><span class="ci muted">${m.priceUnit||''}</span></td>
    <td><span class="ci muted" style="font-size:11px">${m.note||''}</span></td>
    <td style="padding:4px 6px;display:flex;gap:4px">
      <button class="btn btn-ghost btn-sm" onclick="openMatModal('${dbType}',${m.id})">✏️</button>
      <button class="btn-del" onclick="dbDeleteMat('${dbType}',${m.id})">✕</button>
    </td>
  </tr>`;
}

function dbRenderRaw(){
  const q=(document.getElementById('db-raw-search')||{value:''}).value.toLowerCase();
  const list=DB.raw.filter(m=>!q||m.name.toLowerCase().includes(q)||(m.code||'').toLowerCase().includes(q));
  document.getElementById('db-raw-tbody').innerHTML=list.map(m=>dbMatRow(m,'raw')).join('')||'<tr><td colspan="9" style="padding:20px;text-align:center;color:var(--ink3)">尚無食材資料</td></tr>';
  document.getElementById('db-cnt-raw').textContent=DB.raw.length;
}
function dbRenderPkg(){
  const q=(document.getElementById('db-pkg-search')||{value:''}).value.toLowerCase();
  const list=DB.pkg.filter(m=>!q||m.name.toLowerCase().includes(q)||(m.code||'').toLowerCase().includes(q));
  document.getElementById('db-pkg-tbody').innerHTML=list.map(m=>dbMatRow(m,'pkg')).join('')||'<tr><td colspan="9" style="padding:20px;text-align:center;color:var(--ink3)">尚無包材資料</td></tr>';
  document.getElementById('db-cnt-pkg').textContent=DB.pkg.length;
}
function dbRenderLab(){
  document.getElementById('db-lab-tbody').innerHTML=DB.lab.map(m=>`<tr>
    <td><span class="ci mono" style="font-size:10px;font-weight:700;color:var(--gold)">${m.code||''}</span></td>
    <td><span class="ci bold">${m.name}</span></td>
    <td><span class="ci mono tr">$${f2(m.rate)}</span></td>
    <td><span class="ci muted">${m.rateUnit||''}</span></td>
    <td><span class="ci mono tr bold" style="color:var(--gold)">$${f2(m.unitPrice)}</span></td>
    <td><span class="ci muted">${m.priceUnit||''}</span></td>
    <td><span class="ci muted" style="font-size:11px">${m.note||''}</span></td>
    <td style="padding:4px 6px;display:flex;gap:4px">
      <button class="btn btn-ghost btn-sm" onclick="openLabModal(${m.id})">✏️</button>
      <button class="btn-del" onclick="dbDeleteLab(${m.id})">✕</button>
    </td>
  </tr>`).join('')||'<tr><td colspan="8" style="padding:20px;text-align:center;color:var(--ink3)">尚無人工資料</td></tr>';
  document.getElementById('db-cnt-lab').textContent=DB.lab.length;
}
function dbRenderProd(){
  const q=(document.getElementById('db-prod-search')||{value:''}).value.toLowerCase();
  const list=DB.prods.filter(p=>!q||p.name.toLowerCase().includes(q));
  document.getElementById('db-prod-tbody').innerHTML=list.map(p=>{
    const cost=prodTotal(p);
    return `<tr>
      <td><span class="ci bold">${p.name||''}</span></td>
      <td><span class="ci muted" style="font-size:11px">${p.spec||''}</span></td>
      <td><span class="ci mono tr">${p.oq||1}</span></td>
      <td><span class="ci muted">${p.ou||'包'}</span></td>
      <td><span class="ci mono tr bold" style="color:var(--gold)">$${f2(cost)}</span></td>
      <td><span class="ci tr muted">${p.ing.length}</span></td>
      <td><span class="ci tr muted">${p.pkg.length}</span></td>
      <td style="padding:4px 6px;display:flex;gap:4px">
        <button class="btn btn-gold btn-sm" onclick="goToProd(${p.id})">開啟</button>
        <button class="btn-del" onclick="dbDeleteProd(${p.id})">✕</button>
      </td>
    </tr>`;
  }).join('')||'<tr><td colspan="8" style="padding:20px;text-align:center;color:var(--ink3)">尚無產品資料</td></tr>';
  document.getElementById('db-cnt-prod').textContent=DB.prods.length;
}

function goToProd(id){
  // switch to product page and load it
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('on'));
  document.querySelectorAll('.nav-btn').forEach(b=>b.classList.remove('on'));
  document.getElementById('pg-prod').classList.add('on');
  document.querySelector('.nav-btn').classList.add('on');
  loadProd(id);
}

function dbDeleteMat(dbType,id){
  if(!confirm('確定刪除？')) return;
  if(dbType==='raw') DB.raw=DB.raw.filter(x=>x.id!==id);
  else DB.pkg=DB.pkg.filter(x=>x.id!==id);
  saveDB(); renderDBPage(); renderRawLib(); renderPkgLib();
}
function dbDeleteLab(id){ if(!confirm('確定刪除？')) return; DB.lab=DB.lab.filter(x=>x.id!==id); saveDB(); renderDBPage(); renderLabLib(); }
function dbDeleteProd(id){ if(!confirm('確定刪除此產品？')) return; DB.prods=DB.prods.filter(x=>x.id!==id); saveDB(); renderDBPage(); renderSidebar(); }

function dbClearConfirm(type){
  const label=type==='raw'?'所有食材原料':type==='pkg'?'所有包材物料':'所有人工費率';
  if(!confirm(`確定要清空${label}？此操作不可復原。`)) return;
  if(type==='raw') DB.raw=[]; else if(type==='pkg') DB.pkg=[]; else DB.lab=[];
  saveDB(); renderDBPage(); renderRawLib(); renderPkgLib(); renderLabLib();
}

function dbExportCSV(type){
  let csv='\uFEFF', fn='';
  if(type==='raw'){
    csv+='編碼,品名,包裝規格,進價(含稅),進貨單位,單價(含稅),單價單位,備註\n';
    DB.raw.forEach(m=>csv+=`${m.code||''},${m.name},${m.spec||''},${m.buyPrice||''},${m.buyUnit||''},${m.unitPrice||''},${m.priceUnit||''},${m.note||''}\n`);
    fn='食材原料庫';
  } else if(type==='pkg'){
    csv+='編碼,品名,包裝規格,進價(含稅),進貨單位,單價(含稅),單價單位,備註\n';
    DB.pkg.forEach(m=>csv+=`${m.code||''},${m.name},${m.spec||''},${m.buyPrice||''},${m.buyUnit||''},${m.unitPrice||''},${m.priceUnit||''},${m.note||''}\n`);
    fn='包材物料庫';
  } else if(type==='lab'){
    csv+='編碼,品名,時薪,時薪單位,單價(含稅),單價單位,備註\n';
    DB.lab.forEach(m=>csv+=`${m.code||''},${m.name},${m.rate||''},${m.rateUnit||''},${m.unitPrice||''},${m.priceUnit||''},${m.note||''}\n`);
    fn='人工費率';
  } else {
    csv+='品名,規格,每批產出,單位,每單位成本\n';
    DB.prods.forEach(p=>csv+=`${p.name},${p.spec||''},${p.oq||1},${p.ou||'包'},$${f2(prodTotal(p))}\n`);
    fn='產品列表';
  }
  const a=document.createElement('a'); a.href='data:text/csv;charset=utf-8,'+encodeURIComponent(csv);
  a.download=`${fn}_${new Date().toISOString().slice(0,10)}.csv`; a.click();
}

// ═══════════════════════════════════════════════════════
// PASTE IMPORT SYSTEM
// ═══════════════════════════════════════════════════════
let _pasteType='raw';  // 'raw' | 'pkg' | 'lab'
let _pasteRows=[];     // parsed rows
let _pasteCols=[];     // column headers detected

// Field definitions per type
const PASTE_FIELDS = {
  raw: ['編碼','品名','包裝規格','進價','進貨單位','單價','單價單位','備註'],
  pkg: ['編碼','品名','包裝規格','進價','進貨單位','單價','單價單位','備註'],
  lab: ['編碼','品名','包裝規格','時薪','時薪單位','單價','單價單位','備註'],
};
const PASTE_KEYWORDS = {
  '編碼':['編碼','code','id'],
  '品名':['品名','名稱','name','原料','食材','包材'],
  '包裝規格':['包裝','規格','spec','packaging'],
  '進價':['進價','採購價','buyprice','進貨價','price','含稅'],
  '進貨單位':['進貨單位','採購單位','buyunit','進貨'],
  '時薪':['時薪','薪資','rate','薪'],
  '時薪單位':['時薪單位','薪資單位'],
  '單價':['單價','unitprice','每單位'],
  '單價單位':['單價單位','priceunit','計算單位','用量單位'],
  '備註':['備註','note','remark','說明'],
};

function openPasteModal(type){
  _pasteType=type;
  _pasteRows=[]; _pasteCols=[];
  const typeLabel = type==='raw'?'食材原料':type==='pkg'?'包材物料':'人工費率';
  document.getElementById('paste-modal-type').textContent=typeLabel;
  document.getElementById('paste-textarea').value='';
  document.getElementById('paste-step2').style.display='none';
  document.getElementById('paste-step3').style.display='none';
  document.getElementById('paste-dup-opt').style.display='none';
  document.getElementById('paste-import-btn').style.display='none';
  document.getElementById('paste-result-msg').innerHTML='';
  openM('modal-paste');
  setTimeout(()=>document.getElementById('paste-textarea').focus(),100);
}

function clearPaste(){
  document.getElementById('paste-textarea').value='';
  document.getElementById('paste-step2').style.display='none';
  document.getElementById('paste-step3').style.display='none';
  document.getElementById('paste-dup-opt').style.display='none';
  document.getElementById('paste-import-btn').style.display='none';
  _pasteRows=[]; _pasteCols=[];
}

function parsePaste(){
  const raw=document.getElementById('paste-textarea').value.trim();
  if(!raw){ clearPaste(); return; }

  // Split into lines then cells (tab or comma delimited)
  const lines=raw.split(/\r?\n/).filter(l=>l.trim());
  if(!lines.length) return;

  // Detect delimiter: tabs preferred
  const delim = lines[0].includes('\t') ? '\t' : ',';

  // Parse all rows
  const allRows=lines.map(l=>l.split(delim).map(c=>c.trim().replace(/^["']|["']$/g,'')));
  const maxCols=Math.max(...allRows.map(r=>r.length));

  // Detect if first row is a header
  const firstRow=allRows[0];
  const isHeader=firstRow.some(c=>/編碼|品名|進價|單價|規格|time|code|name|price|spec/i.test(c));
  const dataRows=isHeader?allRows.slice(1):allRows;
  _pasteRows=dataRows.filter(r=>r.some(c=>c.length>0));

  // Auto-detect column mapping
  const fields=PASTE_FIELDS[_pasteType]||PASTE_FIELDS.raw;
  _pasteCols=[];
  for(let i=0;i<maxCols;i++){
    const headerCell=isHeader?firstRow[i]||'':'';
    let detected='(忽略)';
    for(const [field,kws] of Object.entries(PASTE_KEYWORDS)){
      if(fields.includes(field)&&kws.some(kw=>headerCell.toLowerCase().includes(kw))){
        detected=field; break;
      }
    }
    // If no header match, use position-based guess
    if(detected==='(忽略)'&&!isHeader&&i<fields.length) detected=fields[i];
    _pasteCols.push({col:i,header:headerCell||`第${i+1}欄`,detected});
  }

  // Render column mapper
  document.getElementById('paste-step2').style.display='flex';
  const mapHtml=_pasteCols.map((c,i)=>{
    const opts=[...fields,'(忽略)'].map(f=>`<option value="${f}"${c.detected===f?'selected':''}>${f}</option>`).join('');
    return `<div class="col-map-item">
      <label>${c.header}</label>
      <select id="col-sel-${i}" onchange="updateColMap(${i},this.value)">${opts}</select>
    </div>`;
  }).join('');
  document.getElementById('paste-col-map').innerHTML=mapHtml;

  renderPastePreview();
}

function updateColMap(idx,val){
  _pasteCols[idx].detected=val;
  renderPastePreview();
}

function renderPastePreview(){
  document.getElementById('paste-step3').style.display='flex';
  document.getElementById('paste-dup-opt').style.display='block';
  document.getElementById('paste-import-btn').style.display='inline-flex';

  const fields=PASTE_FIELDS[_pasteType]||PASTE_FIELDS.raw;
  // Build field→colIdx map
  const fieldMap={};
  _pasteCols.forEach((c,i)=>{ if(c.detected!=='(忽略)') fieldMap[c.detected]=i; });

  // header row
  const headCells=fields.map(f=>`<th>${f}</th>`).join('')+'<th>狀態</th>';
  document.getElementById('paste-preview-head').innerHTML=headCells;

  const db=_pasteType==='raw'?DB.raw:_pasteType==='pkg'?DB.pkg:DB.lab;
  let okCount=0, dupCount=0, errCount=0;

  const bodyHtml=_pasteRows.map(row=>{
    const get=f=>fieldMap[f]!==undefined?(row[fieldMap[f]]||''):'';
    const code=get('編碼'); const name=get('品名');
    if(!name&&!code){ return ''; } // skip blank rows
    const hasDup=!!(code&&db.find(m=>(m.code||'')===(code||'')));
    const isErr=!name;
    if(isErr) errCount++;
    else if(hasDup) dupCount++;
    else okCount++;

    const cells=fields.map(f=>{
      const v=get(f); return `<td>${v}</td>`;
    }).join('');
    const status=isErr?'<td style="color:var(--red)">⚠ 缺品名</td>':hasDup?'<td style="color:#7a5a00">⚠ 重複</td>':'<td style="color:var(--green)">✓</td>';
    return `<tr class="${isErr?'err':hasDup?'':'ok'}">${cells}${status}</tr>`;
  }).filter(Boolean).join('');

  document.getElementById('paste-preview-body').innerHTML=bodyHtml||'<tr><td colspan="10" style="padding:12px;text-align:center;color:var(--ink3)">無可匯入的資料</td></tr>';

  const total=okCount+dupCount;
  document.getElementById('paste-preview-count').textContent=`共 ${total} 筆（新增 ${okCount} 筆，重複 ${dupCount} 筆，錯誤 ${errCount} 筆）`;

  const msgEl=document.getElementById('paste-result-msg');
  if(errCount>0) msgEl.innerHTML=`<div class="import-result warn">⚠ 有 ${errCount} 筆因缺少品名無法匯入，其餘 ${total} 筆可以匯入</div>`;
  else if(dupCount>0) msgEl.innerHTML=`<div class="import-result warn">⚠ 發現 ${dupCount} 筆重複編碼，請選擇下方處理方式</div>`;
  else if(okCount>0) msgEl.innerHTML=`<div class="import-result ok">✓ ${okCount} 筆資料準備就緒，確認後點「匯入」</div>`;
  else msgEl.innerHTML=`<div class="import-result err">✗ 無有效資料可匯入</div>`;
}

function executePasteImport(){
  const fields=PASTE_FIELDS[_pasteType]||PASTE_FIELDS.raw;
  const fieldMap={};
  _pasteCols.forEach((c,i)=>{ if(c.detected!=='(忽略)') fieldMap[c.detected]=i; });
  const get=(row,f)=>fieldMap[f]!==undefined?(row[fieldMap[f]]||''):'';

  const dupMode=document.querySelector('input[name="dup-mode"]:checked')?.value||'skip';
  const db=_pasteType==='raw'?DB.raw:_pasteType==='pkg'?DB.pkg:DB.lab;

  let imported=0, skipped=0, overwritten=0;

  _pasteRows.forEach(row=>{
    const code=get(row,'編碼').trim();
    const name=get(row,'品名').trim();
    if(!name) return; // skip invalid

    const buyPrice=parseFloat(get(row,'進價').replace(/[,$＄]/g,''))||0;
    const buyUnit=get(row,'進貨單位')||'包';
    const unitPrice=parseFloat(get(row,'單價').replace(/[,$＄]/g,''))||0;
    const priceUnit=get(row,'單價單位')||get(row,'用量單位')||'g';
    const rate=parseFloat(get(row,'時薪').replace(/[,$＄]/g,''))||0;
    const rateUnit=get(row,'時薪單位')||'hr';
    const spec=get(row,'包裝規格')||'';
    const note=get(row,'備註')||'';

    const existIdx=code?db.findIndex(m=>(m.code||'')===(code)):-1;

    if(existIdx>=0){
      if(dupMode==='skip'){ skipped++; return; }
      if(dupMode==='overwrite'){
        if(_pasteType==='lab'){
          Object.assign(db[existIdx],{name,spec,rate,rateUnit:rateUnit||'1hr',unitPrice:unitPrice||rate,priceUnit:priceUnit||'hr',note,useUnit:priceUnit||'hr'});
        } else {
          Object.assign(db[existIdx],{name,spec,buyPrice,buyUnit,unitPrice,priceUnit,note,useUnit:priceUnit,buyQty:buyPrice>0&&unitPrice>0?buyPrice/unitPrice:1});
        }
        overwritten++; return;
      }
      // 'both': fall through to add
    }

    // new record
    if(_pasteType==='lab'){
      db.push({id:uid(),code,name,spec,rate,rateUnit:rateUnit||'1hr',unitPrice:unitPrice||rate,priceUnit:priceUnit||'hr',useQty:'',useUnit:priceUnit||'hr',note});
    } else {
      const bq=buyPrice>0&&unitPrice>0?(buyPrice/unitPrice):1;
      db.push({id:uid(),code,name,spec,buyPrice,buyQty:bq,buyUnit,unitPrice,priceUnit,useQty:'',useUnit:priceUnit,note,spec2:''});
    }
    imported++;
  });

  saveDB();
  CM('modal-paste');
  renderDBPage();
  renderRawLib(); renderPkgLib(); renderLabLib();

  const msg=`✅ 匯入完成！新增 ${imported} 筆${overwritten?`、更新 ${overwritten} 筆`:''}${skipped?`、略過 ${skipped} 筆`:''}`;
  setTimeout(()=>alert(msg),100);
}

// ─── EXPORT EXCEL ───
function exportExcel(){
  if(typeof XLSX === 'undefined'){ alert('Excel 程式庫尚未載入，請確認網路連線後重試'); return; }

  const wb = XLSX.utils.book_new();
  const date = new Date().toLocaleDateString('zh-TW');

  // ── 樣式輔助 (XLSX不支援完整樣式，用欄寬+粗體已是上限)
  const ao = (v, t='s') => ({ v, t });

  // ── 共用：標題列底色用 !cols 控制欄寬
  const COL_GOLD = { fgColor:{ rgb:'8A6500' } };

  /* ─── Sheet 1: 原料資料庫 ─── */
  const rawHeader = ['編碼','品名','包裝規格','進價(含稅)','進貨單位','單價(含稅)','單價單位','備註'];
  const rawRows = DB.raw.map(m=>[
    m.code||'', m.name||'', m.spec||'',
    m.buyPrice||'', m.buyUnit||'',
    m.unitPrice||'', m.priceUnit||'',
    m.note||''
  ]);
  const rawSheet = XLSX.utils.aoa_to_sheet([rawHeader, ...rawRows]);
  rawSheet['!cols'] = [12,22,18,12,10,12,10,16].map(w=>({wch:w}));
  XLSX.utils.book_append_sheet(wb, rawSheet, '原料資料庫');

  /* ─── Sheet 2: 包材物料庫 ─── */
  const pkgHeader = ['編碼','品名','包裝規格','進價(含稅)','進貨單位','單價(含稅)','單價單位','備註'];
  const pkgRows = DB.pkg.map(m=>[
    m.code||'', m.name||'', m.spec||'',
    m.buyPrice||'', m.buyUnit||'',
    m.unitPrice||'', m.priceUnit||'',
    m.note||''
  ]);
  const pkgSheet = XLSX.utils.aoa_to_sheet([pkgHeader, ...pkgRows]);
  pkgSheet['!cols'] = [12,22,18,12,10,12,10,16].map(w=>({wch:w}));
  XLSX.utils.book_append_sheet(wb, pkgSheet, '包材物料庫');

  /* ─── Sheet 3: 人工費率 ─── */
  const labHeader = ['編碼','品名','包裝規格','時薪','時薪單位','單價(含稅)','單價單位','備註'];
  const labRows = DB.lab.map(m=>[
    m.code||'', m.name||'', m.spec||'',
    m.rate||'', m.rateUnit||'',
    m.unitPrice||'', m.priceUnit||'',
    m.note||''
  ]);
  const labSheet = XLSX.utils.aoa_to_sheet([labHeader, ...labRows]);
  labSheet['!cols'] = [10,20,10,8,8,10,8,16].map(w=>({wch:w}));
  XLSX.utils.book_append_sheet(wb, labSheet, '人工費率');

  /* ─── 每個產品一個 Sheet ─── */
  DB.prods.forEach(p => {
    const oq = parseFloat(p.oq)||1;
    const ou = p.ou||'包';
    const sumArr = arr => arr.reduce((s,r)=>s+(parseFloat(r.cost)||0),0);
    const ingTotal = sumArr(p.ing);
    const pkgTotal = sumArr(p.bao||p.pkg||[]);  // support both field names
    const labTotal = sumArr(p.lab);
    const feeTotal = sumArr(p.fee);
    const grandTotal = (ingTotal+pkgTotal+labTotal+feeTotal)/oq;

    const rows = [];

    // 產品基本資料
    rows.push(['產品名稱', p.name||'']);
    rows.push(['規格', p.spec||'']);
    rows.push(['每批產出', oq, ou]);
    rows.push(['日期', date]);
    rows.push([]);

    // ① 食材原料
    rows.push(['① 食材原料成本']);
    rows.push(['編碼','品名','進價(含稅)','進貨單位','單價(含稅)','單價單位','用量','用量單位','製造成本']);
    p.ing.forEach(r => rows.push([
      r.code||'', r.name||'',
      r.buyPrice!==''?Number(r.buyPrice):'',
      r.buyUnit||'',
      r.unitPrice!==''?Number(r.unitPrice):'',
      r.priceUnit||'',
      r.qty!==''?Number(r.qty):'',
      r.qtyUnit||'',
      parseFloat(r.cost)||0
    ]));
    rows.push(['','','','','','','','食材小計', ingTotal/oq]);
    rows.push([]);

    // ② 包材物料
    rows.push(['② 包材物料成本']);
    rows.push(['編碼','品名','進價(含稅)','進貨單位','單價(含稅)','單價單位','用量','用量單位','製造成本']);
    const pkgArr = p.bao||p.pkg||[];
    pkgArr.forEach(r => rows.push([
      r.code||'', r.name||'',
      r.buyPrice!==''?Number(r.buyPrice):'',
      r.buyUnit||'',
      r.unitPrice!==''?Number(r.unitPrice):'',
      r.priceUnit||'',
      r.qty!==''?Number(r.qty):'',
      r.qtyUnit||'',
      parseFloat(r.cost)||0
    ]));
    rows.push(['','','','','','','','包材小計', pkgTotal/oq]);
    rows.push([]);

    // ③ 人工費
    rows.push(['③ 人工費']);
    rows.push(['編碼','工項名稱','時薪','時薪單位','單價(含稅)','單價單位','用量','用量單位','製造成本']);
    p.lab.forEach(r => rows.push([
      r.code||'', r.name||'',
      r.buyPrice!==''?Number(r.buyPrice):'',
      r.buyUnit||'',
      r.unitPrice!==''?Number(r.unitPrice):'',
      r.priceUnit||'',
      r.qty!==''?Number(r.qty):'',
      r.qtyUnit||'',
      parseFloat(r.cost)||0
    ]));
    rows.push(['','','','','','','','人工小計', labTotal/oq]);
    rows.push([]);

    // ④ 管銷費用
    rows.push(['④ 管銷費用攤提']);
    rows.push(['費用項目','金額','備註']);
    p.fee.forEach(r => rows.push([r.name||'', parseFloat(r.cost)||0, r.note||'']));
    rows.push(['管銷小計', feeTotal/oq]);
    rows.push([]);

    // 成本合計
    rows.push(['⑤ 每'+ou+'成本總計']);
    rows.push(['料｜食材', ingTotal/oq]);
    rows.push(['料｜包材', pkgTotal/oq]);
    rows.push(['工｜人工', labTotal/oq]);
    rows.push(['費｜管銷', feeTotal/oq]);
    rows.push(['每'+ou+'總成本', grandTotal]);
    rows.push([]);

    // ⑥ 客戶定價
    if(p.prices && p.prices.length){
      rows.push(['⑥ 客戶定價']);
      rows.push(['客戶名稱','產品成本','末端售價','毛利','毛利率']);
      p.prices.forEach(r => {
        const sp = parseFloat(r.sellPrice)||0;
        const profit = sp>0 ? sp-grandTotal : '';
        const margin = sp>0 ? (profit/sp)*100 : '';
        rows.push([
          r.channel||'',
          grandTotal,
          sp||'',
          profit!==''?profit:'',
          margin!==''?margin/100:''
        ]);
      });
    }

    const ws = XLSX.utils.aoa_to_sheet(rows);
    ws['!cols'] = [14,22,12,10,12,10,10,10,12].map(w=>({wch:w}));

    // 格式化百分比欄（客戶定價的毛利率）
    const sheetName = (p.name||'產品').substring(0,28).replace(/[:\\/\*\?\[\]]/g,'_');
    XLSX.utils.book_append_sheet(wb, ws, sheetName);
  });

  /* ─── 匯出 ─── */
  const filename = `食品成本系統_${date.replace(/\//g,'-')}.xlsx`;
  XLSX.writeFile(wb, filename);
}

// ─── EXPORT JSON ───
function exportCSV(){
  const p=DB.prods.find(x=>x.id===activeProd); if(!p) return;
  const oq=parseFloat(p.oq)||1; const ou=p.ou||'包';
  const per=prodTotal(p);
  let csv=`\uFEFF食品成本計算系統\n品名：${p.name}\n規格：${p.spec||'—'}\n日期：${new Date().toLocaleDateString('zh-TW')}\n\n`;
  csv+=`=== 食材原料成本 ===\n編碼,品名,進價(含稅),進貨單位,單價(含稅),單價單位,用量,用量單位,製造成本\n`;
  p.ing.forEach(r=>csv+=`${r.code||''},${r.name||''},${r.buyPrice||''},${r.buyUnit||''},${r.unitPrice||''},${r.priceUnit||''},${r.qty||''},${r.qtyUnit||''},$${f2(parseFloat(r.cost)||0)}\n`);
  csv+=`\n=== 包材物料成本 ===\n編碼,品名,進價(含稅),進貨單位,單價(含稅),單價單位,用量,用量單位,製造成本\n`;
  p.pkg.forEach(r=>csv+=`${r.code||''},${r.name||''},${r.buyPrice||''},${r.buyUnit||''},${r.unitPrice||''},${r.priceUnit||''},${r.qty||''},${r.qtyUnit||''},$${f2(parseFloat(r.cost)||0)}\n`);
  csv+=`\n=== 人工費 ===\n編碼,工項名稱,時薪,時薪單位,單價(含稅),單價單位,用量,用量單位,製造成本\n`;
  p.lab.forEach(r=>csv+=`${r.code||''},${r.name||''},${r.buyPrice||''},${r.buyUnit||''},${r.unitPrice||''},${r.priceUnit||''},${r.qty||''},${r.qtyUnit||''},$${f2(parseFloat(r.cost)||0)}\n`);
  csv+=`\n=== 管銷費用 ===\n費用項目,金額,備註\n`;
  p.fee.forEach(r=>csv+=`${r.name||''},$${f2(parseFloat(r.cost)||0)},${r.note||''}\n`);
  csv+=`\n=== 每${ou}總成本 ===\n食材,$${f2(p.ing.reduce((a,r)=>a+(parseFloat(r.cost)||0),0)/oq)}\n包材,$${f2(p.pkg.reduce((a,r)=>a+(parseFloat(r.cost)||0),0)/oq)}\n人工,$${f2(p.lab.reduce((a,r)=>a+(parseFloat(r.cost)||0),0)/oq)}\n管銷,$${f2(p.fee.reduce((a,r)=>a+(parseFloat(r.cost)||0),0)/oq)}\n總成本,$${f2(per)}\n`;
  if(p.prices&&p.prices.length){
    csv+=`\n=== 客戶定價 ===\n客戶名稱,產品成本,末端售價,毛利,毛利率\n`;
    p.prices.forEach(r=>{
      const sp=parseFloat(r.sellPrice)||0;
      const profit=sp>0?sp-per:null;
      const margin=sp>0?(profit/sp)*100:null;
      csv+=`${r.channel||''},$${f2(per)},${sp>0?'$'+f2(sp):'—'},${profit!==null?(profit>=0?'+':'')+f2(profit):'—'},${margin!==null?f2(margin,1)+'%':'—'}\n`;
    });
  }
  const a=document.createElement('a'); a.href='data:text/csv;charset=utf-8,'+encodeURIComponent(csv);
  a.download=`成本_${p.name}_${new Date().toISOString().slice(0,10)}.csv`; a.click();
}
function exportJSON(){
  const b=new Blob([JSON.stringify(DB,null,2)],{type:'application/json'});
  const a=document.createElement('a'); a.href=URL.createObjectURL(b);
  a.download=`backup_${new Date().toISOString().slice(0,10)}.json`; a.click();
}
function importJSON(inp){
  const f=inp.files[0]; if(!f) return;
  const r=new FileReader();
  r.onload=e=>{try{Object.assign(DB,JSON.parse(e.target.result));saveDB();location.reload();}catch{alert('匯入失敗');}};
  r.readAsText(f);
}

// ═══════════════════════════════════════════════════════
// NATURAL LANGUAGE IMPORT
// ═══════════════════════════════════════════════════════
let _nlType = 'ing';       // which table we're importing to
let _nlParsed = [];        // parsed + matched items from AI

function openNLImport(type){
  _nlType = type;
  _nlParsed = [];
  document.getElementById('nl-input').value = '';
  document.getElementById('nl-result-wrap').style.display = 'none';
  document.getElementById('nl-thinking').style.display = 'none';
  document.getElementById('nl-import-btn').style.display = 'none';
  document.getElementById('nl-api-status').textContent = '';
  openM('modal-nl');
  setTimeout(()=>document.getElementById('nl-input').focus(), 100);
}

async function runNLParse(){
  const text = document.getElementById('nl-input').value.trim();
  if(!text){ alert('請先輸入食材清單'); return; }

  document.getElementById('nl-thinking').style.display = 'block';
  document.getElementById('nl-result-wrap').style.display = 'none';
  document.getElementById('nl-parse-btn').disabled = true;
  document.getElementById('nl-import-btn').style.display = 'none';
  document.getElementById('nl-api-status').textContent = '';

  // Build DB name list for context
  const dbArr = _nlType === 'ing' ? DB.raw : DB.pkg;
  const dbNames = dbArr.map(m => `${m.code||''}|${m.name}|${m.priceUnit}`).join('\n');

  const prompt = `你是一個食品原料資料解析助手。請解析以下食材清單，每行一項，輸出 JSON 陣列。

食材清單：
${text}

資料庫現有品項（格式：編碼|品名|單位）：
${dbNames || '（目前無資料）'}

請將每行解析為：
- name: 辨識出的品名（繁體中文，修正錯別字，例如「塩」→「鹽」、「麥片絲」→「小麥肉片」）
- qty: 數量（數字，例如 200）
- unit: 單位（例如 斤、兩、g、公斤、個、包）
- note: 括號內的備註（如果有）
- dbMatch: 資料庫中最相近的品名（完全一樣的品名優先，否則找最接近的，無則填 null）
- matchType: "exact"=完全符合, "fuzzy"=模糊相近, "none"=找不到

注意：
- 「兩」= 37.5g，「斤」= 600g（台制）
- 數量可能是 "x4" 這種格式，代表乘以4，請計算出總量
- 只輸出 JSON 陣列，不要其他文字

輸出範例：
[{"name":"杏鮑菇","qty":200,"unit":"斤","note":"","dbMatch":"杏鮑菇(B級)","matchType":"fuzzy"},{"name":"鹽","qty":44,"unit":"兩","note":"","dbMatch":"高級精鹽","matchType":"fuzzy"}]`;

  try {
    const resp = await fetch('https://api.anthropic.com/v1/messages', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        model: 'claude-sonnet-4-20250514',
        max_tokens: 1000,
        messages: [{ role: 'user', content: prompt }]
      })
    });
    const data = await resp.json();
    const raw = data.content?.map(c=>c.text||'').join('').trim();
    // Strip markdown code fences if present
    const jsonStr = raw.replace(/^```(?:json)?\s*/,'').replace(/\s*```$/,'').trim();
    const parsed = JSON.parse(jsonStr);
    _nlParsed = parsed;
    renderNLResult(parsed, dbArr);
  } catch(err) {
    document.getElementById('nl-api-status').textContent = '⚠ 解析失敗，請檢查網路或重試';
    console.error(err);
  } finally {
    document.getElementById('nl-thinking').style.display = 'none';
    document.getElementById('nl-parse-btn').disabled = false;
  }
}

function renderNLResult(items, dbArr){
  document.getElementById('nl-result-wrap').style.display = 'block';

  let matchCount = 0, fuzzyCount = 0, newCount = 0;

  const html = items.map((item, idx) => {
    // find actual DB record
    let dbRecord = null;
    if(item.dbMatch){
      dbRecord = dbArr.find(m => m.name === item.dbMatch);
      if(!dbRecord) dbRecord = dbArr.find(m => m.name.includes(item.dbMatch) || item.dbMatch.includes(m.name));
    }

    const type = item.matchType === 'exact' ? 'match' :
                 item.matchType === 'fuzzy' ? 'fuzzy' : 'new';
    if(type==='match') matchCount++;
    else if(type==='fuzzy') fuzzyCount++;
    else newCount++;

    const typeLabel = type==='match'?'完全比對':type==='fuzzy'?'模糊比對':'新品項';

    // calc cost preview
    let costStr = '—';
    if(dbRecord && item.qty){
      // unit conversion
      let qtyInDBUnit = item.qty;
      const fromUnit = item.unit;
      const toUnit = dbRecord.priceUnit;
      // common conversions
      const toG = {
        '兩': 37.5, '公兩': 37.5,
        '斤': 600, '台斤': 600,
        '公斤': 1000, 'kg': 1000,
        'g': 1, 'G': 1,
        '公克': 1,
      };
      if(toUnit === 'g' && toG[fromUnit]){
        qtyInDBUnit = item.qty * toG[fromUnit];
      } else if(fromUnit === toUnit){
        qtyInDBUnit = item.qty;
      }
      const cost = dbRecord.unitPrice * qtyInDBUnit;
      if(isFinite(cost)) costStr = '$' + f2(cost);
    }

    const matchedName = dbRecord ? dbRecord.name : (item.dbMatch || '—');
    const unitConvNote = (item.unit !== (dbRecord?.priceUnit||item.unit)) ? `<span style="font-size:10px;color:var(--ink4)">${item.qty}${item.unit} → 換算中</span>` : '';

    return `<div class="nl-result-row" id="nl-row-${idx}">
      <span class="nl-badge ${type}">${typeLabel}</span>
      <div style="flex:1;min-width:0">
        <div style="display:flex;align-items:center;gap:6px;flex-wrap:wrap">
          <span class="nl-name">${item.name}</span>
          ${item.note?`<span style="font-size:10px;color:var(--ink3)">(${item.note})</span>`:''}
          ${type!=='match'&&matchedName!=='—'?`<span style="font-size:10px;color:var(--ink3)">→ 比對為：<strong>${matchedName}</strong></span>`:''}
        </div>
        ${unitConvNote}
      </div>
      <span class="nl-qty">${item.qty} ${item.unit}</span>
      <span class="nl-cost">${costStr}</span>
      <label style="font-size:11px;color:var(--ink3);display:flex;align-items:center;gap:4px;cursor:pointer;flex-shrink:0">
        <input type="checkbox" id="nl-chk-${idx}" ${type!=='none'||dbRecord?'checked':''} style="cursor:pointer">
        加入
      </label>
    </div>`;
  }).join('');

  document.getElementById('nl-result-list').innerHTML = html;
  document.getElementById('nl-result-summary').textContent =
    `共 ${items.length} 項 — 完全比對 ${matchCount} 項、模糊比對 ${fuzzyCount} 項、新品項 ${newCount} 項`;
  document.getElementById('nl-import-btn').style.display = 'inline-flex';
}

function executeNLImport(){
  const p = DB.prods.find(x=>x.id===activeProd);
  if(!p){ alert('請先選擇產品'); return; }
  const dbArr = _nlType === 'ing' ? DB.raw : DB.pkg;
  let added = 0, skipped = 0;

  _nlParsed.forEach((item, idx) => {
    const chk = document.getElementById(`nl-chk-${idx}`);
    if(!chk || !chk.checked){ skipped++; return; }

    // find DB record (same logic as renderNLResult)
    let dbRecord = null;
    if(item.dbMatch){
      dbRecord = dbArr.find(m => m.name === item.dbMatch);
      if(!dbRecord) dbRecord = dbArr.find(m => m.name.includes(item.dbMatch) || item.dbMatch.includes(m.name));
    }

    // unit conversion
    const toG = {
      '兩':37.5,'公兩':37.5,'斤':600,'台斤':600,
      '公斤':1000,'kg':1000,'g':1,'G':1,'公克':1
    };
    let qtyInDBUnit = item.qty;
    if(dbRecord && dbRecord.priceUnit==='g' && toG[item.unit]){
      qtyInDBUnit = item.qty * toG[item.unit];
    }

    let rowCost = 0;
    if(dbRecord) rowCost = dbRecord.unitPrice * qtyInDBUnit;

    const row = {
      id: uid(),
      code: dbRecord?.code || '',
      name: dbRecord?.name || item.name,
      buyPrice: dbRecord?.buyPrice || '',
      buyUnit: dbRecord?.buyUnit || '',
      unitPrice: dbRecord?.unitPrice || '',
      priceUnit: dbRecord?.priceUnit || item.unit,
      qty: qtyInDBUnit,
      qtyUnit: dbRecord?.priceUnit || item.unit,
      cost: rowCost,
      note: item.note || ''
    };

    p[_nlType].push(row);
    added++;
  });

  saveDB();
  CM('modal-nl');

  if(_nlType === 'ing') renderIngTable(p);
  else renderPkgTable(p);
  recalc();

  setTimeout(()=>alert(`✅ 已加入 ${added} 項${skipped?`，略過 ${skipped} 項`:''}！`), 80);
}

// ─── INIT ───
loadDB();
seedIfEmpty();
renderSidebar();
if(DB.prods.length) loadProd(DB.prods[0].id);
</script>
</body>
</html>
