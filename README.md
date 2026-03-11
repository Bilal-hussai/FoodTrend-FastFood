<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
<title>FoodTrend Fastfood</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@700;900&family=DM+Sans:wght@300;400;500;600;700&display=swap" rel="stylesheet">
<style>
:root{
  --cream:#FDF6EC;--brown:#5C3D2E;--brown-l:#8B6355;
  --or:#E8821A;--or-s:#F5A623;--white:#FFFFFF;
  --text:#2C1810;--ts:#9E7B6A;--sh:rgba(92,61,46,0.12);
  --green:#25D366;--red:#E53E3E;
}
*{margin:0;padding:0;box-sizing:border-box;-webkit-tap-highlight-color:transparent;}
html{scroll-behavior:smooth;}
body{background:var(--cream);color:var(--text);font-family:'DM Sans',sans-serif;min-height:100vh;overflow-x:hidden;}

/* ── PAGES ── */
.pg{display:none;opacity:0;transition:opacity .3s;}
.pg.on{opacity:1;}
#pg-login{flex-direction:column;align-items:center;justify-content:center;min-height:100vh;padding:32px 20px;position:relative;overflow:hidden;background:var(--cream);}
#pg-login.on{display:flex;}
#pg-main.on,#pg-checkout.on{display:block;}

