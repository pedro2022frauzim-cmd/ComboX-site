<!DOCTYPE html>
<html lang="pt-br">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ComboX - Gamer Hub</title>

<style>
body {
  font-family: Arial;
  margin: 0;
  background: linear-gradient(135deg,#0f0f0f,#1a1a1a);
  color: white;
}

header {
  background:#111;
  padding:20px;
  text-align:center;
  font-size:28px;
}

nav {
  background:#222;
  padding:10px;
  text-align:center;
}

nav button {
  margin:5px;
  padding:10px;
  background:#00ff88;
  border:none;
  border-radius:8px;
  cursor:pointer;
}

.section {display:none; padding:20px;}
.active {display:block;}

.ads {
  background:#222;
  padding:15px;
  margin:15px 0;
  border-radius:10px;
  text-align:center;
}

input, button {
  padding:10px;
  margin:5px;
  border-radius:8px;
  border:none;
}

#login {text-align:center; margin-top:100px;}
#site {display:none;}
</style>
</head>

<body>

<div id="login">
  <h2>ðŸ” Login ComboX</h2>
  <input id="user" placeholder="UsuÃ¡rio">
  <input id="pass" type="password" placeholder="Senha">
  <br>
  <button onclick="login()">Entrar</button>
</div>

<div id="site">
<header>ðŸ”¥ ComboX - Gamer Hub</header>

<nav>
<button onclick="show('dicas')">ðŸ’¡ Combos</button>
<button onclick="show('trades')">ðŸ’° Trades</button>
<button onclick="show('wiki')">ðŸ“– Wiki</button>
<button onclick="show('crew')">ðŸš¢ Crew</button>
<button onclick="show('perfil')">ðŸ‘¤ Perfil</button>
<button onclick="show('chat')">ðŸ’¬ Chat</button>
<button onclick="logout()">ðŸšª Sair</button>
</nav>

<div class="ads">ðŸ”¥ ANÃšNCIO TOPO</div>

<div id="dicas" class="section active">
<h2>IA de Combos</h2>
<input id="pergunta" placeholder="Pergunte algo...">
<button onclick="responder()">Perguntar</button>
<p id="resposta"></p>
</div>

<div id="trades" class="section">
<h2>Postar Trade</h2>
<input id="tradeInput" placeholder="Ex: Dragon por Leopard">
<button onclick="addTrade()">Postar</button>
<div id="tradesList"></div>
</div>

<div id="wiki" class="section">
<h2>Wiki / IA</h2>
<input id="wikiPergunta" placeholder="Como pegar item?">
<button onclick="wikiResp()">Perguntar</button>
<p id="wikiResposta"></p>
</div>

<div id="crew" class="section">
<h2>Divulgar Crew</h2>
<input id="crewInput" placeholder="Nome da crew">
<button onclick="addCrew()">Divulgar</button>
<div id="crewList"></div>
</div>

<div id="perfil" class="section">
<h2>Perfil</h2>
<p id="nomeUser"></p>
<h3>Ranking</h3>
<ol>
<li>TopPlayer - 2500</li>
<li>ProGamer - 2300</li>
<li>NoobMaster - 2000</li>
</ol>
</div>

<div id="chat" class="section">
<h2>Chat</h2>
<input id="msg" placeholder="Mensagem...">
<button onclick="sendMsg()">Enviar</button>
<div id="chatBox"></div>
</div>

<div class="ads">ðŸ”¥ ANÃšNCIO MEIO</div>

<div class="ads">ðŸ”¥ ANÃšNCIO FINAL</div>

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
 let r='NÃ£o sei ainda';
 if(p.includes('combo')) r='Use combos rÃ¡pidos e frutas fortes';
 document.getElementById('resposta').innerText=r;
}

function wikiResp(){
 let p=document.getElementById('wikiPergunta').value.toLowerCase();
 let r='Procure bosses ou raids';
 document.getElementById('wikiResposta').innerText=r;
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
