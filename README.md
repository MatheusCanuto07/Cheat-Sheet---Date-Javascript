# JavaScript Date Cheat Sheet

Este arquivo é um guia rápido (*cheat sheet*) com exemplos práticos para trabalhar com datas no JavaScript.  
Inclui construtores, métodos de formatação, manipulação de fuso horário, cálculos de diferença e validação.

---

## 📅 Construtores da Classe `Date`

```javascript
// Cria data/hora atual no fuso horário local
let agora = new Date();

// Cria cópia de outra data
let copia = new Date(agora);

// Date.parse() → retorna timestamp em milissegundos (não recomendado para parsing genérico)
let dateParse = Date.parse(agora); 

// Criação via string
let d1 = new Date("2025-08-11"); //Sun Aug 10 2025 21:00:00 GMT-0300 (Horário Padrão de Brasília)
let d2 = new Date("August 11, 2025 15:30:00");

// Criação via parâmetros numéricos (mês começa em 0)
let d3 = new Date(2025, 7, 11); // Agosto
let d4 = new Date(2025, 7, 11, 15, 30, 0, 0);

// Criação via timestamp
let d5 = new Date(1691769600000);

// Criação via Date.now()
let d6 = new Date(Date.now());
```

---

## ⏳ Trabalhando com fusos horários

```javascript
// Garantir um fuso específico na formatação
let sp = agora.toLocaleString("pt-BR", { timeZone: "America/Sao_Paulo" });
```

---

## 📆 Obtendo partes da data

```javascript
let hoje = new Date();
let dia = hoje.getDate();        // Dia do mês (1–31)
let mes = hoje.getMonth() + 1;   // Mês (0–11) → +1
let ano = hoje.getFullYear();    // Ano completo
```

---

## ✏️ Alterando datas

```javascript
let data = new Date();
data.setFullYear(2030);
data.setMonth(0); // Janeiro
data.setDate(15);
data.setHours(10, 30, 0);
```

---

## 🌐 Trabalhando com UTC

```javascript
// Obtendo valores UTC
agora.getUTCDate();
agora.getUTCMonth();
agora.getUTCFullYear();
agora.getUTCHours();

// Criando data UTC
let dateUTC = Date.UTC(2025, 7, 11, 30, 0, 0);
```

---

## 🖨️ Formatações úteis

```javascript
let dataAtual = new Date();

dataAtual.toISOString();          // "2025-08-11T12:34:56.789Z"
dataAtual.toDateString();         // "Mon Aug 11 2025"
dataAtual.toLocaleDateString("pt-BR"); // "11/08/2025"
dataAtual.toLocaleString("pt-BR");     // "11/08/2025 09:30:00"
```

---

## 📏 Calcular diferença entre datas

```javascript
let inicio = new Date("2025-08-01");
let fim = new Date("2025-08-11");

let diferencaMs = fim - inicio;
let diferencaDias = diferencaMs / (1000 * 60 * 60 * 24);
console.log(diferencaDias); // 10
```

---

## ➕➖ Adicionar / subtrair tempo

```javascript
let data = new Date();
data.setDate(data.getDate() + 5); // Soma 5 dias
data.setHours(data.getHours() - 3); // Subtrai 3 horas
```

---

## ✅ Validar se uma data é válida

```javascript
let d = new Date("data inválida");
if (isNaN(d)) {
  console.log("Data inválida");
}
```
