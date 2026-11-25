<!DOCTYPE html>
<html lang="en"><head><meta charset="utf-8"><meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover"><title>Optical fibre lock simulator</title>
<style>
:root{--bg:#f4f6fb;--card:#fff;--ink:#101828;--mut:#566074;--line:#d5dbe8;--cell:#e3e8f2;--lit:#fff;--acc:#0e7490;--red:#dc2626;--grn:#059669;--amb:#b45309;--pulse:#e11d48;box-sizing:border-box;padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px)}
@media(prefers-color-scheme:dark){:root:not([data-theme="light"]){--bg:#0b1020;--card:#141b33;--ink:#f1f4fb;--mut:#aab4d0;--line:#2a3558;--cell:#222c4d;--lit:#f4f6fb;--acc:#22d3ee;--red:#ff6b5e;--grn:#34d399;--amb:#ffc857;--pulse:#ff5a4d}}
:root[data-theme="dark"]{--bg:#0b1020;--card:#141b33;--ink:#f1f4fb;--mut:#aab4d0;--line:#2a3558;--cell:#222c4d;--lit:#f4f6fb;--acc:#22d3ee;--red:#ff6b5e;--grn:#34d399;--amb:#ffc857;--pulse:#ff5a4d}
html{scroll-padding-top:env(safe-area-inset-top,0px)}
*{box-sizing:border-box}
body{margin:0 auto;max-width:520px;padding:16px;background:var(--bg);color:var(--ink);font:16px/1.5 system-ui,sans-serif}
h1{font-size:22px;margin:0 0 4px}h2{font-size:16px;margin:0 0 10px;color:var(--acc)}
.m{color:var(--mut);margin:0 0 14px;font-size:14px}
.card{background:var(--card);border:1px solid var(--line);border-radius:12px;padding:14px;margin-bottom:12px}
#grid{display:grid;grid-template-columns:repeat(3,64px);gap:8px;justify-content:center}
#grid button{height:64px;border-radius:10px;border:2px solid transparent;background:var(--cell);color:var(--ink);font-size:20px;cursor:pointer}
#grid .w{background:var(--lit);border-color:var(--ink);color:#101828}
#grid .r{background:var(--red);color:#fff}#grid .g{background:var(--grn);color:#fff}
#fib{display:flex;gap:12px;margin-bottom:12px}
.lane{flex:1;position:relative;height:96px;border:1px dashed var(--line);border-radius:12px;font-size:12px;color:var(--mut);padding:6px 8px;overflow:hidden}
.dot{position:absolute;left:calc(50% - 7px);width:14px;height:14px;border-radius:50%}
.row{display:flex;justify-content:space-between;gap:8px;font-size:14px;margin-bottom:6px}
code{background:var(--cell);padding:2px 6px;border-radius:6px}
#msg{font-weight:500}
.ctl{display:flex;flex-wrap:wrap;gap:8px;align-items:center;margin-bottom:10px;font-size:14px}
.ctl button{padding:8px 12px;border-radius:8px;border:1px solid var(--line);background:var(--card);color:var(--ink);cursor:pointer}
.ctl input{flex:1;min-width:120px}
ol{margin:0;padding-left:20px;font-size:14px;color:var(--mut)}
</style></head><body>
<h1>Optical fibre lock simulator</h1>
<p class="m">Tap three cells to enter a key. The default key is 1, 5, 9.</p>
<section class="card"><h2>Access Panel</h2><div id="grid"></div></section>
<div id="fib"><div class="lane" id="l1">Fibre 1: key presses</div><div class="lane" id="l2">Fibre 2: verdict</div></div>
<section class="card"><h2>Control Core</h2>
<div class="row"><span>Frame <code id="fr">none</code></span><span>Wrong tries <b id="wc">0</b>/3</span></div>
<div id="msg">Waiting for an entry</div></section>
<div class="ctl"><button id="rs">Reset</button><button id="sk">Set new key</button></div>
<div class="ctl"><label for="nz">Fibre noise <b id="no">0%</b></label><input id="nz" type="range" min="0" max="60" value="0"></div>
<ol id="log"></ol>
<script>
let key=[1,5,9],entry=[],lock=false,wrong=0,setK=false,newK=[],noise=0;
const $=id=>document.getElementById(id),cells=[],l1=$('l1'),l2=$('l2');
for(let i=1;i<=9;i++){const b=document.createElement('button');b.textContent=i;b.onclick=()=>press(i);$('grid').appendChild(b);cells[i]=b}
const paint=(i,c)=>{cells[i].className=c||''},msg=t=>{$('msg').textContent=t};
function log(t){const li=document.createElement('li');li.textContent=t;$('log').prepend(li);while($('log').children.length>5)$('log').lastChild.remove()}
function pulse(lane,down,col,cb){const d=document.createElement('i');d.className='dot';d.style.background=col;lane.appendChild(d);
 const a=d.animate(down?[{top:'24px'},{top:'78px'}]:[{top:'78px'},{top:'24px'}],{duration:650,easing:'linear'});a.onfinish=()=>{d.remove();cb&&cb()}}
const bits=n=>{const b=(n-1).toString(2).padStart(4,'0');return '1 '+b+' '+([...b].filter(x=>x==='1').length%2)};
function sound(code){try{const a=new(window.AudioContext||window.webkitAudioContext)(),s=code===0?[523,659,784]:code===2?[330,262,196,150]:[200];
 s.forEach((f,i)=>{const o=a.createOscillator(),g=a.createGain();o.frequency.value=f;o.type=code===2?'sawtooth':'square';g.gain.value=.05;o.connect(g);g.connect(a.destination);o.start(a.currentTime+i*.15);o.stop(a.currentTime+i*.15+.12)})}catch(e){}}
function clear(){entry=[];lock=false;cells.forEach((b,i)=>i&&paint(i,''));$('wc').textContent=wrong;$('fr').textContent='none'}
function press(i){
 if(lock)return;
 if(setK){if(newK.includes(i))return;newK.push(i);paint(i,'w');log('New key cell '+i+' captured');
  if(newK.length===3){key=newK;setK=false;$('sk').textContent='Set new key';msg('New key saved in Control Core memory');setTimeout(clear,800)}return}
 if(entry.includes(i))return;
 lock=true;paint(i,'w');const f=bits(i);$('fr').textContent=f;
 const bad=Math.random()*100<noise;
 pulse(l1,true,'var(--pulse)',()=>{
  if(bad){log('Cell '+i+': parity error, press again');msg('Parity check failed because of noise. Press again.');pulse(l2,false,'var(--amb)',()=>{paint(i,'');lock=false});return}
  entry.push(i);log('Cell '+i+' received, frame '+f);
  if(entry.length<3){lock=false;return}
  const ok=entry.join()===key.join();let code;
  if(ok){wrong=0;code=0}else{wrong++;if(wrong>=3){code=2}else code=1}
  const shown=code===2?3:wrong;if(code===2)wrong=0;
  $('wc').textContent=shown;
  msg(['Correct key. Counter reset.','Wrong key. Counter plus one.','Third wrong try in a row. Mocking sound plays.'][code]);
  log('Reply code '+code+' sent on Fibre 2');
  pulse(l2,false,'var(--pulse)',()=>{entry.forEach(c=>paint(c,code===0?'g':'r'));sound(code);setTimeout(clear,1300)});
 })}
$('rs').onclick=()=>{wrong=0;setK=false;newK=[];$('sk').textContent='Set new key';clear();msg('Reset. Waiting for an entry');log('Reset code 3')};
$('sk').onclick=()=>{clear();setK=true;newK=[];$('sk').textContent='Setting key';msg('Set-key mode: tap 3 new cells')};
$('nz').oninput=e=>{noise=+e.target.value;$('no').textContent=noise+'%'};
</script></body></html>
