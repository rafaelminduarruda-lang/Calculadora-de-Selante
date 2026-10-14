# Calculadora-de-Selante
Cálculo de cura de Selante 

<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
 
<title>Calculadora de Selagem</title>
 
<style>
:root{
--bg:#e6e8eb;
--card:#ffffff;
--text:#1b1b1b;
--primary:#0057b8;
--border:#c8cdd4;
}
 
.dark{
--bg:#1b1f24;
--card:#2b3138;
--text:#ffffff;
--primary:#4ea1ff;
--border:#46515d;
}
 
*{
margin:0;
padding:0;
box-sizing:border-box;
font-family:Segoe UI,Arial,sans-serif;
}
 
body{
background:var(--bg);
color:var(--text);
padding:30px;
transition:.3s;
}
 
.container{
max-width:1000px;
margin:auto;
}
 
header{
display:flex;
justify-content:space-between;
align-items:center;
margin-bottom:25px;
}
 
.logo{
font-size:28px;
font-weight:700;
letter-spacing:2px;
color:var(--primary);
}
 
.sub{
font-size:13px;
opacity:.8;
}
 
.theme-btn{
padding:10px 18px;
border:none;
border-radius:8px;
cursor:pointer;
background:var(--primary);
color:white;
font-weight:600;
}
 
.form-card{
background:var(--card);
padding:25px;
border-radius:12px;
border:1px solid var(--border);
}
 
.grid{
display:grid;
grid-template-columns:repeat(auto-fit,minmax(250px,1fr));
gap:15px;
}
 
label{
display:block;
margin-bottom:5px;
font-weight:600;
}
 
input,select{
width:100%;
padding:12px;
border:1px solid var(--border);
border-radius:8px;
background:var(--card);
color:var(--text);
}
 
button.calc{
margin-top:20px;
width:100%;
padding:14px;
border:none;
border-radius:10px;
background:var(--primary);
color:white;
font-size:16px;
font-weight:700;
cursor:pointer;
}
 
.resultados{
margin-top:25px;
display:grid;
grid-template-columns:repeat(auto-fit,minmax(250px,1fr));
gap:18px;
}
 
.card{
padding:20px;
border-radius:12px;
color:white;
}
 
.aplicacao{
background:#0066cc;
}
 
.manuseio{
background:#f57c00;
}
 
.cura{
background:#18a558;
}
 
.card h3{
margin-bottom:15px;
}
 
.data{
font-size:22px;
font-weight:700;
}
 
.faixa{
margin-top:20px;
padding:15px;
background:var(--card);
border:1px solid var(--border);
border-radius:12px;
}
 
.copy{
margin-top:15px;
padding:12px;
width:100%;
border:none;
border-radius:10px;
cursor:pointer;
background:#18a558;
color:white;
font-weight:bold;
}
</style>
</head>
 
<body>
 
<div class="container">
 
<header>
<div>
<div class="logo">EMBRAER SELAGEM</div>
<div class="sub">Calculadora de Tempos de Selantes</div>
</div>
 
<button class="theme-btn" onclick="alternarTema()">
🌙 Claro/Escuro
</button>
</header>
 
<div class="form-card">
 
<div class="grid">
 
<div>
<label>Tipo do Selante</label>
<select id="tipo">
<option>MC780 B2</option>
<option>MC780 B1/2</option>
<option>PR2050 B1/2</option>
<option>PR2001 B1/2</option>
<option>C12</option>
<option>C24</option>
<option>C48</option>
</select>
</div>
 
<div>
<label>Temperatura (°C)</label>
<input type="number" step="0.1" id="temp">
</div>
 
<div>
<label>Preparação</label>
<input type="datetime-local" id="prep">
</div>
 
</div>
 
<button class="calc" onclick="calcular()">
CALCULAR
</button>
 
</div>
 
<div class="faixa" id="faixa">
Aguardando cálculo...
</div>
 
<div class="resultados" id="resultados"></div>
 
<button class="copy" onclick="copiarResultado()">
COPIAR RESULTADO
</button>
 
</div>
 
<script>
 
document.getElementById("prep").value =
new Date().toISOString().slice(0,16);
 
function alternarTema(){
document.body.classList.toggle("dark");
}
 
