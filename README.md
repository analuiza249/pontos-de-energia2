<style>
    body {
        font-family: Arial, sans-serif;
        display: flex;
        justify-content: center;
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

    .painel h2 {
        color: #800000; /* vinho */
    }

    /* QUADRADO DO MAPA */
    .mapa {
        width: 800px;
        height: 600px;
        background: #ffffff;
        border: 2px solid black;
        border-radius: 10px;
        position: relative;
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
        position: absolute;
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
        <h2>Pontos de Energia</h2>
        <label>Nome do estande:</label>
        <input type="text" id="nomeConsulta" placeholder="Ex: Biologia">
        <button onclick="consultar()">Consultar</button>
        <div id="resultado"></div>
        <hr>
        <h2>Editar Coordenadas</h2>
        <label>Selecionar estande:</label>
        <select id="estandeSelect">
            <option value="Biologia">Biologia</option>
            <option value="Química">Química</option>
            <option value="Robótica">Robótica</option>
            <option value="Matemática">Matemática</option>
        </select>
        <button onclick="moverPonto()">Mover Ponto</button>
    </div>

    <!-- MAPA -->
    <div class="mapa" id="mapa">

        <!-- PONTO VERMELHO -->
        <div class="ponto" id="ponto"></div>

        <!-- ESTANDES ORGANIZADAS -->
        <div class="estande" id="Estande-Biologia" style="left:200px; top:150px;">
            <h3>Biologia</h3>
            <img src="biologia.png">
        </div>

        <div class="estande" id="Estande-Química" style="left:600px; top:150px;">
            <h3>Química</h3>
            <img src="quimica.png">
        </div>

        <div class="estande" id="Estande-Robótica" style="left:200px; top:450px;">
            <h3>Robótica</h3>
            <img src="robotica.png">
        </div>

        <div class="estande" id="Estande-Matemática" style="left:600px; top:450px;">
            <h3>Matemática</h3>
            <img src="matematica.png">
        </div>

    </div>
</div>

<script>
const pontos = {
    "Biologia": {x: 200, y: 150},
    "Química": {x: 600, y: 150},
    "Robótica": {x: 200, y: 450},
    "Matemática": {x: 600, y: 450}
};

function consultar() {
    const select = document.getElementById("nomeConsulta").value.trim();
    const resultado = document.getElementById("resultado");
    if (pontos[select]) {
        resultado.innerHTML = `Estande: ${select}<br>Coordenadas: X=${pontos[select].x} | Y=${pontos[select].y}`;
    } else {
        resultado.innerHTML = "❌ Estande não encontrado.";
    }
}

function moverPonto() {
    const estandeSelecionado = document.getElementById("estandeSelect").value;
    const ponto = document.getElementById("ponto");
    const pos = pontos[estandeSelecionado];
    ponto.style.left = pos.x + "px";
    ponto.style.top = pos.y + "px";
}
</script>
