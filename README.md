<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <title>Formulário de Produto</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 40px;
        }

        form {
            max-width: 400px;
        }

        label {
            display: block;
            margin-top: 15px;
        }

        input[type="text"] {
            width: 100%;
            padding: 8px;
            margin-top: 5px;
        }

        button {
            margin-top: 20px;
            padding: 10px 15px;
        }
    </style>
</head>
<body>
    <h1>Cadastro de Produto</h1>
    <form>
        <label for="referencia">Referência (4 caracteres):</label>
        <input type="text" id="referencia" name="referencia" maxlength="4" required>

        <label for="cor">Cor (6 caracteres):</label>
        <input type="text" id="cor" name="cor" maxlength="6" required>

        <label for="tamanho">Tamanho (4 caracteres):</label>
        <input type="text" id="tamanho" name="tamanho" maxlength="4" required>

        <label for="colecao">Coleção (3 caracteres):</label>
        <input type="text" id="colecao" name="colecao" maxlength="3" required>

        <button type="submit">Enviar</button>
    </form>

    <script>
        document.querySelector("form").addEventListener("submit", function(e) {
            e.preventDefault();

            const formData = new FormData(e.target);
            const url = "https://script.google.com/macros/s/AKfycbyREaVkidCyyFiZ8TEgdEp_8yuY3XaO86bqCn_YSGrDWmIN-EizujGmTd5BfcL52zXX/exec";

            fetch(url, {
                method: "POST",
                body: formData
            })
            .then(response => response.text())
            .then(data => {
                alert("Cadastro enviado com sucesso!");
                e.target.reset();
            })
            .catch(error => {
                console.error("Erro ao enviar:", error);
                alert("Erro ao enviar os dados.");
            });
        });
    </script>
</body>
</html>