/* blobs */
.blob{position:absolute;border-radius:50%;filter:blur(60px);opacity:.4;pointer-events:none;}
.b1{width:280px;height:280px;background:radial-gradient(circle,#F5A623,#E8821A);top:-80px;right:-60px;animation:bfloat 6s ease-in-out infinite;}
.b2{width:200px;height:200px;background:radial-gradient(circle,#F5DEB3,#DEB887);bottom:40px;left:-60px;animation:bfloat 8s ease-in-out infinite reverse;}
@keyframes bfloat{0%,100%{transform:translate(0,0) scale(1);}50%{transform:translate(12px,-18px) scale(1.05);}}

/* ── LOGIN ── */
.login-card{background:var(--white);border-radius:32px;padding:44px 28px;width:100%;max-width:400px;box-shadow:0 20px 60px rgba(92,61,46,.15);position:relative;z-index:2;animation:cardIn .7s cubic-bezier(.34,1.56,.64,1);}
@keyframes cardIn{from{opacity:0;transform:translateY(40px) scale(.95);}to{opacity:1;transform:translateY(0) scale(1);}}
.l-logo{text-align:center;margin-bottom:28px;}
.l-icon{width:70px;height:70px;background:linear-gradient(135deg,var(--or),var(--or-s));border-radius:22px;margin:0 auto 14px;display:flex;align-items:center;justify-content:center;font-size:2rem;box-shadow:0 8px 24px rgba(232,130,26,.35);}
.l-logo h1{font-family:'Playfair Display',serif;font-size:1.9rem;color:var(--brown);}
.l-logo p{color:var(--ts);font-size:.85rem;margin-top:3px;}
.btn-google{width:100%;display:flex;align-items:center;justify-content:center;gap:12px;padding:14px 20px;background:var(--white);border:2px solid #EDE0D4;border-radius:16px;font-family:'DM Sans',sans-serif;font-size:.95rem;font-weight:600;color:var(--text);cursor:pointer;transition:all .25s;box-shadow:0 2px 8px var(--sh);margin-bottom:14px;}
.btn-google:hover{border-color:var(--or);box-shadow:0 4px 20px rgba(232,130,26,.2);transform:translateY(-1px);}
.gsvg{width:22px;height:22px;flex-shrink:0;}
.divider{display:flex;align-items:center;gap:12px;margin:18px 0;}
.divider::before,.divider::after{content:'';flex:1;height:1px;background:#EDE0D4;}
.divider span{color:var(--ts);font-size:.8rem;}
.inp-grp{margin-bottom:14px;}
.inp-lbl{display:block;font-size:.8rem;font-weight:600;color:var(--brown-l);margin-bottom:6px;letter-spacing:.4px;}
.gw{position:relative;}
.gw::after{content:'';position:absolute;inset:-2px;border-radius:16px;background:linear-gradient(135deg,var(--or),var(--or-s),#F5C57A);opacity:0;transition:opacity .35s;z-index:0;filter:blur(8px);pointer-events:none;}
.gw:focus-within::after{opacity:.55;}
.gi{position:relative;z-index:1;width:100%;padding:13px 16px;background:var(--white);border:2px solid #EDE0D4;border-radius:14px;font-family:'DM Sans',sans-serif;font-size:.95rem;color:var(--text);outline:none;transition:border-color .3s,box-shadow .3s;}
.gi:focus{border-color:var(--or);box-shadow:0 0 0 4px rgba(232,130,26,.1),0 4px 16px rgba(232,130,26,.12);}
.gi::placeholder{color:#C4A898;}
.btn-si{width:100%;padding:15px;background:linear-gradient(135deg,var(--or),var(--or-s));color:white;border:none;border-radius:16px;font-family:'DM Sans',sans-serif;font-size:1rem;font-weight:700;cursor:pointer;box-shadow:0 8px 24px rgba(232,130,26,.35);transition:all .25s;margin-top:8px;}
.btn-si:hover{transform:translateY(-2px);}
.l-foot{text-align:center;margin-top:20px;font-size:.82rem;color:var(--ts);}
.l-foot a{color:var(--or);font-weight:600;cursor:pointer;}

/* ── TICKER ── */
.ticker{background:var(--brown);padding:7px 0;overflow:hidden;white-space:nowrap;}
.t-inner{display:inline-block;animation:tick 24s linear infinite;font-size:.75rem;letter-spacing:1.5px;color:var(--or-s);font-weight:600;}
@keyframes tick{0%{transform:translateX(0);}100%{transform:translateX(-50%);}}

/* ── TOPBAR ── */
.topbar{padding:14px 16px 0;display:flex;align-items:center;justify-content:space-between;position:sticky;top:0;background:rgba(253,246,236,.95);backdrop-filter:blur(10px);z-index:50;}
.t-logo{font-family:'Playfair Display',serif;font-size:1.4rem;font-weight:900;color:var(--brown);}
.t-logo span{color:var(--or);}
.t-right{display:flex;align-items:center;gap:8px;}
.icon-btn{position:relative;background:var(--white);border:none;border-radius:14px;width:42px;height:42px;display:flex;align-items:center;justify-content:center;cursor:pointer;box-shadow:0 2px 10px var(--sh);transition:transform .2s,box-shadow .2s;}
.icon-btn:active{transform:scale(.9);}
.icon-btn:hover{box-shadow:0 4px 16px var(--sh);}
.icon-btn svg{width:20px;height:20px;stroke:var(--brown);fill:none;stroke-width:2;stroke-linecap:round;stroke-linejoin:round;}
.cart-badge{position:absolute;top:-5px;right:-5px;background:var(--red);color:white;border-radius:50%;width:18px;height:18px;font-size:.62rem;font-weight:700;display:none;align-items:center;justify-content:center;border:2px solid var(--cream);}
.cart-badge.show{display:flex;}
.avatar-btn{width:38px;height:38px;background:linear-gradient(135deg,var(--or),var(--or-s));border-radius:50%;display:flex;align-items:center;justify-content:center;color:white;font-weight:700;font-size:.9rem;border:none;cursor:pointer;box-shadow:0 3px 10px rgba(232,130,26,.3);}

/* ── HERO ── */
.hero{margin:14px 16px;background:linear-gradient(135deg,var(--brown) 0%,#7A4E3B 100%);border-radius:26px;padding:24px 20px;position:relative;overflow:hidden;min-height:158px;display:flex;flex-direction:column;justify-content:center;}
.hero::before{content:'';position:absolute;width:200px;height:200px;background:radial-gradient(circle,rgba(245,166,35,.28),transparent 70%);top:-40px;right:-40px;border-radius:50%;}
.hero::after{content:'';position:absolute;width:120px;height:120px;background:radial-gradient(circle,rgba(255,255,255,.06),transparent 70%);bottom:-20px;left:20px;border-radius:50%;}
.hero-food{position:absolute;right:-6px;bottom:-6px;font-size:6.8rem;transform:rotate(-12deg);filter:drop-shadow(0 8px 16px rgba(0,0,0,.25));pointer-events:none;line-height:1;animation:heroFloat 4s ease-in-out infinite;}
@keyframes heroFloat{0%,100%{transform:rotate(-12deg) translateY(0);}50%{transform:rotate(-10deg) translateY(-6px);}}
.h-badge{background:rgba(255,255,255,.15);color:var(--or-s);font-size:.68rem;font-weight:700;letter-spacing:2px;padding:4px 12px;border-radius:50px;display:inline-block;margin-bottom:10px;backdrop-filter:blur(6px);border:1px solid rgba(255,255,255,.15);}
.hero h2{font-family:'Playfair Display',serif;font-size:1.7rem;color:white;line-height:1.15;max-width:178px;}
.hero h2 span{color:var(--or-s);}
.hero p{color:rgba(255,255,255,.6);font-size:.78rem;margin-top:8px;}

/* ── SEARCH + SUGGESTIONS ── */
.srch-wrap{margin:14px 16px 6px;position:relative;z-index:40;}
.srch-glow{position:absolute;inset:-3px;border-radius:22px;background:linear-gradient(135deg,var(--or),var(--or-s));filter:blur(10px);opacity:0;transition:opacity .4s;pointer-events:none;}
.srch-wrap:focus-within .srch-glow{opacity:.4;}
.srch-inner{position:relative;background:var(--white);border-radius:18px;display:flex;align-items:center;padding:12px 16px;gap:10px;box-shadow:0 4px 20px var(--sh);border:2px solid transparent;transition:border-color .3s;z-index:1;}
.srch-wrap:focus-within .srch-inner{border-color:rgba(232,130,26,.3);}
.srch-inner input{flex:1;border:none;outline:none;font-family:'DM Sans',sans-serif;font-size:.9rem;color:var(--text);background:transparent;}
.srch-inner input::placeholder{color:#C4A898;}
.srch-inner svg{width:18px;height:18px;stroke:var(--ts);fill:none;stroke-width:2.2;stroke-linecap:round;flex-shrink:0;}
.srch-clear{background:none;border:none;cursor:pointer;display:none;padding:2px;border-radius:50%;color:var(--ts);}
.srch-clear svg{width:16px;height:16px;stroke:var(--ts);}
/* suggestions dropdown */
.suggestions{position:absolute;top:calc(100% + 6px);left:0;right:0;background:var(--white);border-radius:16px;box-shadow:0 8px 30px rgba(92,61,46,.15);overflow:hidden;z-index:45;max-height:260px;overflow-y:auto;display:none;animation:dropIn .2s ease;}
@keyframes dropIn{from{opacity:0;transform:translateY(-8px);}to{opacity:1;transform:translateY(0);}}
.suggestions.open{display:block;}
.sug-item{display:flex;align-items:center;gap:12px;padding:12px 16px;cursor:pointer;transition:background .18s;border-bottom:1px solid #F5ECD7;}
.sug-item:last-child{border:none;}
.sug-item:hover,.sug-item:active{background:#FFF8EC;}
.sug-em{font-size:1.5rem;flex-shrink:0;}
.sug-info{flex:1;}
.sug-name{font-size:.88rem;font-weight:600;color:var(--brown);}
.sug-cat{font-size:.72rem;color:var(--ts);}
.sug-price{font-family:'Playfair Display',serif;font-weight:700;font-size:.9rem;color:var(--or);}
.sug-add{background:linear-gradient(135deg,var(--or),var(--or-s));border:none;color:white;width:28px;height:28px;border-radius:50%;font-size:1.1rem;cursor:pointer;display:flex;align-items:center;justify-content:center;flex-shrink:0;font-weight:700;box-shadow:0 2px 8px rgba(232,130,26,.35);}

/* ── SEC LABEL ── */
.sec-lbl{font-family:'Playfair Display',serif;font-size:1.05rem;font-weight:700;color:var(--brown);padding:0 16px;margin-bottom:10px;display:flex;align-items:center;gap:8px;}
.sec-lbl::after{content:'';flex:1;height:1px;background:linear-gradient(to right,rgba(92,61,46,.12),transparent);margin-left:4px;}

/* ── CATS ── */
.cats{display:flex;gap:10px;padding:0 16px 2px;overflow-x:auto;scrollbar-width:none;margin-bottom:18px;scroll-snap-type:x mandatory;}
.cats::-webkit-scrollbar{display:none;}
.cat{display:flex;align-items:center;gap:6px;padding:9px 16px;border-radius:50px;font-size:.82rem;font-weight:600;white-space:nowrap;cursor:pointer;transition:all .25s;border:2px solid transparent;flex-shrink:0;scroll-snap-align:start;}
.cat svg{width:15px;height:15px;fill:none;stroke:currentColor;stroke-width:2;stroke-linecap:round;}
.cat.on{background:linear-gradient(135deg,var(--or),var(--or-s));color:white;box-shadow:0 4px 14px rgba(232,130,26,.3);}
.cat:not(.on){background:var(--white);color:var(--ts);box-shadow:0 2px 8px var(--sh);}
.cat:not(.on):hover{border-color:var(--or);color:var(--or);}

/* ── MENU GRID ── */
.mgrid{display:grid;grid-template-columns:repeat(3,1fr);gap:10px;padding:0 16px;margin-bottom:22px;}
/* slide-in animation for grid items */
.mc{background:var(--white);border-radius:20px;padding:14px 10px 30px;text-align:center;box-shadow:0 3px 16px var(--sh);cursor:pointer;transition:all .28s cubic-bezier(.34,1.1,.64,1);position:relative;overflow:hidden;border:2px solid transparent;opacity:0;transform:translateY(18px);}
.mc.vis{opacity:1;transform:translateY(0);}
.mc:active{transform:scale(.95);}
.mc:hover{box-shadow:0 10px 28px rgba(232,130,26,.18);border-color:rgba(232,130,26,.3);}
.mc.pop{animation:mcPop .35s cubic-bezier(.34,1.56,.64,1);}
@keyframes mcPop{0%,100%{transform:scale(1);}50%{transform:scale(1.07);}}
.mc-em{font-size:2.2rem;display:block;margin-bottom:5px;filter:drop-shadow(0 3px 6px rgba(0,0,0,.1));}
.mc-name{font-size:.7rem;font-weight:600;color:var(--ts);margin-bottom:5px;line-height:1.3;}
.mc-price{font-family:'Playfair Display',serif;font-size:.95rem;font-weight:700;color:var(--brown);}
.mc-add{position:absolute;bottom:7px;right:7px;width:26px;height:26px;background:linear-gradient(135deg,var(--or),var(--or-s));color:white;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:1.2rem;font-weight:700;cursor:pointer;box-shadow:0 3px 8px rgba(232,130,26,.4);transition:transform .2s;border:none;line-height:1;}
.mc-add:active{transform:scale(.82);}

/* ── DEALS ── */
.deals{padding:0 16px;margin-bottom:22px;}
.deal-row{background:var(--white);border-radius:20px;padding:16px 14px;display:flex;align-items:center;gap:12px;box-shadow:0 3px 16px var(--sh);margin-bottom:10px;cursor:pointer;transition:all .28s;position:relative;overflow:hidden;opacity:0;transform:translateX(-16px);}
.deal-row.vis{opacity:1;transform:translateX(0);}
.deal-row::before{content:'';position:absolute;left:0;top:0;bottom:0;width:4px;background:linear-gradient(to bottom,var(--or),var(--or-s));}
.deal-row:active{transform:scale(.98);}
.dr-icon{font-size:2.2rem;flex-shrink:0;}
.dr-info{flex:1;}
.dr-name{font-weight:700;font-size:.9rem;color:var(--brown);}
.dr-desc{font-size:.72rem;color:var(--ts);margin-top:2px;}
.dr-price{font-family:'Playfair Display',serif;font-weight:700;font-size:1.1rem;color:var(--or);text-align:right;flex-shrink:0;}
.dr-sub{font-size:.65rem;color:var(--ts);text-align:right;}
.dr-add-btn{flex-shrink:0;width:32px;height:32px;background:linear-gradient(135deg,var(--or),var(--or-s));border:none;border-radius:50%;color:white;font-size:1.2rem;font-weight:700;cursor:pointer;box-shadow:0 3px 10px rgba(232,130,26,.4);display:flex;align-items:center;justify-content:center;transition:transform .2s;}
.dr-add-btn:active{transform:scale(.82);}

/* ── SIZES ── */
.szscroll{display:flex;gap:10px;padding:0 16px 6px;overflow-x:auto;scrollbar-width:none;margin-bottom:22px;scroll-snap-type:x mandatory;}
.szscroll::-webkit-scrollbar{display:none;}
.szc{background:var(--white);border-radius:18px;padding:14px 12px;text-align:center;box-shadow:0 3px 16px var(--sh);flex-shrink:0;width:108px;cursor:pointer;transition:all .25s;border:2px solid transparent;scroll-snap-align:start;opacity:0;transform:translateY(12px);}
.szc.vis{opacity:1;transform:translateY(0);}
.szc:hover,.szc.picked{border-color:var(--or);transform:translateY(-3px);box-shadow:0 8px 24px rgba(232,130,26,.18);}
.sz-em{font-size:1.9rem;display:block;margin-bottom:5px;}
.sz-nm{font-weight:700;font-size:.82rem;color:var(--brown);}
.sz-in{font-size:.68rem;color:var(--ts);margin-bottom:7px;}
.sz-pr{font-family:'Playfair Display',serif;font-size:.95rem;font-weight:700;color:var(--or);}
.sz-tp{font-size:.62rem;color:#BBB;margin-top:3px;}

/* ── FLAVOURS ── */
.flavsec{padding:0 16px;margin-bottom:26px;}
.flavscroll{display:flex;gap:10px;overflow-x:auto;scrollbar-width:none;padding-bottom:6px;scroll-snap-type:x mandatory;}
.flavscroll::-webkit-scrollbar{display:none;}
.flav{background:var(--white);border:2px solid #EDE0D4;border-radius:16px;padding:12px 12px;text-align:center;flex-shrink:0;min-width:90px;cursor:pointer;transition:all .25s;scroll-snap-align:start;}
.flav:hover,.flav.sel{border-color:var(--or);background:rgba(232,130,26,.05);transform:translateY(-2px);box-shadow:0 6px 16px rgba(232,130,26,.14);}
.flav.special{min-width:158px;border-color:rgba(232,130,26,.35);background:linear-gradient(135deg,rgba(232,130,26,.06),rgba(245,166,35,.04));}
.fl-em{font-size:1.5rem;display:block;margin-bottom:4px;}
.fl-nm{font-size:.72rem;font-weight:700;color:var(--brown);}
.fl-sub{font-size:.65rem;color:var(--ts);margin-top:2px;}

/* ── BOTTOM NAV ── */
.bnav{position:fixed;bottom:0;left:50%;transform:translateX(-50%);width:100%;max-width:480px;background:rgba(255,255,255,.96);backdrop-filter:blur(12px);border-top:1px solid rgba(92,61,46,.08);padding:10px 0 calc(10px + env(safe-area-inset-bottom));display:flex;justify-content:space-around;box-shadow:0 -6px 24px rgba(92,61,46,.07);z-index:100;}
.ni{display:flex;flex-direction:column;align-items:center;gap:3px;cursor:pointer;padding:5px 20px;border-radius:14px;transition:background .2s;position:relative;}
.ni.on .ni-icon-wrap{background:rgba(232,130,26,.12);}
.ni.on .ni-lbl{color:var(--or);font-weight:700;}
.ni.on .ni-svg{stroke:var(--or);}
.ni-icon-wrap{width:36px;height:36px;border-radius:12px;display:flex;align-items:center;justify-content:center;transition:background .2s;}
.ni-svg{width:20px;height:20px;stroke:#C4A898;fill:none;stroke-width:2;stroke-linecap:round;stroke-linejoin:round;transition:stroke .2s;}
.ni-lbl{font-size:.62rem;color:#C4A898;font-weight:500;transition:color .2s;}
.ni-badge{position:absolute;top:2px;right:12px;background:var(--red);color:white;border-radius:50%;width:16px;height:16px;font-size:.58rem;font-weight:700;display:none;align-items:center;justify-content:center;border:2px solid rgba(255,255,255,.9);}
.ni-badge.show{display:flex;}

/* ── CART PANEL ── */
.cart-overlay{position:fixed;inset:0;background:rgba(0,0,0,.45);z-index:200;opacity:0;pointer-events:none;transition:opacity .3s;backdrop-filter:blur(2px);}
.cart-overlay.open{opacity:1;pointer-events:all;}
.cart-panel{position:fixed;top:0;right:0;bottom:0;width:88%;max-width:360px;background:var(--white);z-index:201;transform:translateX(100%);transition:transform .32s cubic-bezier(.4,0,.2,1);display:flex;flex-direction:column;border-radius:20px 0 0 20px;overflow:hidden;box-shadow:-8px 0 40px rgba(92,61,46,.15);}
.cart-panel.open{transform:translateX(0);}
.cp-head{padding:20px 16px 14px;background:var(--white);border-bottom:1px solid #F0E6DA;display:flex;align-items:center;justify-content:space-between;flex-shrink:0;}
.cp-title{font-family:'Playfair Display',serif;font-size:1.2rem;font-weight:700;color:var(--brown);}
.cp-title span{font-size:.82rem;color:var(--ts);font-family:'DM Sans',sans-serif;font-weight:400;margin-left:4px;}
.cp-close{background:var(--cream);border:none;border-radius:50%;width:34px;height:34px;cursor:pointer;display:flex;align-items:center;justify-content:center;transition:background .2s;}
.cp-close svg{width:16px;height:16px;stroke:var(--brown);fill:none;stroke-width:2.5;}
.cp-close:hover{background:#F0E6DA;}
.cp-body{flex:1;overflow-y:auto;padding:12px 16px;-webkit-overflow-scrolling:touch;}
.cp-empty{text-align:center;padding:50px 20px;}
.cp-empty .em-ico{font-size:3.5rem;display:block;margin-bottom:12px;}
.cp-empty p{color:var(--ts);font-size:.9rem;margin-bottom:20px;}
.btn-browse{background:linear-gradient(135deg,var(--or),var(--or-s));color:white;border:none;padding:12px 28px;border-radius:50px;font-family:'DM Sans',sans-serif;font-weight:700;cursor:pointer;font-size:.9rem;}
.cart-item{display:flex;align-items:center;gap:10px;padding:12px 0;border-bottom:1px solid #F5ECD7;animation:itemIn .3s ease;}
@keyframes itemIn{from{opacity:0;transform:translateX(10px);}to{opacity:1;transform:translateX(0);}}
.ci-em{font-size:2rem;flex-shrink:0;}
.ci-info{flex:1;}
.ci-name{font-weight:700;font-size:.88rem;color:var(--brown);}
.ci-price{font-family:'Playfair Display',serif;font-size:.85rem;color:var(--or);margin-top:2px;}
.qty-ctrl{display:flex;align-items:center;gap:8px;flex-shrink:0;}
.qbtn{width:28px;height:28px;border-radius:50%;border:2px solid #EDE0D4;background:var(--white);font-size:1rem;font-weight:700;cursor:pointer;display:flex;align-items:center;justify-content:center;color:var(--brown);transition:all .2s;}
.qbtn:hover{border-color:var(--or);color:var(--or);}
.qnum{font-weight:700;font-size:.95rem;min-width:18px;text-align:center;color:var(--brown);}
.cp-foot{padding:14px 16px 20px;background:var(--white);border-top:1px solid #F0E6DA;flex-shrink:0;}
.cp-row{display:flex;justify-content:space-between;font-size:.85rem;color:var(--ts);margin-bottom:6px;}
.delivery-note{background:#FFF8EC;border:1px dashed var(--or-s);border-radius:10px;padding:8px 10px;margin:8px 0;font-size:.72rem;color:var(--brown);line-height:1.6;}
.cp-total{display:flex;justify-content:space-between;font-family:'Playfair Display',serif;font-size:1.1rem;font-weight:700;color:var(--brown);padding-top:8px;border-top:2px dashed #EDE0D4;}
.cp-total span:last-child{color:var(--or);}
.btn-checkout{width:100%;padding:15px;background:linear-gradient(135deg,var(--or),var(--or-s));color:white;border:none;border-radius:16px;font-family:'DM Sans',sans-serif;font-size:1rem;font-weight:700;cursor:pointer;box-shadow:0 8px 24px rgba(232,130,26,.35);transition:all .25s;margin-top:14px;display:flex;align-items:center;justify-content:center;gap:8px;}
.btn-checkout svg{width:18px;height:18px;stroke:white;fill:none;stroke-width:2.2;}
.btn-checkout:hover{transform:translateY(-2px);box-shadow:0 12px 30px rgba(232,130,26,.45);}

/* ── CHECKOUT ── */
#pg-checkout{background:var(--cream);min-height:100vh;padding-bottom:30px;max-width:480px;margin:0 auto;}
.co-head{padding:16px 16px 0;display:flex;align-items:center;gap:12px;margin-bottom:4px;}
.back-btn{background:var(--white);border:none;border-radius:14px;width:42px;height:42px;display:flex;align-items:center;justify-content:center;cursor:pointer;box-shadow:0 2px 10px var(--sh);transition:transform .2s;}
.back-btn svg{width:20px;height:20px;stroke:var(--brown);fill:none;stroke-width:2.5;}
.back-btn:active{transform:scale(.9);}
.co-head h2{font-family:'Playfair Display',serif;font-size:1.3rem;color:var(--brown);}
.co-summary{margin:14px 16px 0;background:var(--white);border-radius:22px;padding:20px 16px;box-shadow:0 3px 16px var(--sh);}
.co-sum-title{font-family:'Playfair Display',serif;font-weight:700;font-size:1rem;color:var(--brown);margin-bottom:12px;display:flex;align-items:center;gap:6px;}
.co-item-row{display:flex;justify-content:space-between;align-items:center;padding:7px 0;border-bottom:1px solid #F5ECD7;font-size:.85rem;}
.co-item-row:last-of-type{border:none;}
.co-iname{color:var(--text);}
.co-iqty{color:var(--ts);font-size:.78rem;}
.co-iprice{font-family:'Playfair Display',serif;font-weight:700;color:var(--or);}
.co-total-row{display:flex;justify-content:space-between;margin-top:12px;padding-top:12px;border-top:2px dashed #EDE0D4;}
.co-total-row span:first-child{font-weight:700;color:var(--brown);}
.co-total-row span:last-child{font-family:'Playfair Display',serif;font-size:1.2rem;font-weight:700;color:var(--or);}
.co-dlv-note{background:#FFF8EC;border:1px dashed var(--or-s);border-radius:12px;padding:11px 13px;margin-top:12px;font-size:.78rem;color:var(--brown);line-height:1.7;}
.co-form{margin:14px 16px 0;background:var(--white);border-radius:22px;padding:20px 16px;box-shadow:0 3px 16px var(--sh);}
.co-form-title{font-family:'Playfair Display',serif;font-weight:700;font-size:1rem;color:var(--brown);margin-bottom:16px;display:flex;align-items:center;gap:6px;}
.f-grp{margin-bottom:14px;}
.f-lbl{display:block;font-size:.8rem;font-weight:600;color:var(--brown-l);margin-bottom:6px;letter-spacing:.4px;}
.f-inp,.f-ta{width:100%;padding:13px 16px;background:var(--cream);border:2px solid #EDE0D4;border-radius:14px;font-family:'DM Sans',sans-serif;font-size:.92rem;color:var(--text);outline:none;transition:border-color .3s,box-shadow .3s,background .3s;resize:none;}
.f-inp:focus,.f-ta:focus{border-color:var(--or);box-shadow:0 0 0 4px rgba(232,130,26,.1);background:var(--white);}
.f-inp::placeholder,.f-ta::placeholder{color:#C4A898;}
.f-inp.err,.f-ta.err{border-color:var(--red);animation:shake .4s ease;}
@keyframes shake{0%,100%{transform:translateX(0);}25%{transform:translateX(-6px);}75%{transform:translateX(6px);}}
.btn-confirm{display:flex;align-items:center;justify-content:center;gap:10px;width:calc(100% - 32px);margin:20px 16px 0;padding:17px;background:linear-gradient(135deg,#25D366,#1da851);color:white;border:none;border-radius:18px;font-family:'DM Sans',sans-serif;font-size:1.05rem;font-weight:700;cursor:pointer;box-shadow:0 10px 28px rgba(37,211,102,.35);transition:all .25s;}
.btn-confirm svg{width:22px;height:22px;fill:white;}
.btn-confirm:hover{transform:translateY(-2px);box-shadow:0 14px 36px rgba(37,211,102,.45);}

/* ── TOAST ── */
.toast{position:fixed;bottom:88px;left:50%;transform:translateX(-50%) translateY(20px);background:var(--brown);color:white;padding:11px 22px;border-radius:50px;font-size:.82rem;font-weight:600;z-index:999;opacity:0;transition:all .35s;pointer-events:none;white-space:nowrap;max-width:90vw;box-shadow:0 6px 20px rgba(92,61,46,.3);}
.toast.show{opacity:1;transform:translateX(-50%) translateY(0);}

/* ── FLOAT WA ── */
.fwa{position:fixed;bottom:80px;right:16px;background:var(--green);color:white;width:52px;height:52px;border-radius:50%;display:none;align-items:center;justify-content:center;box-shadow:0 6px 20px rgba(37,211,102,.45);text-decoration:none;z-index:150;animation:fbounce 3s ease-in-out infinite;transition:transform .2s;}
.fwa:active{transform:scale(.9);}
.fwa svg{width:26px;height:26px;fill:white;}
@keyframes fbounce{0%,100%{transform:translateY(0);}50%{transform:translateY(-6px);}}

/* main wrapper */
#pg-main{max-width:480px;margin:0 auto;padding-bottom:82px;}

/* scroll reveal base */
.reveal{opacity:0;transform:translateY(18px);transition:opacity .45s ease,transform .45s ease;}
.reveal.vis{opacity:1;transform:translateY(0);}
</style>
</head>
<body>

<!-- ══ LOGIN PAGE ══ -->
<div id="pg-login" class="pg on">
  <div class="blob b1"></div>
  <div class="blob b2"></div>
  <div class="login-card">
    <div class="l-logo">
      <div class="l-icon">🍕</div>
      <h1>FoodTrend</h1>
      <p>Haq's Bakers • Food Trends</p>
    </div>
    <button class="btn-google" id="gBtn">
      <svg class="gsvg" viewBox="0 0 24 24"><path fill="#4285F4" d="M22.56 12.25c0-.78-.07-1.53-.2-2.25H12v4.26h5.92c-.26 1.37-1.04 2.53-2.21 3.31v2.77h3.57c2.08-1.92 3.28-4.74 3.28-8.09z"/><path fill="#34A853" d="M12 23c2.97 0 5.46-.98 7.28-2.66l-3.57-2.77c-.98.66-2.23 1.06-3.71 1.06-2.86 0-5.29-1.93-6.16-4.53H2.18v2.84C3.99 20.53 7.7 23 12 23z"/><path fill="#FBBC05" d="M5.84 14.09c-.22-.66-.35-1.36-.35-2.09s.13-1.43.35-2.09V7.07H2.18C1.43 8.55 1 10.22 1 12s.43 3.45 1.18 4.93l2.85-2.22.81-.62z"/><path fill="#EA4335" d="M12 5.38c1.62 0 3.06.56 4.21 1.64l3.15-3.15C17.45 2.09 14.97 1 12 1 7.7 1 3.99 3.47 2.18 7.07l3.66 2.84c.87-2.6 3.3-4.53 6.16-4.53z"/></svg>
      Continue with Google
    </button>
    <div class="divider"><span>ya email se login karo</span></div>
    <div class="inp-grp">
      <label class="inp-lbl">Email Address</label>
      <div class="gw"><input type="email" class="gi" placeholder="you@example.com"></div>
    </div>
    <div class="inp-grp">
      <label class="inp-lbl">Password</label>
      <div class="gw"><input type="password" class="gi" placeholder="••••••••"></div>
    </div>
    <button class="btn-si" id="signInBtn">Sign In →</button>
    <div class="l-foot">Account nahi? <a id="signUpLink">Sign Up Free</a></div>
  </div>
</div>

<!-- ══ MAIN PAGE ══ -->
<div id="pg-main" class="pg">
  <div class="ticker">
    <div class="t-inner">🍕 PIZZA DEALS • 🍔 ZINGER BURGER Rs.280 • 🌯 SHAWARMA Rs.170 • 🔥 HOT &amp; SPICY PIZZA • ⭐ HAQS SPECIAL • 🧀 CHEESE LOVER • 🥩 SEEKH KABAB • 🍕 PIZZA DEALS • 🍔 ZINGER BURGER Rs.280 • 🌯 SHAWARMA Rs.170 • 🔥 HOT &amp; SPICY PIZZA • ⭐ HAQS SPECIAL • 🧀 CHEESE LOVER • 🥩 SEEKH KABAB •&nbsp;</div>
  </div>

  <div class="topbar">
    <div class="t-logo">Food<span>Trend</span></div>
    <div class="t-right">
      <button class="icon-btn" id="cartBtnTop">
        <svg viewBox="0 0 24 24"><circle cx="9" cy="21" r="1"/><circle cx="20" cy="21" r="1"/><path d="M1 1h4l2.68 13.39a2 2 0 0 0 2 1.61h9.72a2 2 0 0 0 2-1.61L23 6H6"/></svg>
        <span class="cart-badge" id="cartBadge">0</span>
      </button>
      <button class="avatar-btn">H</button>
    </div>
  </div>

  <!-- HERO -->
  <div class="hero">
    <div class="h-badge">🔥 TODAY'S SPECIAL</div>
    <h2>Best Pizza <span>in Town!</span></h2>
    <p>Order karo, fresh deliver hoga 🛵</p>
    <div class="hero-food">🍕</div>
  </div>

  <!-- SEARCH + SUGGESTIONS -->
  <div class="srch-wrap" id="srchWrap">
    <div class="srch-glow"></div>
    <div class="srch-inner">
      <svg viewBox="0 0 24 24"><circle cx="11" cy="11" r="8"/><path d="m21 21-4.35-4.35"/></svg>
      <input type="text" id="searchInp" placeholder="Search pizza, burgers, shawarma..." autocomplete="off">
      <button class="srch-clear" id="srchClear">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/></svg>
      </button>
    </div>
    <div class="suggestions" id="suggestions"></div>
  </div>

  <!-- CATS -->
  <span class="sec-lbl" style="margin-top:10px">Categories</span>
  <div class="cats" id="cats">
    <div class="cat on" data-cat="all">
      <svg viewBox="0 0 24 24"><path d="M3 9l9-7 9 7v11a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2z"/></svg>All
    </div>
    <div class="cat" data-cat="pizza">
      <svg viewBox="0 0 24 24"><path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2z" stroke-width="1.5"/><path d="M12 2v10l6.5 3.5"/></svg>Pizza
    </div>
    <div class="cat" data-cat="burger">
      <svg viewBox="0 0 24 24"><rect x="3" y="10" width="18" height="4" rx="2"/><path d="M5 10V7a7 7 0 0 1 14 0v3"/><path d="M3 14v2a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2v-2"/></svg>Burgers
    </div>
    <div class="cat" data-cat="shawarma">
      <svg viewBox="0 0 24 24"><path d="M4 20h16M4 4h16M12 4v16M8 8l4 4 4-4M8 16l4-4 4 4"/></svg>Shawarma
    </div>
    <div class="cat" data-cat="wings">
      <svg viewBox="0 0 24 24"><path d="M20.84 4.61a5.5 5.5 0 0 0-7.78 0L12 5.67l-1.06-1.06a5.5 5.5 0 0 0-7.78 7.78l1.06 1.06L12 21.23l7.78-7.78 1.06-1.06a5.5 5.5 0 0 0 0-7.78z"/></svg>Wings
    </div>
    <div class="cat" data-cat="sandwich">
      <svg viewBox="0 0 24 24"><path d="M21 15a2 2 0 0 1-2 2H7l-4 4V5a2 2 0 0 1 2-2h14a2 2 0 0 1 2 2z"/></svg>Sandwich
    </div>
  </div>

  <span class="sec-lbl reveal">Popular Items</span>
  <div class="mgrid" id="menuGrid"></div>

  <!-- DEALS -->
  <div class="deals" id="dealsSection">
    <span class="sec-lbl reveal" style="padding:0;margin-bottom:12px">🔥 Pizza Deals</span>
    <div class="deal-row reveal">
      <div class="dr-icon">🍕🍕</div>
      <div class="dr-info"><div class="dr-name">XL + Medium Combo</div><div class="dr-desc">Best value • Extra topping +Rs.450</div></div>
      <div><div class="dr-price">Rs.2,650</div><div class="dr-sub">combo</div></div>
      <button class="dr-add-btn" onclick="addItem({id:'deal1',name:'XL + Medium Combo',emoji:'🍕🍕',price:2650})">+</button>
    </div>
    <div class="deal-row reveal">
      <div class="dr-icon">🍕🍕</div>
      <div class="dr-info"><div class="dr-name">Large + Small Combo</div><div class="dr-desc">Family deal • Extra topping +Rs.250</div></div>
      <div><div class="dr-price">Rs.2,000</div><div class="dr-sub">combo</div></div>
      <button class="dr-add-btn" onclick="addItem({id:'deal2',name:'Large + Small Combo',emoji:'🍕🍕',price:2000})">+</button>
    </div>
  </div>

  <!-- SIZES -->
  <span class="sec-lbl reveal">Pizza Sizes</span>
  <div class="szscroll" id="szscroll">
    <div class="szc reveal" onclick="pickSize(this,{id:'sxl',name:'XL Pizza (16\u22)',emoji:'🍕',price:1850})"><span class="sz-em">🍕</span><div class="sz-nm">XL</div><div class="sz-in">16"</div><div class="sz-pr">Rs.1,850</div><div class="sz-tp">+Rs.300 topping</div></div>
    <div class="szc reveal" onclick="pickSize(this,{id:'slg',name:'Large Pizza (13\u22)',emoji:'🍕',price:1450})"><span class="sz-em">🍕</span><div class="sz-nm">Large</div><div class="sz-in">13"</div><div class="sz-pr">Rs.1,450</div><div class="sz-tp">+Rs.270 topping</div></div>
    <div class="szc reveal" onclick="pickSize(this,{id:'smd',name:'Medium Pizza (10\u22)',emoji:'🍕',price:950})"><span class="sz-em">🍕</span><div class="sz-nm">Medium</div><div class="sz-in">10"</div><div class="sz-pr">Rs.950</div><div class="sz-tp">+Rs.200 topping</div></div>
    <div class="szc reveal" onclick="pickSize(this,{id:'ssm',name:'Small Pizza (9\u22)',emoji:'🍕',price:650})"><span class="sz-em">🍕</span><div class="sz-nm">Small</div><div class="sz-in">9"</div><div class="sz-pr">Rs.650</div><div class="sz-tp">+Rs.130 topping</div></div>
  </div>

  <!-- FLAVOURS -->
  <div class="flavsec reveal">
    <span class="sec-lbl" style="padding:0;margin-bottom:12px">Pizza Flavours</span>
    <div class="flavscroll">
      <div class="flav sel"><span class="fl-em">🌶️</span><div class="fl-nm">Chicken Tikka</div></div>
      <div class="flav"><span class="fl-em">🔥</span><div class="fl-nm">BBQ</div></div>
      <div class="flav"><span class="fl-em">🌮</span><div class="fl-nm">Fujita</div></div>
      <div class="flav"><span class="fl-em">🧀</span><div class="fl-nm">Cheese Lover</div></div>
      <div class="flav"><span class="fl-em">🍢</span><div class="fl-nm">Mali Boti</div></div>
      <div class="flav"><span class="fl-em">🥩</span><div class="fl-nm">Seekh Kabab</div></div>
      <div class="flav"><span class="fl-em">💥</span><div class="fl-nm">Hot &amp; Spicy</div></div>
      <div class="flav special"><span class="fl-em">⭐</span><div class="fl-nm">HAQS Special</div><div class="fl-sub">Tikka+BBQ+Fujita+Seekh</div></div>
    </div>
  </div>

  <!-- BOTTOM NAV (3 items only) -->
  <div class="bnav">
    <div class="ni on" id="ni-home" onclick="setNav('home')">
      <div class="ni-icon-wrap">
        <svg class="ni-svg" viewBox="0 0 24 24"><path d="M3 9l9-7 9 7v11a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2z"/><polyline points="9 22 9 12 15 12 15 22"/></svg>
      </div>
      <span class="ni-lbl">Home</span>
    </div>
    <div class="ni" id="ni-menu" onclick="setNav('menu')">
      <div class="ni-icon-wrap">
        <svg class="ni-svg" viewBox="0 0 24 24"><path d="M9 5H7a2 2 0 0 0-2 2v12a2 2 0 0 0 2 2h10a2 2 0 0 0 2-2V7a2 2 0 0 0-2-2h-2"/><rect x="9" y="3" width="6" height="4" rx="2"/><path d="M9 12h6M9 16h4"/></svg>
      </div>
      <span class="ni-lbl">Menu</span>
    </div>
    <div class="ni" id="ni-cart" onclick="openCart();setNav('cart')">
      <div class="ni-icon-wrap">
        <svg class="ni-svg" viewBox="0 0 24 24"><circle cx="9" cy="21" r="1"/><circle cx="20" cy="21" r="1"/><path d="M1 1h4l2.68 13.39a2 2 0 0 0 2 1.61h9.72a2 2 0 0 0 2-1.61L23 6H6"/></svg>
      </div>
      <span class="ni-lbl">Cart</span>
      <span class="ni-badge" id="niBadge">0</span>
    </div>
  </div>
</div>

<!-- ══ CHECKOUT PAGE ══ -->
<div id="pg-checkout" class="pg">
  <div class="co-head">
    <button class="back-btn" id="backBtn">
      <svg viewBox="0 0 24 24"><polyline points="15 18 9 12 15 6"/></svg>
    </button>
    <h2>Complete Your Order</h2>
  </div>

  <div class="co-summary">
    <div class="co-sum-title">🛒 Order Summary</div>
    <div id="coItemsList"></div>
    <div class="co-total-row"><span>Total Amount</span><span id="coTotal">Rs.0</span></div>
    <div class="co-dlv-note">🎁 <b>Pehla Order:</b> Delivery bilkul FREE!<br>🛵 <b>Agli Orders:</b> Rider distance ke hisab se fee batayega</div>
  </div>

  <div class="co-form">
    <div class="co-form-title">📋 Delivery Details</div>
    <div class="f-grp">
      <label class="f-lbl">Your Name *</label>
      <input type="text" class="f-inp" id="f-name" placeholder="Apna naam likhein">
    </div>
    <div class="f-grp">
      <label class="f-lbl">Phone Number *</label>
      <input type="tel" class="f-inp" id="f-phone" placeholder="03XX-XXXXXXX">
    </div>
    <div class="f-grp">
      <label class="f-lbl">Delivery Address *</label>
      <textarea class="f-ta" id="f-addr" rows="3" placeholder="Ghar ka pura address likhein..."></textarea>
    </div>
    <div class="f-grp">
      <label class="f-lbl">Special Instructions (Optional)</label>
      <textarea class="f-ta" id="f-note" rows="2" placeholder="Koi khaas baat ho toh likhein..."></textarea>
    </div>
  </div>

  <button class="btn-confirm" id="confirmBtn">
    <svg viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347z"/><path d="M13 0C5.82 0 0 5.82 0 13c0 2.295.6 4.44 1.647 6.3L0 26l6.9-1.617A12.94 12.94 0 0 0 13 26c7.18 0 13-5.82 13-13S20.18 0 13 0zm0 23.8a10.79 10.79 0 0 1-5.477-1.488l-.393-.233-4.096.961.979-3.997-.257-.41A10.822 10.822 0 0 1 2.2 13C2.2 7.029 7.029 2.2 13 2.2c5.971 0 10.8 4.829 10.8 10.8 0 5.971-4.829 10.8-10.8 10.8z"/></svg>
    Confirm Order on WhatsApp
  </button>
</div>

<!-- CART OVERLAY + PANEL -->
<div class="cart-overlay" id="cartOverlay" onclick="closeCart()"></div>
<div class="cart-panel" id="cartPanel">
  <div class="cp-head">
    <span class="cp-title">Your Order <span id="cartCount"></span></span>
    <button class="cp-close" onclick="closeCart()">
      <svg viewBox="0 0 24 24"><line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/></svg>
    </button>
  </div>
  <div class="cp-body" id="cartBody"></div>
  <div class="cp-foot" id="cartFoot" style="display:none">
    <div class="cp-row"><span>Subtotal</span><span id="subtotalTxt">Rs.0</span></div>
    <div class="delivery-note">🎁 <b>Pehla Order:</b> Delivery FREE!<br>🛵 <b>Agli Orders:</b> Distance ke hisab se fee</div>
    <div class="cp-total"><span>Total</span><span id="totalTxt">Rs.0</span></div>
    <button class="btn-checkout" onclick="goCheckout()">
      <svg viewBox="0 0 24 24"><polyline points="9 18 15 12 9 6"/></svg>
      Proceed to Order
    </button>
  </div>
</div>

<div class="toast" id="toast"></div>
<a href="https://wa.me/923135964444" class="fwa" id="fwa">
  <svg viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347z"/><path d="M13 0C5.82 0 0 5.82 0 13c0 2.295.6 4.44 1.647 6.3L0 26l6.9-1.617A12.94 12.94 0 0 0 13 26c7.18 0 13-5.82 13-13S20.18 0 13 0zm0 23.8a10.79 10.79 0 0 1-5.477-1.488l-.393-.233-4.096.961.979-3.997-.257-.41A10.822 10.822 0 0 1 2.2 13C2.2 7.029 7.029 2.2 13 2.2c5.971 0 10.8 4.829 10.8 10.8 0 5.971-4.829 10.8-10.8 10.8z"/></svg>
</a>

<script>
// ── DATA ──
const MENU=[
  {id:'zb',name:'Zinger Burger',emoji:'🍔',price:280,cat:'burger',tag:'Crispy fried chicken'},
  {id:'cb',name:'Cheese Burger',emoji:'🧀',price:380,cat:'burger',tag:'Double cheese loaded'},
  {id:'zw',name:'Zinger Wings',emoji:'🍗',price:110,cat:'wings',tag:'Per piece crispy'},
  {id:'cs',name:'Chicken Shawarma',emoji:'🌯',price:170,cat:'shawarma',tag:'Classic marinated'},
  {id:'chsh',name:'Cheese Shawarma',emoji:'🌯',price:300,cat:'shawarma',tag:'Extra cheese'},
  {id:'gs',name:'Grilled Sandwich',emoji:'🥪',price:380,cat:'sandwich',tag:'Hot grilled'},
  {id:'pxl',name:'XL Pizza (16")',emoji:'🍕',price:1850,cat:'pizza',tag:'Feeds 4-5 people'},
  {id:'plg',name:'Large Pizza (13")',emoji:'🍕',price:1450,cat:'pizza',tag:'Feeds 3-4 people'},
  {id:'pmd',name:'Medium Pizza (10")',emoji:'🍕',price:950,cat:'pizza',tag:'Feeds 2-3 people'},
  {id:'psm',name:'Small Pizza (9")',emoji:'🍕',price:650,cat:'pizza',tag:'Feeds 1-2 people'},
];
let cart=[], loggedIn=false;

// ── RENDER MENU ──
function renderMenu(filter='all',query=''){
  const grid=document.getElementById('menuGrid');
  let items=filter==='all'?MENU:MENU.filter(i=>i.cat===filter);
  if(query) items=items.filter(i=>i.name.toLowerCase().includes(query.toLowerCase())||i.tag.toLowerCase().includes(query.toLowerCase()));
  if(items.length===0){
    grid.innerHTML=`<div style="grid-column:1/-1;text-align:center;padding:30px;color:var(--ts);font-size:.88rem;">Koi item nahi mila 😔</div>`;
    return;
  }
  grid.innerHTML=items.map(item=>`
    <div class="mc" id="mc-${item.id}">
      <span class="mc-em">${item.emoji}</span>
      <div class="mc-name">${item.name}</div>
      <div class="mc-price">Rs.${item.price.toLocaleString()}</div>
      <button class="mc-add" onclick="addItem(${JSON.stringify(item).replace(/"/g,'&quot;')})">+</button>
    </div>`).join('');
  // staggered reveal
  setTimeout(()=>{
    document.querySelectorAll('.mc').forEach((el,i)=>{
      setTimeout(()=>el.classList.add('vis'),i*45);
    });
  },30);
}

// ── ADD TO CART ──
function addItem(item){
  const ex=cart.find(c=>c.id===item.id);
  if(ex) ex.qty++;
  else cart.push({...item,qty:1});
  updateCartUI();
  showToast(`${item.emoji} ${item.name} added!`);
  const card=document.getElementById('mc-'+item.id);
  if(card){card.classList.remove('pop');void card.offsetWidth;card.classList.add('pop');}
}

// ── CART UI ──
function updateCartUI(){
  const total=cart.reduce((s,i)=>s+i.price*i.qty,0);
  const count=cart.reduce((s,i)=>s+i.qty,0);
  document.getElementById('cartBadge').textContent=count;
  document.getElementById('cartBadge').classList.toggle('show',count>0);
  document.getElementById('niBadge').textContent=count;
  document.getElementById('niBadge').classList.toggle('show',count>0);
  document.getElementById('cartCount').textContent=count>0?`(${count} items)`:'';
  const body=document.getElementById('cartBody');
  const foot=document.getElementById('cartFoot');
  if(cart.length===0){
    body.innerHTML=`<div class="cp-empty"><span class="em-ico">🛒</span><p>Cart abhi khali hai</p><button class="btn-browse" onclick="closeCart()">Menu Browse Karo</button></div>`;
    foot.style.display='none';
  }else{
    body.innerHTML=cart.map(i=>`
      <div class="cart-item">
        <span class="ci-em">${i.emoji}</span>
        <div class="ci-info"><div class="ci-name">${i.name}</div><div class="ci-price">Rs.${(i.price*i.qty).toLocaleString()}</div></div>
        <div class="qty-ctrl">
          <button class="qbtn" onclick="changeQty('${i.id}',-1)">−</button>
          <span class="qnum">${i.qty}</span>
          <button class="qbtn" onclick="changeQty('${i.id}',1)">+</button>
        </div>
      </div>`).join('');
    foot.style.display='block';
    document.getElementById('subtotalTxt').textContent=`Rs.${total.toLocaleString()}`;
    document.getElementById('totalTxt').textContent=`Rs.${total.toLocaleString()}`;
  }
}

function changeQty(id,delta){
  const idx=cart.findIndex(c=>c.id===id);
  if(idx===-1)return;
  cart[idx].qty+=delta;
  if(cart[idx].qty<=0)cart.splice(idx,1);
  updateCartUI();
}

// ── CART OPEN/CLOSE ──
function openCart(){
  document.getElementById('cartOverlay').classList.add('open');
  document.getElementById('cartPanel').classList.add('open');
  document.body.style.overflow='hidden';
}
function closeCart(){
  document.getElementById('cartOverlay').classList.remove('open');
  document.getElementById('cartPanel').classList.remove('open');
  document.body.style.overflow='';
}

// ── CHECKOUT ──
function goCheckout(){
  closeCart();
  showPage('pg-checkout');
  const list=document.getElementById('coItemsList');
  const total=cart.reduce((s,i)=>s+i.price*i.qty,0);
  list.innerHTML=cart.map(i=>`
    <div class="co-item-row">
      <div><span>${i.emoji} </span><span class="co-iname">${i.name}</span> <span class="co-iqty">x${i.qty}</span></div>
      <span class="co-iprice">Rs.${(i.price*i.qty).toLocaleString()}</span>
    </div>`).join('');
  document.getElementById('coTotal').textContent=`Rs.${total.toLocaleString()}`;
}

// ── CONFIRM ORDER ──
document.getElementById('confirmBtn').addEventListener('click',function(){
  const name=document.getElementById('f-name').value.trim();
  const phone=document.getElementById('f-phone').value.trim();
  const addr=document.getElementById('f-addr').value.trim();
  const note=document.getElementById('f-note').value.trim();
  let valid=true;
  ['f-name','f-phone','f-addr'].forEach(id=>{
    const el=document.getElementById(id);
    if(!el.value.trim()){el.classList.add('err');valid=false;setTimeout(()=>el.classList.remove('err'),600);}
  });
  if(!valid){showToast('⚠️ Pehle saari details fill karein!');return;}
  const total=cart.reduce((s,i)=>s+i.price*i.qty,0);
  const lines=cart.map(i=>`• ${i.emoji} ${i.name} x${i.qty} = Rs.${(i.price*i.qty).toLocaleString()}`).join('\n');
  const msg=`🍕 *New Order — FoodTrend Fastfood*\n\n👤 *Name:* ${name}\n📞 *Phone:* ${phone}\n📍 *Address:* ${addr}\n\n🛒 *Order:*\n${lines}\n\n💰 *Total: Rs.${total.toLocaleString()}*\n🚚 *Delivery:* 1st Order FREE\n\n📝 *Note:* ${note||'None'}\n\n_via FoodTrend Website_`;
  window.open('https://wa.me/923135964444?text='+encodeURIComponent(msg),'_blank');
  showToast('🎉 Order WhatsApp pe bhej diya!');
});

// ── PAGES ──
function showPage(id){
  document.querySelectorAll('.pg').forEach(p=>{p.classList.remove('on');});
  const el=document.getElementById(id);
  el.classList.add('on');
  window.scrollTo({top:0,behavior:'smooth'});
  document.getElementById('fwa').style.display=id==='pg-main'?'flex':'none';
}

// ── LOGIN ──
function doLogin(){
  loggedIn=true;
  showPage('pg-main');
  renderMenu();
  updateCartUI();
  setTimeout(()=>initReveal(),100);
}
document.getElementById('gBtn').addEventListener('click',function(){
  this.innerHTML='✅ Signed in with Google!';
  this.style.borderColor='#34A853';this.style.color='#34A853';
  setTimeout(doLogin,700);
});
document.getElementById('signInBtn').addEventListener('click',doLogin);
document.getElementById('signUpLink').addEventListener('click',doLogin);

// ── BACK BTN ──
document.getElementById('backBtn').addEventListener('click',function(){
  showPage('pg-main');
  setTimeout(()=>openCart(),120);
});

// ── CART TOP BTN ──
document.getElementById('cartBtnTop').addEventListener('click',openCart);

// ── CATS ──
document.getElementById('cats').addEventListener('click',function(e){
  const cat=e.target.closest('.cat');
  if(!cat)return;
  document.querySelectorAll('.cat').forEach(c=>c.classList.remove('on'));
  cat.classList.add('on');
  renderMenu(cat.dataset.cat,document.getElementById('searchInp').value);
});

// ── SEARCH + SUGGESTIONS ──
const searchInp=document.getElementById('searchInp');
const sugBox=document.getElementById('suggestions');
const srchClear=document.getElementById('srchClear');

searchInp.addEventListener('input',function(){
  const q=this.value.trim();
  srchClear.style.display=q?'block':'none';
  const activeCat=document.querySelector('.cat.on')?.dataset.cat||'all';
  renderMenu(activeCat,q);
  if(q.length<1){sugBox.classList.remove('open');return;}
  const matches=MENU.filter(i=>
    i.name.toLowerCase().includes(q.toLowerCase())||
    i.tag.toLowerCase().includes(q.toLowerCase())
  ).slice(0,6);
  if(matches.length===0){sugBox.classList.remove('open');return;}
  sugBox.innerHTML=matches.map(i=>`
    <div class="sug-item" onclick="selectSug(${JSON.stringify(i).replace(/"/g,'&quot;')})">
      <span class="sug-em">${i.emoji}</span>
      <div class="sug-info">
        <div class="sug-name">${highlightMatch(i.name,q)}</div>
        <div class="sug-cat">${i.tag}</div>
      </div>
      <span class="sug-price">Rs.${i.price.toLocaleString()}</span>
      <button class="sug-add" onclick="event.stopPropagation();addItem(${JSON.stringify(i).replace(/"/g,'&quot;')})">+</button>
    </div>`).join('');
  sugBox.classList.add('open');
});

function highlightMatch(text,q){
  const idx=text.toLowerCase().indexOf(q.toLowerCase());
  if(idx===-1)return text;
  return text.slice(0,idx)+'<b style="color:var(--or)">'+text.slice(idx,idx+q.length)+'</b>'+text.slice(idx+q.length);
}

function selectSug(item){
  searchInp.value=item.name;
  sugBox.classList.remove('open');
  renderMenu('all',item.name);
}

srchClear.addEventListener('click',function(){
  searchInp.value='';
  this.style.display='none';
  sugBox.classList.remove('open');
  const activeCat=document.querySelector('.cat.on')?.dataset.cat||'all';
  renderMenu(activeCat,'');
});

document.addEventListener('click',function(e){
  if(!document.getElementById('srchWrap').contains(e.target)){
    sugBox.classList.remove('open');
  }
});

// ── NAV ──
function setNav(name){
  document.querySelectorAll('.ni').forEach(i=>i.classList.remove('on'));
  document.getElementById('ni-'+name)?.classList.add('on');
}

// ── SIZE PICK ──
function pickSize(el,item){
  document.querySelectorAll('.szc').forEach(s=>s.classList.remove('picked'));
  el.classList.add('picked');
  addItem(item);
}

// ── FLAVOURS ──
document.querySelectorAll('.flav').forEach(f=>{
  f.addEventListener('click',function(){
    document.querySelectorAll('.flav').forEach(x=>x.classList.remove('sel'));
    this.classList.add('sel');
  });
});

// ── TOAST ──
function showToast(msg){
  const t=document.getElementById('toast');
  t.textContent=msg;t.classList.add('show');
  setTimeout(()=>t.classList.remove('show'),2500);
}

// ── SCROLL REVEAL ──
function initReveal(){
  const obs=new IntersectionObserver((entries)=>{
    entries.forEach(e=>{
      if(e.isIntersecting){e.target.classList.add('vis');obs.unobserve(e.target);}
    });
  },{threshold:0.12});
  document.querySelectorAll('.reveal,.szc,.deal-row').forEach(el=>obs.observe(el));
}
</script>
</body>
</html>
