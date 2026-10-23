<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mi Emprendimiento - Sitio Oficial</title>
    <style>
        /* Estilos generales de la página */
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f4f4f9;
            color: #333;
        }
        header {
            background-color: #2c3e50;
            color: white;
            text-align: center;
            padding: 2rem;
        }
        main {
            padding: 2rem;
            max-width: 800px;
            margin: 0 auto;
        }
        .card {
            background: white;
            padding: 1.5rem;
            border-radius: 8px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
            margin-bottom: 1rem;
        }

        /* Estilos del Chatbot */
        #chat-button {
            position: fixed;
            bottom: 20px;
            right: 20px;
            background-color: #25d366;
            color: white;
            border: none;
            border-radius: 50%;
            width: 60px;
            height: 60px;
            font-size: 24px;
            cursor: pointer;
            box-shadow: 0 4px 8px rgba(0,0,0,0.2);
        }
        #chat-box {
            display: none;
            position: fixed;
            bottom: 90px;
            right: 20px;
            width: 300px;
            height: 400px;
            background-color: white;
            border-radius: 10px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.2);
            flex-direction: column;
            overflow: hidden;
        }
        .chat-header {
            background-color: #2c3e50;
            color: white;
            padding: 10px;
            text-align: center;
            font-weight: bold;
        }
        .chat-content {
            flex: 1;
            padding: 10px;
            overflow-y: auto;
            display: flex;
            flex-direction: column;
            gap: 8px;
        }
        .msg {
            padding: 8px 12px;
            border-radius: 15px;
            max-width: 80%;
            font-size: 14px;
        }
        .bot-msg {
            background-color: #e9ecef;
            align-self: flex-start;
        }
        .user-msg {
            background-color: #007bff;
            color: white;
            align-self: flex-end;
        }
        .chat-input {
            display: flex;
            border-top: 1px solid #ccc;
        }
        .chat-input input {
            flex: 1;
            padding: 10px;
            border: none;
            outline: none;
        }
        .chat-input button {
            background-color: #2c3e50;
            color: white;
            border: none;
            padding: 10px 15px;
            cursor: pointer;
        }
    </style>
</head>
<body>

    <header>
        <h1>Bienvenido a Mi Emprendimiento</h1>
        <p>Soluciones innovadoras para nuestros clientes</p>
    </header>

    <main>
        <div class="card">
            <h2>Sobre Nosotros</h2>
            <p>Somos un emprendimiento enfocado en brindar la mejor atención y productos de calidad.</p>
        </div>
        <div class="card">
            <h2>Nuestros Servicios</h2>
            <ul>
                <li>Atención personalizada</li>
                <li>Envíos rápidos</li>
                <li>Asesoría continua</li>
            </ul>
        </div>
    </main>

    <!-- Botón Flotante del Chatbot -->
    <button id="chat-button" onclick="toggleChat()">💬</button>

    <!-- Ventana del Chatbot -->
    <div id="chat-box">
        <div class="chat-header">Asistente Virtual</div>
        <div class="chat-content" id="chat-content">
            <div class="msg bot-msg">¡Hola! 👋 ¿En qué te puedo ayudar hoy? Escribe "productos", "horarios" o "contacto".</div>
        </div>
        <div class="chat-input">
            <input type="text" id="user-input" placeholder="Escribe tu consulta..." onkeypress="handleKey(event)">
            <button onclick="sendMessage()">Enviar</button>
        </div>
    </div>

    <script>
        function toggleChat() {
            const chatBox = document.getElementById('chat-box');
            chatBox.style.display = (chatBox.style.display === 'flex') ? 'none' : 'flex';
        }

        function handleKey(event) {
            if (event.key === 'Enter') sendMessage();
        }

        function sendMessage() {
            const input = document.getElementById('user-input');
            const content = document.getElementById('chat-content');
            const text = input.value.trim();

            if (text === "") return;

            // Mostrar mensaje del usuario
            const userDiv = document.createElement('div');
            userDiv.className = 'msg user-msg';
            userDiv.textContent = text;
            content.appendChild(userDiv);

            input.value = "";

            // Lógica de respuestas del Chatbot
            setTimeout(() => {
                const botDiv = document.createElement('div');
                botDiv.className = 'msg bot-msg';
                const lowerText = text.toLowerCase();

                if (lowerText.includes("hola")) {
                    botDiv.textContent = "¡Hola! ¿Qué tal? ¿En qué te puedo asesorar?";
                } else if (lowerText.includes("producto") || lowerText.includes("servicios")) {
                    botDiv.textContent = "Ofrecemos productos y servicios personalizados para cada cliente.";
                } else if (lowerText.includes("horario")) {
                    botDiv.textContent = "Atendemos de Lunes a Viernes de 09:00 a 18:00.";
                } else if (lowerText.includes("contacto") || lowerText.includes("telefono")) {
                    botDiv.textContent = "Puedes contactarnos vía WhatsApp o dejarnos tus datos.";
                } else {
                    botDiv.textContent = "Gracias por escribirnos. Pronto un asesor tomará tu solicitud.";
                }

                content.appendChild(botDiv);
                content.scrollTop = content.scrollHeight;
            }, 500);
        }
    </script>
</body>
</html>
