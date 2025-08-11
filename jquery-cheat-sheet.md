
# Guia prático de jQuery: seleção e manipulação de elementos

---

## 📌 Selecionando elementos no jQuery

```js
// Seleção por ID
let elementoId = $("#meuId");

// Seleção por classe
let elementosClasse = $(".minhaClasse");
console.log(elementosClasse[0]);        // DOM puro
console.log($(elementosClasse[0]));    // jQuery wrap

// Seleção por tipo de elemento
let elementosParagrafo = $("p");
console.log(elementosParagrafo); // Todos os <p> no documento

// Acessando o elemento DOM puro
let primeiroElementoDOM = elementosClasse[0];      // DOM puro
let primeiroElementoDOM2 = elementosClasse.get(0); // DOM puro
```

---

## 📝 Trabalhando com inputs (valores, propriedades, atributos)

```js
// Selecionando inputs do tipo texto
let inputsTexto = $("input[type='text']");

// Obter e definir valor do input
let valor = $("#meuInput").val();       // obtém valor
$("#meuInput").val("novo valor");       // define valor

// Trabalhando com checkbox: verificar e alterar estado
let marcado = $("#meuCheckbox").prop("checked");   // true ou false
$("#meuCheckbox").prop("checked", true);           // marca o checkbox

// Manipular atributos do input
$("#meuInput").attr("disabled", true);    // desabilita
$("#meuInput").removeAttr("disabled");    // habilita
$("#meuInput").attr("placeholder", "Digite seu nome");

// Manipular propriedades booleanas (mais confiáveis para estados)
$("#meuInput").prop("readonly", true);
$("#meuInput").prop("readonly", false);

// Selecionar checkboxes marcados
let selecionados = $("input[type=checkbox]:checked");
```

---

## 🔧 Exemplos práticos com elementos e eventos jQuery

```js
$(document).ready(function() {
  // Alterar texto
  $("#meuId").text("Texto alterado via jQuery");

  // Alterar cor dos elementos com classe
  $(".minhaClasse").css("color", "blue");

  // Adicionar borda aos parágrafos
  $("p").css("border", "1px solid red");

  // Buscar elementos filhos com classe específica
  let filhosComClasse = elementoId.find(".filho");

  // Ocultar elemento (display: none)
  elementoId.hide();

  // Mostrar elemento (remove display:none ou restaura valor original)
  elementoId.show();

  // Obter e definir HTML interno
  let conteudoHtml = elementoId.html(); // obtém o HTML interno
  elementoId.html("<strong>Novo conteúdo HTML</strong>"); // define novo HTML

  // Inserir conteúdo ao final e início do elemento
  elementoId.append("<p>Parágrafo adicionado no final</p>");
  elementoId.prepend("<p>Parágrafo adicionado no início</p>");

  // Eventos: adicionar e remover listener
  elementoId.on("click", function () {
    alert("Elemento clicado!");
  });
  elementoId.off("click");

  // Trabalhando com atributos
  let idAtual = elementoId.attr("id"); // obtém atributo 'id'
  console.log("ID atual:", idAtual);
  elementoId.attr("title", "Título dinâmico"); // define atributo 'title'

  // Manipular valor do input
  $("#meuInput").val("Novo valor no input");

  // Obter e definir texto (sem HTML)
  let texto = elementoId.text(); // obtém texto interno
  console.log("Texto interno:", texto);
  elementoId.text("Novo texto sem tags HTML"); // define texto

  // Iterar sobre múltiplos elementos
  $(".minhaClasse").each(function (index, elemento) {
    console.log(`Elemento ${index}:`, $(elemento).text());
  });
});
```

---

## 🔍 Resumo rápido

| Operação       | Método jQuery            | Descrição                                      |
|----------------|-------------------------|------------------------------------------------|
| Selecionar     | `$()`, `.find()`        | Seleciona elementos por ID, classe, tipo       |
| Obter valor    | `.val()`                | Obtém valor de inputs, selects, textareas      |
| Definir valor  | `.val(valor)`           | Define valor de inputs, selects, textareas     |
| Checar checkbox| `.prop('checked')`      | Verifica se checkbox/radio está marcado        |
| Alterar prop.  | `.prop()`               | Define propriedades booleanas (`checked`, etc)|
| Alterar attr.  | `.attr()`               | Define atributos (`disabled`, `placeholder`)   |
| Mostrar/ocultar| `.show()`, `.hide()`    | Mostra ou oculta elementos                      |
| HTML interno   | `.html()`               | Obter/definir conteúdo HTML interno            |
| Texto interno  | `.text()`               | Obter/definir texto (sem tags HTML)            |
| Eventos        | `.on()`, `.off()`       | Adicionar e remover eventos                      |
| Iterar         | `.each()`               | Iterar coleção de elementos                     |

