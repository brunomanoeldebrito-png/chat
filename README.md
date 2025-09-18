# chat
ia
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <title>IA Programadora</title>
  <style>
    body { font-family: Arial, sans-serif; background: #111; color: #eee; margin: 0; padding: 0; }
    .container { max-width: 800px; margin: auto; padding: 20px; }
    h1 { text-align: center; color: #0f0; }
    #chat {
      background: #222; border-radius: 10px; padding: 20px;
      height: 400px; overflow-y: auto; margin-bottom: 15px;
    }
    .msg { margin: 10px 0; padding: 10px; border-radius: 8px; }
    .user { background: #0055aa; text-align: right; }
    .bot { background: #333; color: #0f0; }
    input, button {
      padding: 10px; border: none; border-radius: 5px;
    }
    input { width: 70%; }
    button { background: #0f0; color: #000; cursor: pointer; font-weight: bold; }
    button:hover { background: #0c0; }
  </style>
</head>
<body>
  <div class="container">
    <h1>🤖 IA Programadora</h1>
    <div id="chat"></div>
    <input type="text" id="pergunta" placeholder="Digite sua pergunta...">
    <button onclick="enviar()">Enviar</button>
  </div>

  <script>
    const chat = document.getElementById("chat");

    function adicionarMensagem(texto, classe) {
      const div = document.createElement("div");
      div.className = "msg " + classe;
      div.textContent = texto;
      chat.appendChild(div);
      chat.scrollTop = chat.scrollHeight;
    }

    function falar(texto) {
      const fala = new SpeechSynthesisUtterance(texto);
      fala.lang = "pt-BR";
      fala.voice = speechSynthesis.getVoices().find(v => v.name.includes("Google") || v.name.includes("Siri")) || null;
      speechSynthesis.speak(fala);
    }

    function enviar() {
      const input = document.getElementById("pergunta");
      const pergunta = input.value.trim();
      if (!pergunta) return;

      adicionarMensagem(pergunta, "user");
      input.value = "";

      // Resposta provisória (simulando uma IA super inteligente)
      let resposta = "";

      if (pergunta.toLowerCase().includes("html")) {
        resposta = "Aqui está um exemplo básico de HTML:\n\n<!DOCTYPE html><html><head><title>Exemplo</title></head><body><h1>Olá Mundo!</h1></body></html>";
      } else if (pergunta.toLowerCase().includes("java")) {
        resposta = "Aqui está um exemplo básico em Java:\n\npublic class Main {\n  public static void main(String[] args) {\n    System.out.println(\"Olá, Mundo!\");\n  }\n}";
      } else {
        resposta = "Sou sua IA programadora 🚀. Posso gerar códigos super rápidos em HTML, Java, JS, Python e muito mais!";
      }

      adicionarMensagem(resposta, "bot");
      falar(resposta);
    }
  </script>
</body>
</html>