const dados = {
 
"MC780 B1/2":[
[10,120,960,1200,"Até 10°C"],
[17,60,480,600,"10,1 a 17°C"],
[24,30,240,300,"17,1 a 24°C"],
[31,15,120,150,"24,1 a 31°C"],
[38,7.5,60,75,"31,1 a 38°C"],
[45,3.75,30,37.5,"38,1 a 45°C"]
],
 
"MC780 B2":[
[10,480,1920,2400,"Até 10°C"],
[17,240,960,1200,"10,1 a 17°C"],
[24,120,480,600,"17,1 a 24°C"],
[31,60,240,300,"24,1 a 31°C"],
[38,30,120,150,"31,1 a 38°C"],
[45,15,60,75,"38,1 a 45°C"]
],
 
"PR2050 B1/2":[
[10,120,480,720,"Até 10°C"],
[17,60,240,360,"10,1 a 17°C"],
[24,30,120,180,"17,1 a 24°C"],
[31,15,60,90,"24,1 a 31°C"],
[38,7.5,30,45,"31,1 a 38°C"],
[45,3.75,15,22.5,"38,1 a 45°C"]
],
 
"PR2001 B1/2":[
[10,120,480,720,"Até 10°C"],
[17,60,240,360,"10,1 a 17°C"],
[24,30,120,180,"17,1 a 24°C"],
[31,15,60,90,"24,1 a 31°C"],
[38,7.5,30,45,"31,1 a 38°C"],
[45,3.75,15,22.5,"38,1 a 45°C"]
],
 
"C12":[
[10,2880,4800,"Até 10°C"],
[17,1440,2400,"10,1 a 17°C"],
[24,720,1200,"17,1 a 24°C"],
[31,360,600,"24,1 a 31°C"],
[38,180,300,"31,1 a 38°C"],
[45,90,150,"38,1 a 45°C"]
],
 
"C24":[
[10,5760,19200,"Até 10°C"],
[17,2880,9600,"10,1 a 17°C"],
[24,1440,4800,"17,1 a 24°C"],
[31,720,2400,"24,1 a 31°C"],
[38,360,1200,"31,1 a 38°C"],
[45,180,600,"38,1 a 45°C"]
],
 
"C48":[
[10,11520,40320,"Até 10°C"],
[17,5760,20160,"10,1 a 17°C"],
[24,2880,10080,"17,1 a 24°C"],
[31,1440,5040,"24,1 a 31°C"],
[38,720,2520,"31,1 a 38°C"],
[45,360,1260,"38,1 a 45°C"]
]
 
};
 
let textoResultado="";
 
function formatar(data){
return data.toLocaleString('pt-BR');
}
 
function calcular(){
 
const tipo=document.getElementById("tipo").value;
const temp=parseFloat(document.getElementById("temp").value);
const prep=new Date(document.getElementById("prep").value);
 
if(isNaN(temp)){
alert("Informe a temperatura.");
return;
}
 
const linha=dados[tipo].find(x=>temp<=x[0]);
 
if(!linha){
alert("Temperatura fora da faixa.");
return;
}
 
document.getElementById("faixa").innerHTML=
"<b>Faixa utilizada:</b> "+linha[linha.length-1];
 
let html="";
 
if(tipo.startsWith("C")){
 
const aplicacao=new Date(prep.getTime()+linha[1]*60000);
const montagem=new Date(prep.getTime()+linha[2]*60000);
 
html+=`
<div class="card aplicacao">
<h3>APLICAÇÃO</h3>
<div class="data">${formatar(aplicacao)}</div>
</div>
 
<div class="card manuseio">
<h3>MONTAGEM</h3>
<div class="data">${formatar(montagem)}</div>
</div>
`;
 
textoResultado=
`${tipo}
 
Preparação: ${formatar(prep)}
 
Aplicação: ${formatar(aplicacao)}
 
Montagem: ${formatar(montagem)}`;
 
}else{
 
const aplicacao=new Date(prep.getTime()+linha[1]*60000);
const manuseio=new Date(prep.getTime()+linha[2]*60000);
const cura=new Date(prep.getTime()+linha[3]*60000);
 
html+=`
<div class="card aplicacao">
<h3>APLICAÇÃO</h3>
<div class="data">${formatar(aplicacao)}</div>
</div>
 
<div class="card manuseio">
<h3>MANUSEIO</h3>
<div class="data">${formatar(manuseio)}</div>
</div>
 
<div class="card cura">
<h3>CURA</h3>
<div class="data">${formatar(cura)}</div>
</div>
`;
 
textoResultado=
`${tipo}
 
Preparação: ${formatar(prep)}
 
Aplicação: ${formatar(aplicacao)}
 
Manuseio: ${formatar(manuseio)}
 
Cura: ${formatar(cura)}`;
}
 
document.getElementById("resultados").innerHTML=html;
 
}
 
function copiarResultado(){
 
if(!textoResultado){
alert("Faça um cálculo primeiro.");
return;
}
 
navigator.clipboard.writeText(textoResultado);
 
alert("Resultado copiado.");
}
 
</script>
 
</body>
</html>
