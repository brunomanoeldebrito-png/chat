<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>10de10 V0 - IA Programadora</title>
<style>
body{margin:0;font-family:sans-serif;display:flex;height:100vh;overflow:hidden;}
#chat{width:30%;background:#f4f4f4;border-right:2px solid #ccc;padding:10px;display:flex;flex-direction:column;}
#chatMessages{flex:1;overflow-y:auto;margin-bottom:10px;padding-right:5px;scroll-behavior:smooth;}
.message{background:#007BFF;color:white;padding:8px 12px;border-radius:12px;margin-bottom:8px;max-width:90%;}
.message.user{background:#28a745;align-self:flex-end;}
#inputContainer{display:flex;}
#inputContainer input{flex:1;padding:8px;border-radius:8px;border:1px solid #ccc;}
#inputContainer button{padding:8px 12px;margin-left:5px;border-radius:8px;border:none;background:#007BFF;color:white;cursor:pointer;}
#sitePreview{flex:1;border:none;}
</style>
</head>
<body>

<div id="chat">
  <div id="chatMessages"></div>
  <div id="inputContainer">
    <input type="text" id="userInput" placeholder="Descreva o site que deseja...">
    <button onclick="sendMessage()">Enviar</button>
    <button onclick="publishGitHub()">Publicar</button>
  </div>
</div>

<iframe id="sitePreview"></iframe>

<script>
let siteCode = `<!DOCTYPE html>
<html lang="pt-BR">
<head><meta charset="UTF-8"><meta name="viewport" content="width=device-width, initial-scale=1.0"><title>Site 10de10</title><style>body{font-family:sans-serif;padding:20px;} h1{color:#007BFF;}</style></head>
<body><h1>Bem-vindo ao site 10de10 V0!</h1><p>Aqui a IA gera seu site inteligente em tempo real.</p></body></html>`;

const chatMessages=document.getElementById('chatMessages');
const sitePreview=document.getElementById('sitePreview');

function updatePreview(){ sitePreview.srcdoc=siteCode; }
function addMessage(user,text){ const msg=document.createElement('div'); msg.className='message'+(user?' user':''); msg.textContent=text; chatMessages.appendChild(msg); chatMessages.scrollTop=chatMessages.scrollHeight; }

function sendMessage(){
  const input=document.getElementById('userInput');
  const text=input.value.trim();
  if(!text)return;
  addMessage(true,text);
  addMessage(false,"Gerando site inteligente...");
  
  // Aqui você pode integrar GPT API ou Replit AI para gerar o código real
  setTimeout(()=>{
    siteCode=`<!DOCTYPE html>
<html lang="pt-BR"><head><meta charset="UTF-8"><meta name="viewport" content="width=device-width, initial-scale=1.0"><title>Site 10de10 V0</title><style>body{font-family:sans-serif;padding:20px;} h1{color:#007BFF;}</style></head>
<body>
<h1>${text}</h1>
<p>Site gerado de forma inteligente pela 10de10 V0!</p>
</body></html>`;
    updatePreview();
    addMessage(false,"Site atualizado com sucesso!");
  },1000);
  input.value='';
}

async function publishGitHub(){
  const token=prompt("Digite seu GitHub Personal Access Token:");
  const username=prompt("Digite seu usuário GitHub:");
  const repo=prompt("Digite o nome do repositório:");
  const path=prompt("Nome do arquivo (ex: index.html):");
  const content=btoa(unescape(encodeURIComponent(siteCode)));
  const data={message:"Publicando site via 10de10 V0",content};
  const response=await fetch(`https://api.github.com/repos/${username}/${repo}/contents/${path}`,{
    method:"PUT",
    headers:{ "Authorization":`token ${token}`,"Content-Type":"application/json" },
    body:JSON.stringify(data)
  });
  if(response.ok) alert("Site publicado com sucesso!");
  else alert("Erro ao publicar. Verifique token, usuário e repo.");
}

updatePreview();
</script>

</body>
</html>
