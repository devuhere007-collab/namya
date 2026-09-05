# namya
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Photo Story Planner</title>
<style>
  * { box-sizing: border-box; }
  body {
    margin: 0;
    font-family: Inter, Arial, sans-serif;
    background: #000;
    color: #f5f5f5;
  }
  header {
    position: sticky;
    top: 0;
    z-index: 10;
    padding: 18px 28px;
    background: rgba(255,255,255,.94);
    border-bottom: 1px solid #ddd7cd;
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 20px;
  }
  h1 { margin: 0; font-size: 24px; }
  .subtitle { color: #777; font-size: 13px; margin-top: 4px; }
  button {
    border: 0;
    border-radius: 9px;
    padding: 10px 15px;
    cursor: pointer;
    background: #222;
    color: white;
    font-weight: 600;
  }
  main { padding: 24px; }
  .row {
    background: #111;
    border: 1px solid #ded8cf;
    border-radius: 16px;
    margin-bottom: 22px;
    padding: 18px;
    box-shadow: 0 4px 18px rgba(0,0,0,.04);
  }
  .row-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 14px;
  }
  .row-title {
    font-weight: 800;
    font-size: 15px;
  }
  .row-actions { display: flex; gap: 8px; }
  .row-actions button {
    background: #eeeae4;
    color: #333;
    font-size: 12px;
    padding: 7px 10px;
  }
  .photo-strip {
    display: flex;
    gap: 14px;
    overflow-x: auto;
    padding-bottom: 8px;
    min-height: 285px;
  }
  .card {
    position: relative;
    flex: 0 0 245px;
    border: 1px solid #ddd7cd;
    border-radius: 12px;
    overflow: hidden;
    background: #faf9f7;
  }
  .photo {
    cursor: pointer;
    transition: transform .25s ease, filter .25s ease;
    width: 100%;
    height: 145px;
    object-fit: cover;
    display: block;
    background: #e8e3db;
  }
  .content { padding: 11px; display:none; }
  .name {
    width: 100%;
    border: 0;
    border-bottom: 1px solid #d8d2c9;
    background: transparent;
    padding: 5px 2px 7px;
    font-size: 15px;
    font-weight: 700;
    outline: none;
  }
  .card:hover .photo { transform: scale(1.07); filter: brightness(1.08); }
  .description {
    width: 100%;
    min-height: 76px;
    margin-top: 8px;
    border: 0;
    resize: vertical;
    background: transparent;
    font: 13px/1.45 Arial, sans-serif;
    outline: none;
    color: #555;
  }
  .remove {
    width: calc(100% - 22px);
    margin: 0 11px 11px;
    background: #e9e5df;
    color: #444;
    font-size: 11px;
    padding: 7px;
  }
  .add-card {
    flex: 0 0 245px;
    min-height: 245px;
    border: 2px dashed #c8c1b7;
    border-radius: 12px;
    display: grid;
    place-items: center;
    color: #777;
    cursor: pointer;
    text-align: center;
    padding: 20px;
  }
  .add-card:hover { background: #f8f6f2; }
  input[type=file] { display: none; }
  @media (max-width: 700px) {
    header { position: static; padding: 15px; }
    main { padding: 12px; }
    .row { padding: 12px; }
  }
</style>
<style>
/* Netflix-inspired visual treatment */
body{background:#050505;color:#f5f5f5}
header{background:linear-gradient(180deg,#080808 0%,rgba(8,8,8,.94) 75%,rgba(8,8,8,0) 100%);border:0;color:#fff;padding:24px 4vw}
h1{font-size:30px;letter-spacing:-.5px}.subtitle{color:#aaa}
header button{background:#e50914;border-radius:5px}
main{padding:20px 4vw 50px}
.row{background:transparent;border:0;border-radius:0;padding:0;margin-bottom:34px;box-shadow:none}
.row-header{margin-bottom:10px}.row-title{font-size:20px}.row-title:before{content:"";display:inline-block;width:4px;height:20px;background:#e50914;margin-right:9px;vertical-align:-3px}
.row-actions button{background:#222;color:#eee;border:1px solid #333;border-radius:4px}
.photo-strip{gap:8px;min-height:0;overflow-x:auto;padding:8px 2px 16px;scrollbar-color:#555 transparent}
.card{flex:0 0 220px;border:0;border-radius:4px;overflow:visible;background:transparent;transition:transform .25s ease, z-index .25s;position:relative}
.card:hover{transform:scale(1.07);z-index:5}
.photo{height:124px;border-radius:4px;transition:filter .25s;cursor:pointer;box-shadow:0 2px 10px rgba(0,0,0,.5)}
.card:hover .photo{filter:brightness(1.08)}
.content{padding:8px 2px}.name{color:#fff;border:0;font-size:14px;padding:5px 0}.description{color:#aaa;min-height:55px}
.remove{background:#222;color:#bbb;border:1px solid #333;border-radius:3px;width:auto;margin:0 2px 8px;padding:5px 8px}
.add-card{flex:0 0 220px;min-height:124px;border:1px dashed #444;border-radius:4px;color:#888;background:#111}
.add-card:hover{background:#181818}
input[type=file]{display:none}
/* Detail viewer */
.viewer{position:fixed;inset:0;z-index:100;background:rgba(0,0,0,.94);display:none;overflow:auto}
.viewer.open{display:block}
.viewer-close{position:fixed;top:20px;right:25px;z-index:3;width:42px;height:42px;border-radius:50%;background:#222;color:#fff;font-size:24px;padding:0}
.viewer-inner{min-height:100vh;padding:70px 5vw 5vw;display:grid;grid-template-columns:minmax(320px,52vw) 1fr;gap:34px;align-items:start}
.viewer-image{width:100%;max-height:72vh;object-fit:contain;object-position:top left;border-radius:3px;background:#111;box-shadow:0 20px 60px rgba(0,0,0,.7)}
.viewer-info{padding:8px 0}.viewer-kicker{color:#e50914;font-weight:800;font-size:13px;text-transform:uppercase;letter-spacing:1.5px}.viewer-title{font-size:clamp(28px,4vw,52px);margin:8px 0 20px}.viewer-text{width:100%;min-height:50vh;resize:vertical;background:#151515;color:#eee;border:1px solid #333;border-radius:5px;padding:18px;font:16px/1.65 Arial,sans-serif;outline:none}.viewer-text:focus{border-color:#e50914}.viewer-hint{color:#777;font-size:12px;margin-top:9px}
@media(max-width:800px){.viewer-inner{grid-template-columns:1fr;padding:65px 20px 30px}.viewer-image{max-height:55vh}.viewer-text{min-height:250px}.card{flex-basis:180px}.photo{height:102px}}
</style>
</head>
<body>
<header>
  <div><h1 id="siteTitle" contenteditable="true" spellcheck="false">Photo Story Planner</h1><div class="subtitle">Build your story one visual row at a time.</div></div>
  <button onclick="window.print()">Print / Save PDF</button>
</header>
<main id="planner"></main>

<div class="viewer" id="viewer" aria-hidden="true">
  <button class="viewer-close" onclick="closeViewer()" aria-label="Close">×</button>
  <div class="viewer-inner">
    <img class="viewer-image" id="viewerImage" alt="">
    <div class="viewer-info">
      <div class="viewer-kicker" id="viewerRow">PHOTO</div>
      <h2 class="viewer-title" id="viewerTitle">Photo</h2>
      <textarea class="viewer-text" id="viewerText" placeholder="Write a paragraph about this photo..."></textarea>
      <div class="viewer-hint">Your text is saved while this page is open. Click outside or × to return to the gallery.</div>
    </div>
  </div>
</div>

<script>
const planner=document.getElementById('planner');
const siteTitle=document.getElementById('siteTitle');
const viewer=document.getElementById('viewer');
const STORAGE_KEY='photo-story-planner-v1';
const SYNC_CHANNEL='photo-story-planner-sync-v1';
const syncChannel=('BroadcastChannel' in window)?new BroadcastChannel(SYNC_CHANNEL):null;
function saveState(){
  const state={title:siteTitle.textContent.trim()||'Photo Story Planner',rows:[...planner.querySelectorAll('.row')].map(row=>({
    label:row.dataset.label,
    photos:[...row.querySelectorAll('.card')].map(card=>({src:card.querySelector('.photo').src,title:card.querySelector('.name').value,text:card.querySelector('.description').value}))
  }))};
  try{localStorage.setItem(STORAGE_KEY,JSON.stringify(state)); if(syncChannel) syncChannel.postMessage({type:'state',state})}catch(e){console.warn('Could not save planner state',e)}
}
function loadState(){try{return JSON.parse(localStorage.getItem(STORAGE_KEY)||'null')}catch(e){return null}}

const viewerImage=document.getElementById('viewerImage');
const viewerTitle=document.getElementById('viewerTitle');
const viewerText=document.getElementById('viewerText');
const viewerRow=document.getElementById('viewerRow');
let activeCard=null;
function placeholder(label){const svg=`<svg xmlns="http://www.w3.org/2000/svg" width="600" height="360"><rect width="100%" height="100%" fill="#181818"/><text x="50%" y="50%" dominant-baseline="middle" text-anchor="middle" font-family="Arial" font-size="28" fill="#777">${label}</text></svg>`;return 'data:image/svg+xml;charset=UTF-8,'+encodeURIComponent(svg)}
function escapeHtml(s){return String(s).replaceAll('&','&amp;').replaceAll('<','&lt;').replaceAll('>','&gt;').replaceAll('"','&quot;')}
function createCard(row,imageSrc,title='Photo name',text=''){
 const card=document.createElement('article');card.className='card';
 card.innerHTML=`<img class="photo" src="${imageSrc}" alt="${escapeHtml(title)}"><div class="content"><input class="name" value="${escapeHtml(title)}" aria-label="Photo name"><textarea class="description" aria-label="Photo description" placeholder="Short note...">${escapeHtml(text)}</textarea></div><button class="remove" type="button">Remove</button>`;
 const img=card.querySelector('.photo');img.onclick=()=>openViewer(card,row);
 card.querySelector('.remove').onclick=()=>{card.remove();saveState()};
 card.querySelector('.name').addEventListener('input',saveState);card.querySelector('.description').addEventListener('input',saveState);
 row.querySelector('.photo-strip').insertBefore(card,row.querySelector('.add-card'));
}
function openViewer(card,row){
 activeCard=card;viewerImage.src=card.querySelector('.photo').src;viewerTitle.textContent=card.querySelector('.name').value||'Untitled photo';viewerText.value=card.querySelector('.description').value;viewerRow.textContent=row.dataset.label||'PHOTO';viewer.classList.add('open');viewer.setAttribute('aria-hidden','false');document.body.style.overflow='hidden';viewerText.focus();
}
function closeViewer(){if(activeCard){activeCard.querySelector('.name').value=viewerTitle.textContent;activeCard.querySelector('.description').value=viewerText.value}saveState();viewer.classList.remove('open');viewer.setAttribute('aria-hidden','true');document.body.style.overflow='';activeCard=null}
viewerText.addEventListener('input',()=>{if(activeCard)activeCard.querySelector('.description').value=viewerText.value});
viewerTitle.addEventListener('click',()=>{});
viewer.addEventListener('click',e=>{if(e.target===viewer)closeViewer()});document.addEventListener('keydown',e=>{if(e.key==='Escape'&&viewer.classList.contains('open'))closeViewer()});
function addUpload(row){const input=document.createElement('input');input.type='file';input.accept='image/*';input.multiple=true;input.onchange=()=>[...input.files].forEach(file=>{const reader=new FileReader();reader.onload=e=>{createCard(row,e.target.result,file.name.replace(/\.[^.]+$/,''),'');saveState()};reader.readAsDataURL(file)});input.click()}
function broadcastFullState(){try{const raw=localStorage.getItem(STORAGE_KEY);if(raw&&syncChannel)syncChannel.postMessage({type:'state',state:JSON.parse(raw)});}catch(e){}}
const saved=loadState();
siteTitle.addEventListener('input',saveState);
for(let i=1;i<=6;i++){
 const row=document.createElement('section');row.className='row';
 const savedRow=saved?.rows?.[i-1];row.dataset.label=savedRow?.label||`ROW ${i}`;
 row.innerHTML=`<div class="row-header"><div class="row-title">${escapeHtml(row.dataset.label)}</div><div class="row-actions"><button type="button" class="add-many">+ Add photos</button></div></div><div class="photo-strip"><div class="add-card"><div><strong>+ Add photos</strong><br><small>Select multiple images</small></div></div></div>`;
 row.querySelector('.add-card').onclick=()=>addUpload(row);row.querySelector('.add-many').onclick=()=>addUpload(row);planner.appendChild(row);
 if(savedRow?.photos?.length){savedRow.photos.forEach(photo=>createCard(row,photo.src,photo.title,photo.text));}
 else for(let j=1;j<=3;j++)createCard(row,placeholder(`Photo ${i}.${j}`),`Photo ${i}.${j}`,'Write a paragraph about this photo...');
}
if(saved?.title)siteTitle.textContent=saved.title;
</script>
</body>
</html>
