<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chatbot sobre Switches</title>
    <style>
        body {
            background-color: #56a8fb; /* Fondo azul */
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            font-family: Arial, sans-serif;
        }

        .chat-container {
            background-color: #fff;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
            width: 1200px; /* Aumentar el ancho del contenedor del chat */
            max-width: 90%;
            display: flex;
            flex-direction: column;
        }

        .chat-header, .chat-footer {
            padding: 10px;
            background-color: #0073e6;
            color: white;
            text-align: center;
        }

        .chat-body {
            padding: 20px;
            overflow-y: auto;
            height: 700px; /* Aumentar la altura del contenedor del chat */
        }

        .message {
            margin: 10px 0;
            padding: 10px;
            border-radius: 5px;
        }

        .user-message {
            background-color: #0073e6;
            color: white;
            align-self: flex-end;
            max-width: 80%;
            font-size: 18px; /* Tamaño de fuente del mensaje del usuario */
        }

        .bot-message {
            background-color: #f1f1f1;
            color: black;
            align-self: flex-start;
            max-width: 80%;
            font-size: 18px; /* Tamaño de fuente del mensaje del bot */
        }

        .chat-footer input {
            width: calc(105% - 105px); /* Ajustar ancho del cuadro de texto */
            padding: 15px; /* Aumentar padding del cuadro de texto */
            border: 1px solid #ccc;
            border-radius: 5px;
            margin-right: 10px;
            font-size: 16px; /* Aumentar tamaño de fuente del cuadro de texto */
        }

        .chat-footer button {
            padding: 15px; /* Aumentar padding del botón */
            background-color: #a00404;
            border: none;
            color: white;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px; /* Aumentar tamaño de fuente del botón */
            width: 90px; /* Ajustar ancho del botón */
        }

        .chat-footer button:hover {
            background-color: #005bb5;
        }

        @keyframes ellipsis {
            0% { content: ''; }
            33% { content: '.'; }
            66% { content: '..'; }
            100% { content: '...'; }

        }

        .loading::after {
            content: '';
            animation: ellipsis 1s infinite;
        }

    </style>
</head>
<body>


    <div class="chat-container">
        <div class="chat-header">
            Chatbot FixedIP
        </div>
        <div class="chat-body" id="chat-body">
            <!-- Aquí aparecerán los mensajes -->
        </div>
        <div class="chat-footer">
            <input type="text" id="user-input" placeholder="Escribe tu pregunta aquí...">
            <button onclick="sendMessage()">Enviar</button>
        </div>
    </div>

    <script>
        function sendMessage() {
            const userInput = document.getElementById('user-input');
            const message = userInput.value.trim().toLowerCase();
            if (message === "") return;

            const chatBody = document.getElementById('chat-body');

            // Añadir mensaje del usuario
            const userMessage = document.createElement('div');
            userMessage.className = 'message user-message';
            userMessage.textContent = userInput.value.trim();
            chatBody.appendChild(userMessage);

            // Limpiar el input
            userInput.value = "";

             // Añadir animación de puntos suspensivos
             const botMessage = document.createElement('div');
            botMessage.className = 'message bot-message loading';
            botMessage.textContent = "Recopilando información";
            chatBody.appendChild(botMessage);

            // Desplazar el scroll hacia abajo
            chatBody.scrollTop = chatBody.scrollHeight;

            // Simular retraso del bot y añadir respuesta
            setTimeout(() => {
                // Eliminar animación de puntos suspensivos
                botMessage.classList.remove('loading');

           // Lógica de respuestas
           let response;
                switch (message) {
                    case "que es un switch?":
                        response = "Un switch, también conocido como conmutador en español, es un dispositivo de red utilizado para conectar varios dispositivos entre sí y permitirles comunicarse en una red local (LAN). El switch actúa como un intermediario entre los dispositivos, enviando los datos de un dispositivo a otro de manera eficiente y segura.";
                        break;
                    case "que es un router?":
                        response = "Un router es un dispositivo de red que se utiliza para conectar redes diferentes entre sí, como tu red local (LAN) a internet (WAN). Se encarga de dirigir el tráfico de datos entre las redes y encontrar la mejor ruta para que los datos lleguen a su destino.";
                        break;
                    case "que es una red lan?":
                        response = "Una red LAN (Local Area Network) es una red de computadoras que se extiende sobre un área geográfica limitada, como una casa, oficina o edificio. Permite que los dispositivos dentro de esa área se comuniquen y compartan recursos.";
                        break;
                    default:
                        response = "Lo siento, no entiendo la pregunta.";
                }

                botMessage.textContent = response;

                // Desplazar el scroll hacia abajo
                chatBody.scrollTop = chatBody.scrollHeight;
            }, 2000); // Retraso de 2 segundos
        }
    </script>
</body>
</html>
