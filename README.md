<style>
    body {
        font-family: Arial, sans-serif;
        display: flex;
        justify-content: center; /* centraliza horizontalmente */
        padding: 20px;
        background: #f3f3f3;
    }

    .container {
        display: flex;
        gap: 20px;
    }

    .painel {
        width: 300px;
        background: white;
        padding: 20px;
        border-radius: 10px;
        box-shadow: 0 0 10px rgba(0,0,0,0.1);
    }

    /* QUADRADO DO MAPA */
    .mapa {
        width: 800px;
        height: 600px;
        background: #ffffff;
        border: 2px solid black;
        border-radius: 10px;
        position: relative;
        display: flex;
        flex-wrap: wrap; /* permite organizar as estandes em grade */
        justify-content: space-around; /* espaçamento horizontal */
        align-content: space-around; /* espaçamento vertical */
        padding: 20px;
        box-sizing: border-box;
    }

    /* Ícone de início */
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

    /* Ponto vermelho */
    .ponto {
        width: 22px;
        height: 22px;
        background: red;
        border-radius: 50%;
        position: absolute;
        transform: translate(-50%, -50%);
        z-index: 900;
    }

    /* Estandes */
    .estande {
        width: 150px;
        text-align: center;
        margin: 10px; /* espaço entre as estandes */
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

        <!-- Ícone de INÍCIO -->
        <div class="inicio" id="inicio" style="left:50px; top:50px;"></div>
        <div class="inicio-label" id="inicioLabel" style="left:50px; top:50px;">Início</div>

        <!-- PONTO VERMELHO -->
        <div class="ponto" id="ponto" style="left:50px; top:50px;"></div>

        <!-- ESTANDES ORGANIZADAS -->
        <div class="estande" id="Estande-Biologia">
            <h3>Biologia</h3>
            <img src="biologia.png">
        </div>

        <div class="estande" id="Estande-Química">
            <h3>Química</h3>
            <img src="quimica.png">
        </div>

        <div class="estande" id="Estande-Robótica">
            <h3>Robótica</h3>
            <img src="robotica.png">
        </div>

        <div class="estande" id="Estande-Matemática">
            <h3>Matemática</h3>
            <img src="matematica.png">
        </div>

    </div>
</div>

<script>
function removeAcentos(texto) {
    return texto.normalize("NFD").replace(/[\u0300-\u036f]/g, "").toLowerCase();
}

const pontos = [
    { nome: "Biologia", x: 200, y: 150 },
    { nome: "Química", x: 600, y: 150 },
    { nome: "Robótica", x: 200, y: 450 },
    { nome: "Matemática", x: 600, y: 450 }
];

function consultar() {
    let nomeDigitado = document.getElementById("nomeConsulta").value.trim();
    let nomeLimpo = removeAcentos(nomeDigitado);
    let resultado = document.getElementById("resultado");
    let encontrado = pontos.find(p => removeAcentos(p.nome) === nomeLimpo);
    if (!encontrado) {
        resultado.innerHTML = "❌ Estande não encontrado.";
        return;
    }
    resultado.innerHTML = `Estande: ${encontrado.nome}<br>Coordenadas: X=${encontrado.x} | Y=${encontrado.y}`;
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
