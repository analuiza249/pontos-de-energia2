<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<title>Mapa Interativo – Feira de Ciências</title>

<style>

    body {
        font-family: Arial, sans-serif;
        background: #eef1f5;
        margin: 0;
        padding: 20px;
        display: flex;
        gap: 20px;
    }

    .container {
        display: flex;
        gap: 20px;
        width: 100%;
    }

    .painel {
        width: 320px;
        background: white;
        padding: 25px;
        border-radius: 12px;
        box-shadow: 0 4px 15px rgba(0,0,0,0.15);
    }

    .painel h2 {
        margin-top: 0;
        font-size: 20px;
        color: #333;
        border-left: 4px solid #007bff;
        padding-left: 10px;
    }

    hr {
        border: none;
        border-top: 1px solid #ddd;
        margin: 20px 0;
    }

    label {
        font-weight: bold;
        margin-top: 10px;
        display: block;
        color: #333;
    }

    input {
        width: 100%;
        padding: 10px;
        border-radius: 6px;
        border: 1px solid #bbb;
        margin-top: 5px;
        margin-bottom: 15px;
        font-size: 15px;
    }

    button {
        width: 100%;
        padding: 12px;
        border: none;
        color: white;
        background: #007bff;
        border-radius: 8px;
        font-size: 16px;
        cursor: pointer;
        margin-top: 5px;
    }

    button:hover {
        background: #0056c2;
    }

    #resultado {
        margin-top: 15px;
        padding: 12px;
        background: #f5f5f5;
        border-radius: 8px;
        font-size: 14px;
    }

    /********** MAPA ATUALIZADO **********/
    .mapa {
        width: 1350px;   /* AUMENTADO PARA CABER AS ESTANDES */
        height: 900px;   /* AUMENTADO PARA AS ESTANDES DE BAIXO NÃO SAÍREM */
        background: #ffffff;
        border: 3px solid #000;
        border-radius: 15px;
        position: relative;

        overflow: visible; /* garante que nada fique cortado */

        box-shadow: 0 4px 15px rgba(0,0,0,0.15);
    }

    .inicio {
        width: 18px;
        height: 18px;
        background: #007bff;
        position: absolute;
        transform: translate(-50%, -50%);
        border-radius: 4px;
        z-index: 999;
        left: 100px;
        top: 100px;
    }

    .inicio-label {
        position: absolute;
        left: 100px;
        top: 100px;
        transform: translate(-50%, -160%);
        font-weight: bold;
        font-size: 14px;
        color: #004b9b;
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
        width: 160px;
        transform: translate(-50%, -50%);
        text-align: center;
    }

    .estande img {
        width: 160px;
        height: 160px;
        object-fit: cover;
        border-radius: 12px;
        border: 2px solid #666;
    }

    .estande h3 {
        margin: 6px 0;
        font-size: 17px;
        color: #222;
    }

</style>
</head>

<body>

<div class="container">

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

    <div class="mapa" id="mapa">

        <div class="inicio" id="inicio"></div>
        <div class="inicio-label" id="inicioLabel">Início</div>

        <div class="ponto" id="ponto"></div>

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
