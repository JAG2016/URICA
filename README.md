# URICA
<!DOCTYPE html>
<html lang="pt-br">
<head>
  <meta charset="UTF-8">
  <title>URICA - Questionário para Drogas Ilícitas</title>
  <style>
    body { font-family: Arial, sans-serif; padding: 20px; max-width: 800px; margin: auto; }
    h1 { text-align: center; }
    .question { margin: 15px 0; }
    label { display: block; margin-bottom: 5px; }
    .result { margin-top: 30px; padding: 15px; background: #f0f0f0; border-radius: 10px; }
  </style>
</head>
<body>

<h1>URICA - Drogas Ilícitas</h1>
<p>Responda cada afirmação com uma nota de 1 a 5, sendo 1 = Discordo totalmente e 5 = Concordo totalmente.</p>

<form id="uricaForm">
  <div id="questions"></div>
  <button type="submit">Enviar e Ver Resultado</button>
</form>

<div class="result" id="result" style="display:none;"></div>

<script>
const questions = [
  "Não tenho nenhum problema com drogas que precise ser mudado.",
  "Acho que não preciso mudar nada sobre o uso de drogas.",
  "As pessoas exageram quando dizem que tenho problema com drogas.",
  "Estou satisfeito com o meu uso de drogas atual.",
  "Meu uso de drogas não é um problema para mim.",
  "As críticas sobre meu uso de drogas são injustas.",
  "Não vejo razão para parar de usar drogas.",
  "Não tenho interesse em mudar meu uso de drogas agora.",
  "Tenho pensado que devo mudar meu uso de drogas.",
  "Tenho me preocupado com as consequências do uso de drogas.",
  "Às vezes penso que estou perdendo o controle com as drogas.",
  "Estou começando a perceber que o uso de drogas pode ser um problema.",
  "Tenho pensado nos motivos para parar de usar drogas.",
  "Fico dividido entre continuar e parar de usar drogas.",
  "Às vezes quero parar, mas não sei se consigo.",
  "Acho que poderia me beneficiar se mudasse meu comportamento com drogas.",
  "Estou tomando medidas concretas para parar de usar drogas.",
  "Já comecei a mudar meu comportamento com relação às drogas.",
  "Tenho evitado situações que me levam ao uso de drogas.",
  "Estou determinado a parar de usar drogas.",
  "Estou fazendo algo que realmente vai me ajudar a parar de usar.",
  "Tenho feito planos para mudar meu uso de drogas.",
  "Estou comprometido com a mudança do meu comportamento.",
  "Já iniciei uma mudança na forma como lido com drogas.",
  "Estou trabalhando para manter as mudanças que fiz no meu uso de drogas.",
  "É importante continuar evitando recaídas.",
  "Tenho aprendido a lidar com situações de risco.",
  "Já mudei, mas sei que preciso continuar alerta.",
  "Estou mais confiante em manter a mudança que fiz.",
  "Posso lidar com tentações sem usar drogas.",
  "Aprendi estratégias para manter minha recuperação.",
  "Pode ser necessário manter o controle do uso de drogas para sempre."
];

const stages = ["PC","PC","PC","PC","PC","PC","PC","PC",
                "C","C","C","C","C","C","C","C",
                "A","A","A","A","A","A","A","A",
                "M","M","M","M","M","M","M","M"];

const interpretations = {
  PC: "Você se encontra no estágio de Pré-contemplação...",
  C: "Você está no estágio de Contemplação...",
  A: "Você está no estágio de Ação...",
  M: "Você está no estágio de Manutenção..."
};

const questionDiv = document.getElementById("questions");

questions.forEach((q, i) => {
  const container = document.createElement("div");
  container.className = "question";
  const label = document.createElement("label");
  label.textContent = `${i+1}. ${q}`;
  container.appendChild(label);

  for (let j = 1; j <= 5; j++) {
    const radio = document.createElement("input");
    radio.type = "radio";
    radio.name = `q${i}`;
    radio.value = j;
    radio.required = true;
    container.appendChild(radio);
    container.appendChild(document.createTextNode(` ${j} `));
  }
  questionDiv.appendChild(container);
});

document.getElementById("uricaForm").addEventListener("submit", function(e) {
  e.preventDefault();
  const results = { PC: [], C: [], A: [], M: [] };

  for (let i = 0; i < 32; i++) {
    const val = parseInt(document.querySelector(`input[name="q${i}"]:checked`).value);
    results[stages[i]].push(val);
  }

  const avg = {};
  for (const s in results) {
    avg[s] = (results[s].reduce((a,b)=>a+b,0) / results[s].length).toFixed(2);
  }

  const highest = Object.entries(avg).reduce((a, b) => a[1] > b[1] ? a : b);

  const resultDiv = document.getElementById("result");
  resultDiv.style.display = "block";
  resultDiv.innerHTML = `
    <h3>Resultado:</h3>
    <p><strong>Pré-contemplação:</strong> ${avg.PC}</p>
    <p><strong>Contemplação:</strong> ${avg.C}</p>
    <p><strong>Ação:</strong> ${avg.A}</p>
    <p><strong>Manutenção:</strong> ${avg.M}</p>
    <p><strong>Estágio predominante:</strong> ${highest[0]}</p>
    <p><em>${interpretations[highest[0]]}</em></p>
  `;
});
</script>

</body>
</html
