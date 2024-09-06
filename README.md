<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Treino de Divisão - 3º Ano</title>
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
            max-width: 800px;
            width: 100%;
            text-align: center;
        }
        .question-container {
            margin-top: 20px;
            text-align: left;
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
        button {
            margin-top: 20px;
            padding: 10px 15px;
            border: none;
            background-color: #007bff;
            color: #fff;
            border-radius: 5px;
            cursor: pointer;
            font-size: 1rem;
        }
        button:disabled {
            background-color: #ccc;
            cursor: not-allowed;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Treino de Divisão - 3º Ano - Esther Edler</h1>
        <button id="generateDivisionButton">Gerar Questões</button>

        <div id="questions" class="question-container"></div>
        <button id="checkAnswersButton" style="display: none;">Conferir Respostas</button>
    </div>

    <script>
        const generateDivisionButton = document.getElementById('generateDivisionButton');
        const checkAnswersButton = document.getElementById('checkAnswersButton');
        const questionsContainer = document.getElementById('questions');

        function gerarProblemaAleatorio() {
            const divisores = [2, 3, 4, 5, 6, 7, 8, 9, 10]; // Divisores possíveis
            const divisor = divisores[Math.floor(Math.random() * divisores.length)];
            const quociente = Math.floor(Math.random() * 10) + 1; // Quocientes entre 1 e 10
            const dividendo = divisor * quociente;

            const contextos = [
                `Carlos tem ${dividendo} carrinhos de brinquedo e quer dividir igualmente entre seus ${divisor} amigos. Quantos carrinhos cada amigo vai receber?`,
                `Luiza comprou ${dividendo} bolas para brincar e quer dividir igualmente entre seus ${divisor} colegas. Quantas bolas cada colega vai receber?`,
                `Ana tem ${dividendo} chocolates para dar aos seus ${divisor} irmãos. Se ela dividir igualmente entre todos, quantos chocolates cada irmão receberá?`,
                `Em uma festa, havia ${dividendo} lanches para serem divididos igualmente entre ${divisor} crianças. Quantos lanches cada criança irá receber?`,
                `Uma biblioteca recebeu ${dividendo} livros novos e quer distribuir igualmente entre ${divisor} escolas. Quantos livros cada escola receberá?`,
                `Marcos comprou ${dividendo} maçãs para distribuir igualmente entre ${divisor} famílias. Quantas maçãs cada família receberá?`,
                `Em uma festa, havia ${dividendo} doces para serem divididos igualmente entre ${divisor} crianças. Quantos doces cada criança receberá?`
            ];

            const problema = contextos[Math.floor(Math.random() * contextos.length)];

            return { problema, quociente };
        }

        function criarProblema(problema, index) {
            const container = document.createElement('div');
            container.classList.add('question-container');

            const label = document.createElement('label');
            label.textContent = `Problema ${index + 1}: ${problema.problema}`;
            container.appendChild(label);

            const input = document.createElement('input');
            input.type = 'number';
            input.step = 'any';
            input.dataset.quociente = problema.quociente;
            container.appendChild(input);

            questionsContainer.appendChild(container);
        }

        generateDivisionButton.onclick = function () {
            questionsContainer.innerHTML = '';  // Limpar perguntas anteriores
            checkAnswersButton.style.display = 'block'; // Mostrar botão de conferir respostas
            checkAnswersButton.disabled = false;

            for (let i = 0; i < 7; i++) {  // Gerar 7 problemas aleatórios
                const problema = gerarProblemaAleatorio();
                criarProblema(problema, i);
            }
        };

        checkAnswersButton.onclick = function () {
            const inputs = questionsContainer.querySelectorAll('input');

            inputs.forEach((input, index) => {
                const quocienteCorreto = parseFloat(input.dataset.quociente);
                const resposta = parseFloat(input.value);
                const resultado = document.createElement('div');
                resultado.classList.add('result');
                const explicacaoDiv = document.createElement('div');
                explicacaoDiv.classList.add('explanation');
                explicacaoDiv.innerHTML = `Passo a passo:<br>
                1. Total de itens: ${quocienteCorreto * input.dataset.divisor}<br>
                2. Número de pessoas: ${input.dataset.divisor}<br>
                3. Cada um recebe: ${quocienteCorreto}`;

                if (resposta === quocienteCorreto) {
                    resultado.textContent = `Correto! Cada um receberá ${quocienteCorreto} itens.`;
                    resultado.classList.add('correct');
                } else {
                    resultado.textContent = `Incorreto. Cada um receberá ${quocienteCorreto} itens.`;
                    resultado.classList.add('incorrect');
                }

                input.parentElement.appendChild(resultado);
                input.parentElement.appendChild(explicacaoDiv);
                input.disabled = true;  // Desabilita o input após resposta
            });

            checkAnswersButton.disabled = true;  // Desabilita o botão após a verificação
        };
    </script>
</body>
</html>
