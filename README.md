<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>10de10 - IA Programadora</title>
<style>
body { margin:0; font-family:sans-serif; display:flex; height:100vh; overflow:hidden; }
#chat { width:30%; background:#f4f4f4; border-right:2px solid #ccc; padding:10px; display:flex; flex-direction:column; }
#chatMessages { flex:1; overflow-y:auto; margin-bottom:10px; }
.message { background:#007BFF; color:white; padding:8px 12px; border-radius:12px; margin-bottom:8px; max-width:90%; }
.message.user { background:#28a745; align-self:flex-end; }
#inputContainer { display:flex; }
#inputContainer input { flex:1; padding:8px; border-radius:8px; border:1px solid #ccc; }
#inputContainer button { padding:8px 12px; margin-left:5px; border-radius:8px; border:none; background:#007BFF; color:white; cursor:pointer; }
#sitePreview { flex:1; border:none; }
</style>
</head>
<body>

<div id="chat">
  <div id="chatMessages"></div>
  <div id="inputContainer">
    <input type="text" id="userInput" placeholder="Digite seu comando...">
    <button onclick="sendMessage()">Enviar</button>
    <button onclick="publishGitHub()">Publicar</button>
  </div>
</div>

<iframe id="sitePreview"></iframe>

<script>
let siteCode = `<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Site 10de10</title>
<style>body{font-family:sans-serif;padding:20px;} h1{color:#007BFF;}</style>
</head>
<body>
<h1>Bem-vindo ao site 10de10!</h1>
<p>Aqui a IA gera seu site em tempo real.</p>
</body>
</html>`;

const chatMessages = document.getElementById('chatMessages');
const sitePreview = document.getElementById('sitePreview');

function updatePreview(){ sitePreview.srcdoc = siteCode; }

function sendMessage(){
  const input = document.getElementById('userInput');
  const text = input.value.trim();
  if(!text) return;

  const userMsg = document.createElement('div');
  userMsg.className='message user';
  userMsg.textContent = text;
  chatMessages.appendChild(userMsg);

  const iaMsg = document.createElement('div');
  iaMsg.className='message';
  iaMsg.textContent = "Gerando código do site...";
  chatMessages.appendChild(iaMsg);

  setTimeout(()=>{
    siteCode = `<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Site 10de10</title>
<style>body{font-family:sans-serif;padding:20px;} h1{color:#007BFF;}</style>
</head>
<body>
<h1>${text}</h1>
<p>Site gerado em tempo real pela 10de10!</p>
</body>
</html>`;
    updatePreview();
    iaMsg.textContent="Site atualizado!";
  },1000);

  input.value='';
  chatMessages.scrollTop = chatMessages.scrollHeight;
}

// Função para publicar no GitHub via API
async function publishGitHub(){
  const token = prompt("Digite seu GitHub Personal Access Token:");
  const repo = prompt("Digite o nome do repositório (ex: 10de10-sites):");
  const path = prompt("Digite o nome do arquivo (ex: index.html):");

  const content = btoa(unescape(encodeURIComponent(siteCode))); // Base64
  const data = { message: "Publicando site via 10de10", content };

  const response = await fetch(`https://api.github.com/repos/YOUR_USERNAME/${repo}/contents/${path}`, {
    method: "PUT",
    headers: {
      "Authorization": `token ${token}`,
      "Content-Type": "application/json"
    },
    body: JSON.stringify(data)
  });

  if(response.ok) alert("Site publicado com sucesso!");
  else alert("Erro ao publicar. Verifique token e repo.");
}

updatePreview();
</script>

</body>
</html>const userMsg = document.createElement('div');
userMsg.className='message user';
userMsg.textContent = text;
chatMessages.appendChild(userMsg);

