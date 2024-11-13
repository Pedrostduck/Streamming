# Streamming

<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,
initial-scale=1.0">
<title>Catálogo de Filmes</title>
<style>
body {
font-family: Arial, sans-serif;
padding: 20px;
background-color: #f5f5f5;

}

h1 {
    color: #333;
}



label {
display: block;
margin-top: 10px;

}

input, textarea {
width: 100%;
padding: 8px;
margin-top: 5px;
margin-bottom: 10px;
border-radius: 5px;
border: 1px solid #ccc;

}

button {
padding: 10px 15px;
background-color: #a207fc;
color: white;
border: none;
border-radius: 5px;
cursor: pointer;
margin-right: 10px;
}

button:hover {

    background-color: #06ebfc;
}
.filmes-lista {
margin-top: 20px;
padding: 10px;
background-color: #ddd;
border-radius: 50px;
box-shadow: 0 0 10px rgba(0,0,0,0.1);
}
.filme-item {
margin-bottom: 15px;
padding-bottom: 10px;
border-bottom: 1px solid #6e6e6e;
}
.filme-item:last-child {
border-bottom: none;
}
.filme-item strong {
display: block;
margin-top: 5px;
}
.actions {
margin-top: 10px;
}
</style>
</head>
<body>
<h1>Catálogo de Filmes</hi>
<div>
<h2>Cadastrar Novo Filme</h2>
<label for="nome">Nome do filme:</label>
<input type="text" id="nome" placeholder="Insira o nome do filme">
<label for="classificacao">Classificação indicativa: </label>

<input type="text" id="classificacao" placeholder="Ex: Livre,
12 anos, etc.">
<label for="duracao">Duração (minutos): </label>
<input type="number" id="duracao" placeholder="Duração em
minutos">
<label for="genero">Gênero: </label>
<input type="text" id="genero" placeholder="Ex: Ação, Comédia, Drama, etc.">
<label for="ano">Ano de lançamento:</label>
<input type="number" id="ano" placeholder="Ano de lançamento">
<label for="sinopse">Sinopse:</label>
<textarea id="sinopse" rows="4" placeholder="Insira a sinopse
do filme"></textarea>
<button onclick="cadastrarFilme()">Cadastrar Filme</button>
<button onclick="atualizarFilme()" id="btn-atualizar"
style="display:none;">Atualizar Filme</button>
</div>
<div>
<h2>Buscar Filme por Nome</h2>
<input type="text" id="busca" placeholder="Digite o nome do
filme">
<button onclick="buscarFilme()">Buscar</button>

</div>
<div>
<h2>Todos os Filmes Cadastrados</h2>
<button onclick="listarFilmes ()">Exibir Todos os
Filmes</button>
<div id="lista-filmes" class="filmes-lista"></div>
</div>
<script>
let catalogo = [];
let filmeEditando = null;

function cadastrarFilme() {
const nome = document.getElementById('nome').value;
const classificacao = document.getElementById('classificacao').value;
const duracao = document.getElementById('duracao').value;
const genero = document.getElementById('genero').value;
const ano = document.getElementById('ano').value;
const sinopse = document.getElementById('sinopse').value;

if (nome && classificacao && duracao && genero && ano &&
sinopse) {

const novoFilme = {
nome,
classificacao,
duracao,
genero,
ano,
sinopse
};
catalogo.push (novoFilme);
alert(`Filme "${nome}" cadastrado com sucesso!`);
LimparCampos();
listarFilmes();
} else {
alert("Por favor, preencha todos os campos!");
}
}

function buscarFilme() {
const busca = document.getElementById('busca').value.toLowerCase();
const filmeEncontrado = catalogo.find(filme =>
filme.nome.toLowerCase() === busca);
const listaFilmes = 
document.getElementById('lista-filmes');
listaFilmes.innerHTML = '' ;
if (filmeEncontrado) {
listaFilmes.innerHTM =
formatarDetalhesFilme (filmeEncontrado);

} else {
listaFilmes.innerHTML = `<p>Filme "${busca}" não
encontrado.</p>`;
}
}

function listarFilmes() {
const listaFilmes = document.getElementById('lista-filmes');
listaFilmes.innerHTML = '';

if (catalogo.length === 0) {
listaFilmes.innerHTML = '<p>Nenhum filme cadastrado no catálogo.</p>';
} else {

    catalogo.forEach((filme, index) => {
listaFilmes.innerHTML +=
formatarDetalhesFilme (filme, index);
});
}
}
function formatarDetalhesFilme (filme, index) {
return `
<div class="filme-item">
<strong>Nome:</strong>
 ${filme.nome}
<strong>Classificação Indicativa:</strong>
${filme.classificacao}
<strong>Duração:</strong> ${filme.duracao} minutos
<strong>Gênero:</strong> ${filme.gеnего}
<strong>Ano de Lançamento:</strong> ${filme.ano}
<strong>Sinopse:</strong> ${filme.sinopse}
<div class="actions">
<button
onclick="editarFilme(${index})">Editar</button>
<button onclick="excluirFilme (${index})"
style="background-color: #dc3545;">Excluir</button>
</div>
</div>
`;

}

function recomendarfilmes (genero) {
const recomendacoes = document.getElementById("recomendacoes");
recomendacoes.innerHTML = '<h3>Filmes Recomendados:</h3>';
const filmesRecomendados = catalogo.filter(filme => filme.genero.toLowerCase() === genero.toLowerCase() && filme.nome !== document.getElementById('nome').value);

if (filmesRecomendados.length > 0) {
filmes.Recomendados.forEach(filme => {
recomendacoes.innerHTML += formatarDetalhesFilme (filme);
}); 
} else {
recomendacoes.innerHTML += '<p>Nenhum filme recomendado encontrado.</p>';
}
}

function limparCampos() {
document.getElementById('nome').value = '';
document.getElementById('classificacao').value = '';
document.getElementById('duracao').value = '';
document.getElementById('genero').value = '';
document.getElementById('ano').value = '';
document.getElementById('sinopse').value = '';
document.getElementById('btn-atualizar').style.display = 'none';
filmeEditando = null;
}



function editarFilme (index) {
const filme = catalogo [index];
document.getElementById('nome').value = filme.nome;
document.getElementById('classificacao').value = filme.classificacao;
document.getElementById('duracao').value = filme.duracao;
document.getElementById('genero').value = filme.genero;
document.getElementById('ano').value = filme.ano;
document.getElementById('sinopse').value = filme.sinopse;

filmeEditando = index;
document.getElementById('btn-atualizar').style.display = 'inline';
}

function atualizarFilme() {
if (filmeEditando !== null) {
catalogo [filmeEditando] = {
nome: document.getElementById('nome').value,
classificacao: document.getElementById('classificacao').value, 
duracao: document.getElementById('duracao').value, 
genero: document.getElementById('genero').value,
ano: document.getElementById('ano').value,
sinopse: document.getElementById('sinopse').value
};

alert("Filme atualizado com sucesso!");
limparCampos();
listarFilmes();

}
}

function excluirFilme (index) { 
    catalogo.splice(index, 1); 
    alert("Filme excluído com sucesso!"); 
    listarFilmes();
}

</script>
</body>
</html>
