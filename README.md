 <comboX>
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
  width:200px;
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
}
.sidebar a:hover{text-decoration:underline}

.content{
  flex:1;
  padding:20px;
}

.article{
  background:#fff;
  padding:20px;
  border:1px solid #ccc;
}

.article h1{margin-bottom:10px}

.infobox{
  float:right;
  width:250px;
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

.chat{border:1px solid #ccc;height:150px;overflow:auto;padding:10px}

</style>
</head>

<body>

<header>
<div>ComboX Wiki</div>
<input placeholder="Pesquisar artigos...">
</header>

<div class="layout">

<div class="sidebar">
<h3>Conteúdo</h3>
<a onclick="loadPage('home')">Página inicial</a>
<a onclick="loadPage('combos')">Combos</a>
<a onclick="loadPage('trades')">Trades</a>
<a onclick="loadPage('itens')">Itens</a>
<a onclick="loadPage('chat')">Chat</a>
</div>

<div class="content" id="content"></div>

</div>

<script>

function loadPage(page){

if(page==='home'){
content.innerHTML=`
<div class='article'>
<h1>Bem-vindo ao ComboX</h1>
<p>Wiki completa com guias, estratégias e trades.</p>
<div class='ads'>ANÚNCIO</div>
</div>`;
}

if(page==='combos'){
content.innerHTML=`
<div class='article'>
<h1>Combos</h1>
<div class='infobox'>
<b>Dica</b><br>Use ataques rápidos
</div>
<p>Combos são sequências de ataques para maximizar dano.</p>
<input id='pergunta'><button onclick='ia()'>Perguntar</button>
<p id='resp'></p>
</div>`;
}

if(page==='trades'){
content.innerHTML=`
<div class='article'>
<h1>Trades</h1>
<input id='tradeInput'><button onclick='addTrade()'>Postar</button>
<div id='trades'></div>
</div>`;
}

if(page==='itens'){
content.innerHTML=`
<div class='article'>
<h1>Itens</h1>
<p>Lista de itens e como obter.</p>
</div>`;
}

if(page==='chat'){
content.innerHTML=`
<div class='article'>
<h1>Chat</h1>
<input id='msg'><button onclick='sendMsg()'>Enviar</button>
<div class='chat' id='chatBox'></div>
</div>`;
}
}

function ia(){
let p=document.getElementById('pergunta').value.toLowerCase();
let r='Sem resposta';
if(p.includes('combo')) r='Use habilidades em sequência rápida';
document.getElementById('resp').innerText=r;
}

function addTrade(){
let t=document.getElementById('tradeInput').value;
let div=document.createElement('div');
div.className='trade';
div.innerHTML=t+" <span class='like' onclick='this.innerText="Curtido"'>Curtir</span>";
document.getElementById('trades').appendChild(div);
}

function sendMsg(){
let m=document.getElementById('msg').value;
let p=document.createElement('p');
p.innerText=m;
document.getElementById('chatBox').appendChild(p);
}

loadPage('home');

</script>

</body>
</html>
