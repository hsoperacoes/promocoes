<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <title>Formulário de Produto</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 40px;
            line-height: 1.6;
        }
        
        h1 {
            color: #2c3e50;
        }

        form {
            max-width: 400px;
            padding: 20px;
            border: 1px solid #ddd;
            border-radius: 5px;
            background: #f9f9f9;
        }

        label {
            display: block;
            margin-top: 15px;
            font-weight: bold;
            color: #34495e;
        }

        input[type="text"] {
            width: 100%;
            padding: 10px;
            margin-top: 5px;
            border: 1px solid #ddd;
            border-radius: 4px;
            box-sizing: border-box;
        }

        button {
            margin-top: 25px;
            padding: 10px 15px;
            background-color: #3498db;
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 16px;
            transition: background-color 0.3s;
        }

        button:hover {
            background-color: #2980b9;
        }

        #statusMessage {
            margin-top: 20px;
            padding: 10px;
            border-radius: 4px;
            display: none;
        }

        .success {
            background-color: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }

        .error {
            background-color: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
        }
    </style>
</head>
<body>
    <h1>Cadastro de Produto</h1>
    <form id="produtoForm">
        <label for="referencia">Referência (4 caracteres):</label>
        <input type="text" id="referencia" name="referencia" maxlength="4" required pattern="[A-Za-z0-9]{4}" title="4 caracteres alfanuméricos">

        <label for="cor">Cor (6 caracteres):</label>
        <input type="text" id="cor" name="cor" maxlength="6" required pattern="[A-Za-z0-9]{6}" title="6 caracteres alfanuméricos">

        <label for="tamanho">Tamanho (4 caracteres):</label>
        <input type="text" id="tamanho" name="tamanho" maxlength="4" required pattern="[A-Za-z0-9]{4}" title="4 caracteres alfanuméricos">

        <label for="colecao">Coleção (3 caracteres):</label>
        <input type="text" id="colecao" name="colecao" maxlength="3" required pattern="[A-Za-z0-9]{3}" title="3 caracteres alfanuméricos">

        <button type="submit">Enviar</button>
    </form>

    <div id="statusMessage"></div>

    <script>
        document.getElementById("produtoForm").addEventListener("submit", function(e) {
            e.preventDefault();
            
            // Mostrar estado de carregamento
            const button = e.target.querySelector("button");
            const originalButtonText = button.textContent;
            button.textContent = "Enviando...";
            button.disabled = true;
            
            const statusMessage = document.getElementById("statusMessage");
            statusMessage.style.display = "none";
            
            // Coletar dados do formulário
            const formData = {
                referencia: document.getElementById("referencia").value,
                cor: document.getElementById("cor").value,
                tamanho: document.getElementById("tamanho").value,
                colecao: document.getElementById("colecao").value,
                timestamp: new Date().toISOString()  // Adiciona data/hora automática
            };

            // URL do seu Web App do Google Apps Script
            const url = "https://script.google.com/macros/s/AKfycby8JDGTDAy8CzbnDqQL7qVPJoSMagVjBrzKXQI_ICOw3coEoB-8oz1E2Uoc2Yj1NGqP/exec";
            
            // Enviar dados
            fetch(url, {
                method: "POST",
                headers: {
                    "Content-Type": "application/x-www-form-urlencoded",
                },
                body: new URLSearchParams(formData).toString()
            })
            .then(response => {
                if (!response.ok) throw new Error("Erro na rede");
                return response.text();
            })
            .then(data => {
                // Sucesso
                statusMessage.textContent = "Cadastro enviado com sucesso!";
                statusMessage.className = "success";
                statusMessage.style.display = "block";
                
                // Limpar formulário
                e.target.reset();
            })
            .catch(error => {
                // Erro
                console.error("Erro ao enviar:", error);
                statusMessage.textContent = "Erro ao enviar os dados. Por favor, tente novamente.";
                statusMessage.className = "error";
                statusMessage.style.display = "block";
            })
            .finally(() => {
                // Restaurar botão
                button.textContent = originalButtonText;
                button.disabled = false;
            });
        });
    </script>
</body>
</html>
