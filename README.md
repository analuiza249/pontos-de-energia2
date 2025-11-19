<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <title>Mapa Interativo – Feira de Ciências</title>

    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            gap: 20px;
            padding: 20px;
            background: #f3f3f3;
            overflow-x: hidden;
        }

        .container {
            display: flex;
            gap: 20px;
            width: 100%;
        }

        .painel {
            width: 300px;
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
        }

        /* MAPA — SOMENTE O TAMANHO ALTERADO */
        .mapa {
            width: 1500px;   /* AUMENTADO PARA CABER TUDO */
            height: 1000px;  /* AUMENTADO PARA AS ESTANDES DE BAIXO */
            background: #ffffff;
            border: 2px solid black;
            border-radius: 10px;
            position: relative;
            overflow: hidden;
        }

        .inicio {
            width: 18px;
            height: 18px;
            background: #007bff;
            position: absolute;
            transform: translate(-50%, -50%);
            border-radius: 3px;
            z-index: 999;
        }

        .inicio-label {
            position: absolute;
            font-size: 14px;
            font-weight: bold;
            color: #004b9b;
            transform: translate(-50%, -160%);
            z-index: 999;
        }

        .ponto {
            width: 22px;
            height: 22px;
            background: red;
            border-radius: 50%;
            position: absolute;
            transform: translate(-50%, -50%);
            z-index: 900;
        }

        .estande {
            position: absolute;
            text-align: center;
            width: 150px;
            transform: translate(-50%, -50%);
        }

        .estande img {
            width: 150px;
            height: 150px;
            object-fit: cover;
            border: 2px solid #aaa;
            border-radius: 10px;
        }

        .estande h3 {
            margin: 0;
            margin-bottom: 5px;
            font-size: 16px;
            font-weight: bold;
        }

        input, button, label {
            width: 100%;
        }

        input {
            padding: 6px;
            margin-bottom: 10px;
        }

        button {
            padding: 10px;
            border: none;
            background: #007bff;
            color: white;
            font-size: 16px;
            border-radius: 8px;
            cursor: pointer;
        }

        button:hover {
            background: #0056c2;
        }

        #resultado {
            margin-top: 10px;
            padding: 10px;
            background: #eee;
            border-radius: 6px;
        }
    </style>
</head>

<body>
<div class="container">

    <!-- PAINEL LATERAL -->
    <div class="painel">
        <h2>Consultar Estande</h2>

        <label>Nome do estande:</label>
        <input type="text" id="nomeConsulta" placeholder="Ex: Biologia">

        <button onclick="consultar()">Consultar</button>
        <div id="resultado"></div>

        <hr>

        <h2>Editar Coordenadas</h2>

        <label>X:</label>
        <input type="number" id="coordX" placeholder="Ex: 200">

        <label>Y:</label>
        <input type="number" id="coordY" placeholder="Ex: 150">

        <button onclick="moverPonto()">Mover Ponto</button>
    </div>

    <!-- MAPA -->
    <div class="mapa" id="mapa">

        <div class="inicio" id="inicio" style="left:100px; top:100px;"></div>
        <div class="inicio-label" id="inicioLabel" style="left:100px; top:100px;">Início</div>

        <div class="ponto" id="ponto" style="left:100px; top:100px;"></div>

        <div class="estande" id="Estande-Biologia" style="left:200px; top:150px;">
            <h3>Biologia</h3>
            <img src="biologia.png">
        </div>

        <div class="estande" id="Estande-Química" style="left:700px; top:150px;">
            <h3>Química</h3>
            <img src="quimica.png">
        </div>

        <div class="estande" id="Estande-Robótica" style="left:200px; top:500px;">
            <h3>Robótica</h3>
            <img src="robotica.png">
        </div>

        <div class="estande" id="Estande-Matemática" style="left:700px; top:500px;">
            <h3>Matemática</h3>
            <img src="matematica.png">
        </div>

    </div>
</div>

<script>

    function removerAcentos(texto) {
        return texto.normalize("NFD").replace(/[\u0300-\u036f]/g, "").toLowerCase();
    }

    const pontos = [
        { nome: "Biologia", x: 200, y: 150 },
        { nome: "Química", x: 700, y: 150 },
        { nome: "Robótica", x: 200, y: 500 },
        { nome: "Matemática", x: 700, y: 500 }
    ];

    function consultar() {
        let nomeDigitado = document.getElementById("nomeConsulta").value.trim();
        let nomeLimpo = removerAcentos(nomeDigitado);
        let resultado = document.getElementById("resultado");

        let encontrado = pontos.find(p => removerAcentos(p.nome) === nomeLimpo);

        if (!encontrado) {
            resultado.innerHTML = "❌ Estande não encontrada.";
            return;
        }

        resultado.innerHTML = `
            <strong>Estande:</strong> ${encontrado.nome}<br>
            <strong>Coordenadas:</strong> X=${encontrado.x} | Y=${encontrado.y}
        `;
    }

    function moverPonto() {
        let x = parseInt(document.getElementById("coordX").value);
        let y = parseInt(document.getElementById("coordY").value);

        if (isNaN(x) || isNaN(y)) return;

        const ponto = document.getElementById("ponto");
        ponto.style.left = x + "px";
        ponto.style.top = y + "px";
    }

</script>

</body>
</html>
