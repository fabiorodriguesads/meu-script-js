<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Simulação de WhatsApp</title>
  <style>
    /* Estilos básicos para chat */
    #chat-box {
      width: 300px;
      max-height: 500px;
      border: 1px solid #ddd;
      padding: 10px;
      overflow-y: auto;
      background-color: #f0f0f0;
      font-family: Arial, sans-serif;
    }
    .message {
      padding: 8px;
      margin: 5px;
      border-radius: 5px;
      max-width: 80%;
    }
    .user-message {
      background-color: #dcf8c6;
      align-self: flex-end;
    }
    .bot-message {
      background-color: #ffffff;
      align-self: flex-start;
    }
    .typing {
      font-style: italic;
      color: #aaa;
    }
  </style>
</head>
<body>

<div id="chat-box"></div>

<script>
  // Sons para envio e recebimento de mensagens
  const sendSound = new Audio('sendSound.mp3');
  const receiveSound = new Audio('receiveSound.mp3');

  // Elemento do chat
  const chatBox = document.getElementById("chat-box");

  // Função para adicionar mensagens no chat
  function addMessage(content, sender = 'bot') {
    const message = document.createElement('div');
    message.classList.add('message', sender === 'user' ? 'user-message' : 'bot-message');
    message.innerText = content;
    chatBox.appendChild(message);
    chatBox.scrollTop = chatBox.scrollHeight; // Rolagem automática

    // Toca som de recebimento para mensagem do bot e de envio para o usuário
    if (sender === 'bot') receiveSound.play();
    if (sender === 'user') sendSound.play();
  }

  // Função para simular digitando
  function showTyping() {
    const typing = document.createElement('div');
    typing.classList.add('typing');
    typing.innerText = 'Digitando...';
    chatBox.appendChild(typing);
    chatBox.scrollTop = chatBox.scrollHeight;
    return typing;
  }

  // Função para remover o status de "digitando"
  function hideTyping(typingElement) {
    chatBox.removeChild(typingElement);
  }

  // Função para enviar uma mensagem do usuário
  function sendMessage(message) {
    addMessage(message, 'user');
  }

  // Simulação de interação (alterne para personalizar conforme necessário)
  function simulateChat() {
    sendMessage("Olá!"); // Mensagem do usuário

    // Simula a resposta após alguns segundos
    setTimeout(() => {
      const typing = showTyping(); // Exibe o "digitando..."
      
      // Remover "digitando..." e enviar mensagem do bot após um tempo
      setTimeout(() => {
        hideTyping(typing);
        addMessage("Oi! Como posso ajudar?");
      }, 2000);
    }, 1000);

    // Outra mensagem do usuário e resposta do bot
    setTimeout(() => {
      sendMessage("Gostaria de saber mais sobre seus serviços.");

      setTimeout(() => {
        const typing = showTyping();
        setTimeout(() => {
          hideTyping(typing);
          addMessage("Claro! Oferecemos várias opções.");
        }, 2000);
      }, 1000);
    }, 4000);
  }

  // Inicia a simulação do chat
  simulateChat();

</script>

</body>
</html>
