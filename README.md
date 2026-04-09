
<html lang="pt-br">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ComboX Wiki Pro</title>

<style>
*{margin:0;padding:0;box-sizing:border-box}
body{font-family:Arial;background:#f8f9fa;color:#202122}

header{
  background:#202122;
  color:#fff;
  padding:12px 20px;
  display:flex;
  justify-content:space-between;
  align-items:center;
}

header input{
  padding:8px;
  border-radius:4px;
  border:none;
  width:220px;
}

.layout{display:flex}

.sidebar{
  width:260px;
  background:#fff;
  border-right:1px solid #ccc;
  height:100vh;
  overflow:auto;
  padding:15px;
}

.sidebar h3{margin-bottom:10px}
.sidebar a{
  display:block;
  padding:6px;
  color:#0645ad;
  text-decoration:none;
  border-radius:4px;
}
.sidebar a:hover{background:#eee}

.content{flex:1;padding:20px}

.article{
  background:#fff;
  padding:20px;
  border:1px solid #ccc;
  border-radius:6px;
}

.infobox{
  float:right;
  width:260px;
  background:#f8f9fa;
  border:1px solid #ccc;
  padding:10px;
  margin:10px;
}

.section{margin-top:20px}

.ads{
  background:#f1f1f1;
  border:1px dashed #bbb;
  padding:15px;
  margin:20px 0;
  text-align:center;
}

.trade{border-bottom:1px solid #ddd;padding:8px}
.like{color:#0645ad;cursor:pointer;margin-left:10px}

.chat{border:1px solid #ccc;height:200px;overflow:auto;padding:10px;margin-top:10px}

.btn{
  padding:8px 12px;
  border:none;
  background:#3366cc;
  color:white;
  border-radius:4px;
  cursor:pointer;
}

.btn:hover{background:#254a91}

input{
  padding:8px;
  border:1px solid #ccc;
  border-radius:4px;
}

.fade{animation:fade .3s ease}
@keyframes fade{from{opacity:0}to{opacity:1}}

</style>
</head>

<body>

<header>
<div>ComboX Wiki</div>
<input id="search" placeholder="Pesquisar artigos..." oninput="search()">
</header>

<div class="layout">

<div class="sidebar">
<h3>Conteúdo</h3>
<a onclick="loadPage('home')">Página inicial</a>
<a onclick="loadPage('combos')">Combos</a>
<a onclick="loadPage('trades')">Trades</a>
<a onclick="loadPage('itens')">Itens</a>
<a onclick="loadPage('ranking')">Ranking</a>
<a onclick="loadPage('chat')">Chat</a>
</div>

<div class="content" id="content"></div>

</div>

<script>
let tradesData=[];

function loadPage(page){
content.classList.add('fade');

if(page==='home'){
content.innerHTML=`
<div class='article'>
<h1>ComboX Wiki</h1>
<p>Plataforma completa de guias, trades e estratégias.</p>
<div class='ads'>ANÚNCIO</div>
</div>`;
}

if(page==='combos'){
content.innerHTML=`
<div class='article'>
<h1>Combos</h1>
<div class='infobox'><b>Dica:</b> Combine ataques rápidos</div>
<p>Aprenda combos avançados para PvP.</p>
<input id='pergunta'><button class='btn' onclick='ia()'>Perguntar</button>
<p id='resp'></p>
</div>`;
}

if(page==='trades'){
content.innerHTML=`
<div class='article'>
<h1>Trades</h1>
<input id='tradeInput'><button class='btn' onclick='addTrade()'>Postar</button>
<div id='trades'></div>
</div>`;
renderTrades();
}

if(page==='itens'){
content.innerHTML=`
<div class='article'>
<h1>Itens</h1>
<p>Guias de como obter itens raros.</p>
</div>`;
}

if(page==='ranking'){
content.innerHTML=`
<div class='article'>
<h1>Ranking</h1>
<ol id='rankingList'></ol>
</div>`;
loadRanking();
}

if(page==='chat'){
content.innerHTML=`
<div class='article'>
<h1>Chat</h1>
<input id='msg'><button class='btn' onclick='sendMsg()'>Enviar</button>
<div class='chat' id='chatBox'></div>
</div>`;
}
}

function ia(){
let p=document.getElementById('pergunta').value.toLowerCase();
let r='Sem resposta';
if(p.includes('combo')) r='Use habilidades em sequência rápida.';
if(p.includes('espada')) r='Espadas são obtidas derrotando bosses.';
document.getElementById('resp').innerText=r;
}

function addTrade(){
let t=document.getElementById('tradeInput').value;
if(!t) return;
tradesData.push({text:t,likes:0});
saveTrades();
renderTrades();
}

function renderTrades(){
let container=document.getElementById('trades');
if(!container) return;
container.innerHTML='';
tradesData.forEach((t,i)=>{
let div=document.createElement('div');
div.className='trade';
div.innerHTML=`${t.text} <span class='like' onclick='like(${i})'>Curtir (${t.likes})</span>`;
container.appendChild(div);
});
}

function like(i){
tradesData[i].likes++;
saveTrades();
renderTrades();
}

function saveTrades(){
localStorage.setItem('trades',JSON.stringify(tradesData));
}

function loadTrades(){
let data=localStorage.getItem('trades');
if(data) tradesData=JSON.parse(data);
}

function loadRanking(){
let list=document.getElementById('rankingList');
let players=["Player1","Player2","Player3"];
players.sort(()=>Math.random()-0.5);
players.forEach(p=>{
let li=document.createElement('li');
li.innerText=p;
list.appendChild(li);
});
}

function sendMsg(){
let m=document.getElementById('msg').value;
if(!m) return;
let p=document.createElement('p');
p.innerText=m;
document.getElementById('chatBox').appendChild(p);
}

function search(){
let q=document.getElementById('search').value.toLowerCase();
if(q.includes('trade')) loadPage('trades');
if(q.includes('combo')) loadPage('combos');
}

loadTrades();
loadPage('home');

</script>

</body>
</html>
