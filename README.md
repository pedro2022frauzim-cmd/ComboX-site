<!DOCTYPE html>
<html lang="pt-br">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ComboX - Gamer Hub</title>

<style>
*{margin:0;padding:0;box-sizing:border-box}

body{
  font-family: 'Segoe UI', Arial;
  background: radial-gradient(circle at top,#0a0a0a,#000);
  color:#eaeaea;
}

header{
  background: linear-gradient(90deg,#0f0f0f,#1c1c1c);
  padding:25px;
  text-align:center;
  font-size:32px;
  letter-spacing:2px;
  border-bottom:1px solid #222;
}

nav{
  display:flex;
  justify-content:center;
  flex-wrap:wrap;
  gap:10px;
  background:#111;
  padding:15px;
  border-bottom:1px solid #222;
}

nav button{
  background:#1f1f1f;
  color:#fff;
  border:1px solid #333;
  padding:10px 15px;
  border-radius:8px;
  cursor:pointer;
  transition:0.3s;
}

nav button:hover{
  background:#00ff88;
  color:#000;
  transform:translateY(-2px);
}

.section{
  display:none;
  padding:30px;
  max-width:900px;
  margin:auto;
}

.active{display:block}

.card{
  background:#111;
  border:1px solid #222;
  padding:20px;
  border-radius:12px;
  margin-bottom:20px;
  box-shadow:0 0 10px rgba(0,255,136,0.1);
}

input{
  width:70%;
  padding:12px;
  border-radius:8px;
  border:1px solid #333;
  background:#0f0f0f;
  color:#fff;
}

button.action{
  padding:12px 20px;
  background:#00ff88;
  border:none;
  color:#000;
  border-radius:8px;
  cursor:pointer;
  transition:0.3s;
}

button.action:hover{
  transform:scale(1.05);
}

.ads{
  max-width:900px;
  margin:30px auto;
  padding:25px;
  background:linear-gradient(135deg,#111,#1a1a1a);
  border:1px solid #333;
  border-radius:12px;
  text-align:center;
  font-size:14px;
  color:#888;
}

#login{
  text-align:center;
  margin-top:150px;
}

#login input{
  display:block;
  margin:10px auto;
  width:250px;
}

#site{display:none}

h2{
  margin-bottom:15px;
  font-weight:500;
}

p{margin-top:10px}

</style>
</head>

<body>

<div id="login">
  <h2>ComboX Login</h2>
  <input id="user" placeholder="UsuÃ¡rio">
  <input id="pass" type="password" placeholder="Senha">
  <button class="action" onclick="login()">Entrar</button>
</div>

<div id="site">
<header>ComboX Gamer Hub</header>

<nav>
<button onclick="show('dicas')">Combos</button>
<button onclick="show('trades')">Trades</button>
<button onclick="show('wiki')">Wiki</button>
<button onclick="show('crew')">Crew</button>
<button onclick="show('perfil')">Perfil</button>
<button onclick="show('chat')">Chat</button>
<button onclick="logout()">Sair</button>
</nav>

<div class="ads">EspaÃ§o de anÃºncio premium</div>

<div id="dicas" class="section active">
<div class="card">
<h2>Assistente de Combos</h2>
<input id="pergunta" placeholder="Digite sua dÃºvida">
<button class="action" onclick="responder()">Buscar</button>
<p id="resposta"></p>
</div>
</div>

<div id="trades" class="section">
<div class="card">
<h2>Publicar Trade</h2>
<input id="tradeInput" placeholder="Descreva sua troca">
<button class="action" onclick="addTrade()">Postar</button>
<div id="tradesList"></div>
</div>
</div>

<div id="wiki" class="section">
<div class="card">
<h2>Guia de Itens</h2>
<input id="wikiPergunta" placeholder="Como obter item">
<button class="action" onclick="wikiResp()">Buscar</button>
<p id="wikiResposta"></p>
</div>
</div>

<div id="crew" class="section">
<div class="card">
<h2>DivulgaÃ§Ã£o de Crew</h2>
<input id="crewInput" placeholder="Nome da crew">
<button class="action" onclick="addCrew()">Publicar</button>
<div id="crewList"></div>
</div>
</div>

<div id="perfil" class="section">
<div class="card">
<h2>Perfil</h2>
<p id="nomeUser"></p>
<h3>Ranking</h3>
<ol>
<li>TopPlayer - 2500</li>
<li>ProGamer - 2300</li>
<li>NoobMaster - 2000</li>
</ol>
</div>
</div>

<div id="chat" class="section">
<div class="card">
<h2>Chat Global</h2>
<input id="msg" placeholder="Mensagem">
<button class="action" onclick="sendMsg()">Enviar</button>
<div id="chatBox"></div>
</div>
</div>

<div class="ads">EspaÃ§o de anÃºncio premium</div>
<div class="ads">EspaÃ§o de anÃºncio premium</div>

</div>

<script>
function login(){
 let u=document.getElementById('user').value;
 if(u){
  localStorage.setItem('user',u);
  document.getElementById('login').style.display='none';
  document.getElementById('site').style.display='block';
 }
}

function logout(){localStorage.clear(); location.reload();}

function show(id){
 document.querySelectorAll('.section').forEach(s=>s.classList.remove('active'));
 document.getElementById(id).classList.add('active');
}

window.onload=function(){
 if(localStorage.getItem('user')){
  document.getElementById('login').style.display='none';
  document.getElementById('site').style.display='block';
  document.getElementById('nomeUser').innerText='UsuÃ¡rio: '+localStorage.getItem('user');
 }
}

function responder(){
 let p=document.getElementById('pergunta').value.toLowerCase();
 let r='Sem resposta ainda';
 if(p.includes('combo')) r='Use ataques rÃ¡pidos e combine habilidades.';
 document.getElementById('resposta').innerText=r;
}

function wikiResp(){
 document.getElementById('wikiResposta').innerText='Itens sÃ£o obtidos por bosses e eventos.';
}

function addTrade(){
 let t=document.getElementById('tradeInput').value;
 let p=document.createElement('p'); p.innerText=t;
 document.getElementById('tradesList').appendChild(p);
}

function addCrew(){
 let c=document.getElementById('crewInput').value;
 let p=document.createElement('p'); p.innerText=c;
 document.getElementById('crewList').appendChild(p);
}

function sendMsg(){
 let m=document.getElementById('msg').value;
 let p=document.createElement('p'); p.innerText=m;
 document.getElementById('chatBox').appendChild(p);
}
</script>

</body>
</html>
