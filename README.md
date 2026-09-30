<!doctype html>
<html lang="pt-BR">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1">

<title>Chá de Casa Nova</title>

<style>

:root{
--bg:#f7f3ee;
--surface:#fffdf9;
--text:#3b2920;
--muted:#765f52;
--brown:#6f4634;
--gold:#b58a42;
--line:#e5d7c8;
}

*{
box-sizing:border-box;
}

html,body{
margin:0;
min-height:100%;
font-family:Georgia,'Times New Roman',serif;
background:var(--bg);
color:var(--text);
}

#app{
min-height:100vh;
background:var(--bg);
}

.hero{
padding:58px 20px 38px;
text-align:center;
background:linear-gradient(135deg,#fffdf9,#ead8c7);
border-bottom:1px solid var(--line);
}

.badge{
display:inline-block;
border:1px solid var(--gold);
color:var(--gold);
padding:7px 14px;
border-radius:999px;
font:600 12px Arial,sans-serif;
letter-spacing:2px;
text-transform:uppercase;
}

h1{
font-size:clamp(38px,8vw,68px);
margin:18px 0 8px;
font-weight:500;
}

.subtitle{
font:16px Arial,sans-serif;
color:var(--muted);
max-width:620px;
margin:auto;
line-height:1.6;
}

.fork{
font-size:27px;
color:var(--gold);
margin-top:18px;
}

.wrap{
max-width:1050px;
margin:auto;
padding:34px 18px 70px;
}

.intro{
text-align:center;
margin-bottom:28px;
}

.intro h2{
font-size:30px;
margin:0 0 8px;
}

.intro p{
font:15px Arial,sans-serif;
color:var(--muted);
}

.grid{
display:grid;
grid-template-columns:repeat(auto-fit,minmax(220px,1fr));
gap:16px;
}

.card{
background:var(--surface);
border:1px solid var(--line);
border-radius:18px;
padding:22px;
box-shadow:0 7px 24px #5b392218;
display:flex;
flex-direction:column;
min-height:205px;
}

.icon{
font-size:34px;
}

.card h3{
margin:12px 0 6px;
font-size:21px;
}

.card p{
font:13px Arial,sans-serif;
color:var(--muted);
margin:0 0 18px;
line-height:1.45;
flex:1;
}

.btn{
border:0;
border-radius:11px;
padding:12px 15px;
background:var(--brown);
color:white;
font-weight:700;
cursor:pointer;
}

.btn:hover{
filter:brightness(1.08);
}

.reserved{
background:#eee5dc;
color:#806b5e;
cursor:default;
}

.foot{
text-align:center;
color:var(--muted);
font:13px Arial,sans-serif;
margin-top:38px;
}

.modal{
position:fixed;
inset:0;
background:#23171099;
display:none;
align-items:center;
justify-content:center;
padding:18px;
}

.modal.open{
display:flex;
}

.box{
width:min(440px,100%);
background:var(--surface);
border-radius:20px;
padding:26px;
}

.box h3{
font-size:25px;
margin:0 0 8px;
}

.box p{
font:14px Arial,sans-serif;
color:var(--muted);
line-height:1.5;
}

.box input{
width:100%;
padding:13px;
border:1px solid var(--line);
border-radius:10px;
background:transparent;
color:var(--text);
font-size:16px;
margin:8px 0 14px;
}

.actions{
display:flex;
gap:10px;
}

.secondary{
background:transparent;
color:var(--brown);
border:1px solid var(--line);
}

@media(prefers-color-scheme:dark){

:root{
--bg:#241b17;
--surface:#30231d;
--text:#f7eee6;
--muted:#c9b5a7;
--line:#59483d;
}

.hero{
background:linear-gradient(135deg,#30231d,#463329);
}

.reserved{
background:#40332c;
color:#bca99c;
}

}

</style>

</head>

<body>

<div id="app">

<header class="hero">

<div class="badge">
Chá de Casa Nova
</div>

<h1>
Nosso novo lar
</h1>

<div class="fork">
✦
</div>

<p class="subtitle">
Sua presença já é um presente.
Mas, se quiser nos ajudar a montar nossa casa,
escolha um item da nossa lista com carinho.
</p>

</header>


<main class="wrap">

<section class="intro">

<h2>
Lista de presentes
</h2>

<p>
Escolha um presente e informe seu nome.
Organizamos tudo por cômodos para facilitar sua escolha.
</p>

</section>


<section id="grid" class="grid"></section>


<div class="foot">
Feito com carinho para o nosso Chá de Casa Nova ♡
</div>

</main>


<!-- JANELA PARA ESCOLHER PRESENTE -->

<div class="modal" id="modal">

<div class="box">

<h3 id="modalTitle">
Escolher presente
</h3>

<p>
Digite seu nome para reservar este presente.
</p>

<input
id="name"
maxlength="60"
placeholder="Seu nome"
>

<div class="actions">

<button
class="btn secondary"
onclick="closeModal()"
>
Cancelar
</button>

<button
class="btn"
onclick="reserve()"
>
Confirmar escolha
</button>

</div>

</div>

</div>


<script>


/*
================================================
LISTA DE PRESENTES
================================================

Para adicionar um presente, copie um dos modelos
e altere as informações.

Formato:

[
"emoji",
"Nome do presente",
"Descrição"
]

*/


const gifts = [

/* ================================
   SALA
================================ */

[
"🛋️",
"Sala",
"",
true
],

[
"🛋️",
"Almofadas decorativas",
"Para deixar a sala mais aconchegante."
],

[
"🕯️",
"Vela decorativa",
"Para dar um toque especial ao ambiente."
],

[
"🪴",
"Vaso decorativo",
"Para trazer mais vida à casa."
],

[
"🖼️",
"Quadro decorativo",
"Para decorar nosso novo lar."
],

[
"🧺",
"Cesto organizador",
"Para manter tudo no lugar."
],


/* ================================
   COZINHA
================================ */

[
"🍳",
"Cozinha",
"",
true
],

[
"🍽️",
"Jogo de pratos",
"Para as refeições do nosso novo lar."
],

[
"🥤",
"Jogo de copos",
"Para receber família e amigos."
],

[
"🍴",
"Jogo de talheres",
"Um item essencial para a cozinha."
],

[
"🍳",
"Frigideira",
"Para preparar nossas primeiras receitas."
],

[
"🫕",
"Jogo de panelas",
"Para deixar a cozinha completa."
],

[
"☕",
"Jogo de xícaras",
"Para aquele café especial."
],

[
"🥣",
"Tigelas",
"Para café da manhã e refeições."
],

[
"🍰",
"Forma para bolo",
"Para os doces feitos em casa."
],

[
"🫖",
"Bule",
"Para nossos cafés e chás."
],

[
"🧂",
"Potes para mantimentos",
"Para organizar arroz, feijão e outros alimentos."
],

[
"🔪",
"Jogo de facas",
"Para facilitar o preparo das refeições."
],


/* ================================
   QUARTO
================================ */

[
"🛏️",
"Quarto",
"",
true
],

[
"🛏️",
"Jogo de cama",
"Para deixar o quarto aconchegante."
],

[
"🛌",
"Travesseiros",
"Para noites mais confortáveis."
],

[
"🧸",
"Manta",
"Para deixar o quarto mais aconchegante."
],

[
"🧺",
"Cesto para roupas",
"Para organizar as roupas."
],

[
"🪞",
"Espelho",
"Para completar o quarto."
],


/* ================================
   BANHEIRO
================================ */

[
"🛁",
"Banheiro",
"",
true
],

[
"🛁",
"Kit de toalhas",
"Para o banheiro do novo lar."
],

[
"🧼",
"Kit de banheiro",
"Para organizar pia e bancada."
],

[
"🚿",
"Tapete para banheiro",
"Para deixar o banheiro mais confortável."
],

[
"🧻",
"Porta-papel higiênico",
"Um item útil para o dia a dia."
],

[
"🪥",
"Porta-escovas",
"Para manter a pia organizada."
],


/* ================================
   LIMPEZA
================================ */

[
"🧹",
"Limpeza e organização",
"",
true
],

[
"🧹",
"Kit de limpeza",
"Para ajudar nos cuidados da casa."
],

[
"🪣",
"Balde",
"Para facilitar a limpeza da casa."
],

[
"🧽",
"Kit de esponjas e panos",
"Para a limpeza do dia a dia."
],

[
"🧴",
"Produtos de limpeza",
"Para manter nossa casa sempre limpa." 
],

[
"🧺",
"Cesto organizador grande",
"Para guardar objetos e manter tudo organizado."
]

];


/*
================================================
SISTEMA DE ESCOLHA
================================================
*/

let selected = null;

const key = "cha-casa-nova-reservados-v1";

let reserved = JSON.parse(
localStorage.getItem(key) || "{}"
);


/*
================================================
MOSTRAR OS PRESENTES
================================================
*/

function render(){

const grid =
document.getElementById("grid");


grid.innerHTML = gifts.map((g,i)=>{

/* TÍTULO DO CÔMODO */

if(g[3]){

return `

<div
style="
grid-column:1/-1;
margin:18px 0 2px;
padding:12px 4px;
border-bottom:1px solid var(--line);
font-size:25px;
color:var(--brown);
font-weight:600;
">

${g[0]} ${g[1]}

</div>

`;

}


/* VERIFICA SE JÁ FOI ESCOLHIDO */

let r = reserved[i];


return `

<article class="card">

<div class="icon">
${g[0]}
</div>

<h3>
${g[1]}
</h3>

<p>
${g[2]}
</p>

<button
class="btn ${r ? "reserved" : ""}"
${r ? "disabled" : ""}
onclick="openModal(${i})"
>

${r
? "Presente escolhido"
: "Escolher este presente"}

</button>

</article>

`;

}).join("");

}


/*
================================================
ABRIR JANELA
================================================
*/

function openModal(i){

if(reserved[i]){
return;
}

selected = i;

document.getElementById("modalTitle").textContent =
"Escolher: " + gifts[i][1];

document.getElementById("name").value = "";

document
.getElementById("modal")
.classList.add("open");

setTimeout(()=>{
document.getElementById("name").focus();
},50);

}


/*
================================================
FECHAR JANELA
================================================
*/

function closeModal(){

document
.getElementById("modal")
.classList.remove("open");

selected = null;

}


/*
================================================
RESERVAR PRESENTE
================================================
*/

function reserve(){

const name =
document
.getElementById("name")
.value
.trim();


if(!name){

alert("Digite seu nome.");

return;

}


reserved[selected] = {

name:name,

date:new Date().toLocaleString("pt-BR")

};


localStorage.setItem(

key,

JSON.stringify(reserved)

);


closeModal();

render();

alert(
"Presente reservado com sucesso! ❤️"
);

}


/*
================================================
FECHAR CLICANDO FORA
================================================
*/

document
.getElementById("modal")
.addEventListener("click",function(event){

if(event.target === this){

closeModal();

}

});


/*
================================================
INICIAR SITE
================================================
*/

render();

</script>

</div>

</body>
</html>
