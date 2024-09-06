<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Treino de Divisão - 4º Ano</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            margin: 0;
            padding: 20px;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            flex-direction: column;
        }
        h1 {
            color: #333;
        }
        .container {
            background-color: #fff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
            max-width: 600px;
            width: 100%;
            text-align: center;
        }
        .question-container {
            margin-top: 20px;
        }
        .result {
            margin-top: 10px;
            padding: 10px;
            border-radius: 5px;
        }
        .correct {
            background-color: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }
        .incorrect {
            background-color: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
        }
        .explanation {
            margin-top: 10px;
            text-align: left;
            font-size: 0.9rem;
            color: #555;
            background-color: #f1f1f1;
            padding: 10px;
            border-radius: 5px;
            border: 1px solid #ccc;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Treino de Divisão - 4º Ano</h1>
        <button id="generateDivisionButton">Gerar Divisão</button>

        <div id="questions" class="question-container"></div>
    </div>

    <script>
        const generateDivisionButton = document.getElementById('generateDivisionButton');
        const questionsContainer = document.getElementById('questions');

        function gerarDivisaoFacil() {
            const divisor = Math.floor(Math.random() * 9) + 2; // Divisores entre 2 e 10
            const quociente = Math.floor(Math.random() * 10) + 1; // Quocientes entre 1 e 10
            const dividendo = divisor * quociente;

            return { dividendo, divisor, quociente };
        }

        function criarPergunta(dividendo, divisor, quociente) {
            const container = document.createElement('div');
            container.classList.add('question-container');

            const label = document.createElement('label');
            label.textContent = `Quanto é ${dividendo} ÷ ${divisor}?`;
            container.appendChild(label);

            const input = document.createElement('input');
            input.type = 'number';
            input.step = 'any';
            container.appendChild(input);

            const button = document.createElement('button');
            button.textContent = 'Enviar';
            button.onclick = function () {
                const resposta = parseFloat(input.value);
                const resultado = document.createElement('div');
                resultado.classList.add('result');
                const explicacaoDiv = document.createElement('div');
                explicacaoDiv.classList.add('explanation');
                explicacaoDiv.innerHTML = `Passo a passo:<br>
                1. Dividendo: ${dividendo}<br>
                2. Divisor: ${divisor}<br>
                3. Quociente (resultado da divisão) = ${dividendo} ÷ ${divisor} = ${quociente}`;

                if (resposta === quociente) {
                    resultado.textContent = `Correto! ${dividendo} ÷ ${divisor} = ${quociente}.`;
                    resultado.classList.add('correct');
                } else {
                    resultado.textContent = `Incorreto. ${dividendo} ÷ ${divisor} = ${quociente}.`;
                    resultado.classList.add('incorrect');
                }

                container.appendChild(resultado);
                container.appendChild(explicacaoDiv);
                button.disabled = true;  // Desabilita o botão após resposta
            };
            container.appendChild(button);

            questionsContainer.appendChild(container);
        }

        generateDivisionButton.onclick = function () {
            questionsContainer.innerHTML = '';  // Limpar perguntas anteriores

            const { dividendo, divisor, quociente } = gerarDivisaoFacil();

            criarPergunta(dividendo, divisor, quociente);
        };
    </script>
</body>
</html>
