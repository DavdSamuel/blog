+++
title = 'Mathjax'
date = 2024-01-15T15:39:43Z
draft = false
categories = ["Programação", "Matemática", "Tutoriais"]
tags = ["LaTeX"]
+++

Neste tutorial eu vou ensinar a usar o MathJax, ah e esse é o meu primeiro post.

## O que é o MathJax?
O MathJax é uma biblioteca (um código que alguém escreveu para ser usado) para colocar expressões matemáticas em páginas web **incluindo fórmulas LaTeX**.

## Um exemplo vale mais que mil palavras
```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Demonstração do MathJax</title>
  <!-- Importando o MathJax -->
  <script type="text/javascript" async src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.7/MathJax.js?config=TeX-MML-AM_CHTML"></script>
</head>
<body>
  <h1>$$\frac{8}{4 \div 2} = 2$$</h1>

  <script type="text/x-mathjax-config">
    MathJax.Hub.Config({
      tex2jax: {inlineMath: [['$', '$'], ['\\(', '\\)']]}
    });
  </script>
</body>
</html>
```

E aproveite o resultado :)  
![Resultado do código acima](/img/formula.png)  
Você deve ter gostado não é? Vamos fazer um projeto com isso!

## Um projeto de fórmulas
### O que vai ser o projeto?
Vai ser um projeto que gera um resultado com base em uma fórmula LaTeX dada.
### Iniciando o projeto
Vamos começar criando um diretório pro projeto:
```bash
~/Desktop/Projetos/$ mkdir gerador_de_formulas
~/Desktop/Projetos/$ cd gerador_de_formulas
~/Desktop/Projetos/gerador_de_formulas$
```
Agora vamos criar um repositório git, isso é opcional:
```bash
~/Desktop/Projetos/gerador_de_formulas$ git init
```
Vamos criar os arquivos pro projeto:
```bash
~/Desktop/Projetos/gerador_de_formulas$ touch index.html style.css script.js README.md
```
### Hora de codar!
#### Criando o README.md
O README.md serve pra descrever o projeto pra outras pessoas, não precisa ser muito complexo pra este projeto:
```markdown
Este é um projeto simples de um site que recebe a entrada de um formulário e gera um código LaTeX com base nessa entrada.
```

#### Criando a página
Vamos criar a página HTML, saiba que a sintaxe básica da página HTML é essa:
```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Título da página</title>
</head>
<body>
</body>
</html>
```
**Explicação do código:**  
- `<!DOCTYPE html>` É para especificar que a página usa HTML5.
- `<html>` para dizer que aqui começa a página.
- `<head>` é para colocar tags como título, links para CSS, links para JavaScript (caso você use alguma bilioteca, neste caso estamos usando a biblioteca MathJax, mas se você está programando seus próprios códigos JavaScript o recomendável é que você coloque o link para o código JavaScript na tag `<body>`), ou as meta tags (podem ser pra definir os caracteres aceitados, colocar uma descrição, autor, palavras chave, etc.).
- A meta tag `<meta charset="UTF-8">` serve pra que a páagina aceite caracteres UTF-8, que no caso são acentos bem presentes no português e outras línguas.
- `<title>` serve para colocar um título na página.
- `<body>` serve para colocar o conteúdo que vemos na página, como textos imagens, etc.

Ok, agora vamos escrever o nosso código. Para começar vamos colocar a língua da nossa página usando `<html lang="pt-br">`:
```html
<html lang="pt-br"> <!-- pt-br para potuguês do brasil -->
</html>
```
Vamos colocar mais algumas meta-tags e um título:
```html
<!DOCTYPE html>
<html lang="pt-br">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>LaTeX</title>
  <script type="text/javascript" async src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.7/MathJax.js?config=TeX-MML-AM_CHTML"></script>
</head>
</html>
```

**Mas quanta coisa! O que é tudo isso!?**  
Não fique confuso, deixe eu explicar:  
- Eu já expliquei sobre a meta tag `<meta charset=UTF-8>` quando estava explicando sobre a sintaxe básica da página HTML.
- `<meta http-equiv="X-UA-Compatible" content="IE=edge">` é para o código ter um poruco mais de compatibilidade com o Internet Explorer (mas se bem que ninguém usa ele kkkkk).
- `<meta name="viewport" content="width=device-width, initial-scale=1.0">` é para o código ser mais responsivo (se adaptar melhor a dispositivos móveis), mas dá para torná-lo mais responsivo por meio de CSS.
- Eu também já expliquei sobre a tag `<title>`.
- `<script type="text/javascript" async src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.7/MathJax.js?config=TeX-MML-AM_CHTML"></script>` é para importar o MathJax.

Eu vou colocar um link pra o CSS:

```html
<!DOCTYPE html>
<html lang="pt-br">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>LaTeX</title>
  <script type="text/javascript" async src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.7/MathJax.js?config=TeX-MML-AM_CHTML"></script>
  <link rel="stylesheet" href="style.css">
</head>
</html>
```

Se você for recriar o projeto, certifique-se de que o caminho pro seu arquivo CSS está correto. Vamos salvar essas alterações e deixar o código assim por enquanto, vamos partir para o CSS.

```css
body {
  text-align: center;
  font-family: Arial;
  margin: 0 auto; /* Para centralizar outras coisas que não são o texto */
}
```

Vamos colocar o conteúdo da página, por enquanto um texto e uma configuração do MathJax que irá ser útil depois:

```html
<!DOCTYPE html>
<html lang="pt-br">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>LaTeX</title>
  <script type="text/javascript" async src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.7/MathJax.js?config=TeX-MML-AM_CHTML"></script>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <h1>Criador de fórmulas LaTeX</h1>
  <script type="text/x-mathjax-config">
    MathJax.Hub.Config({
      tex2jax: {inlineMath: [['$', '$'], ['\\(', '\\)']]}
    });
  </script>
</body>
</html>
```

Vamos colocar um parágrafo que será o resultado da entrada do usuário:

```html
<!DOCTYPE html>
<html lang="pt-br">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>LaTeX</title>
  <script type="text/javascript" async src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.7/MathJax.js?config=TeX-MML-AM_CHTML"></script>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <h1>Criador de fórmulas LaTeX</h1>
  <p></p>
  <script type="text/x-mathjax-config">
    MathJax.Hub.Config({
      tex2jax: {inlineMath: [['$', '$'], ['\\(', '\\)']]}
    });
  </script>
</body>
</html>
```

Vamos colocar um formulário com um campo de entrada (input) e um botão para enviar:

```html
<!DOCTYPE html>
<html lang="pt-br">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>LaTeX</title>
  <script type="text/javascript" async src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.7/MathJax.js?config=TeX-MML-AM_CHTML"></script>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <h1>Criador de fórmulas LaTeX</h1>
  <form>
    <input type="text" placeholder="Sua fórmula LaTeX"><br>
    <input type="submit" value="Enviar">
  </form>
  <p></p>
  <script type="text/x-mathjax-config">
    MathJax.Hub.Config({
      tex2jax: {inlineMath: [['$', '$'], ['\\(', '\\)']]}
    });
  </script>
</body>
</html>
```

**Explicação rápida:**
- `<input>` é um campo de entrada e o tipo de entrada inserida depende do atributo `type` que no caso o primeiro elemento `<input>` é para inserir texto e o atributo `placeholder` é para inserir um texto explicativo no campo de entrada e o segundo é um botão de enviar que através do atributo `value` eu difini que o texto que iria aparecer no botão seria "Enviar".

Vamos colocar um ids e classes, isso é útil por causa do CSS, assim podemos colocar estilos diferentes em cada elemento ou algum grupo de elementos:

```html
<!DOCTYPE html>
<html lang="pt-br">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>LaTeX</title>
  <script type="text/javascript" async src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.7/MathJax.js?config=TeX-MML-AM_CHTML"></script>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <h1>Criador de fórmulas LaTeX</h1>
  <form>
    <input type="text" id="input" placeholder="Sua fórmula LaTeX"><br>
    <input id="submit" type="submit" value="Enviar">
  </form>
  <p id="resultado"></p>
  <script type="text/x-mathjax-config">
    MathJax.Hub.Config({
      tex2jax: {inlineMath: [['$', '$'], ['\\(', '\\)']]}
    });
  </script>
</body>
</html>
```

Certo, agora vamos usar o CSS, primeiro vamos aumentar a fonte do título:
```css
body {
  text-align: center;
  font-family: Arial;
  margin: 0 auto;
}

h1 {
  font-size: 55px;
}
```

Vamos colocar alguns estilos para os campos de entrada:

```css
body {
  text-align: center;
  font-family: Arial;
  margin: 0 auto;
}

h1 {
  font-size: 55px;
}

input {
  margin: 10px;
  padding: 20px;
  font-size: 20px;
  border-radius: 30px;
}

#submit {
  color: #d6d6d6;
  background-color: #007bff;
}
```

Ok, hora do JavaScript, para isso irei colocar um link para o JavaScript:

```html
<!DOCTYPE html>
<html lang="pt-br">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>LaTeX</title>
  <script type="text/javascript" async src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.7/MathJax.js?config=TeX-MML-AM_CHTML"></script>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <h1>Criador de fórmulas LaTeX</h1>
  <form>
    <input type="text" id="input" placeholder="Sua fórmula LaTeX"><br>
    <input id="submit" type="submit" value="Enviar">
  </form>
  <p id="resultado"></p>
  <script type="text/x-mathjax-config">
    MathJax.Hub.Config({
      tex2jax: {inlineMath: [['$', '$'], ['\\(', '\\)']]}
    });
  </script>
  <script src="script.js"></script>
</body>
</html>
```

Lembre-se, se você quiser recriar o projeto coloque o caminho correto para o seu JavaScript. Ok, para começar iremos criar variáveis para nossos elementos html:

```javascript
const input = document.getElementById("input");
const resultado = document.getElementById("resultado");
const form = document.querySelector("form");
```

Ok, agora vamos adicionar um event listener pra colcoar o resultado quando o usuário clica em "Enviar":

```javascript
const input = document.getElementById("input");
const resultado = document.getElementById("resultado");
const form = document.querySelector("form");
form.addEventListener("submit", function(event) {});
```

Por enquanto nada acontece, mas vamos usar a função `event.preventDefault();` para fazer a página não recarregar, certifique-se que você passou `event` como argumento em `form.addEventListener("submit", function(event) {});`:

```javascript
const input = document.getElementById("input");
const resultado = document.getElementById("resultado");
const form = document.querySelector("form");
form.addEventListener("submit", function(event) {
  event.preventDefault();
});
```

Vamos declarar uma variável pra armazenar o valor inserido no campo de entrada:

```javascript
const input = document.getElementById("input");
const resultado = document.getElementById("resultado");
const form = document.querySelector("form");
form.addEventListener("submit", function(event) {
  event.preventDefault();
  const formula = input.value;
});
```

Vamos colocar o valor de `formula` no conteúdo do parágrafo que colocamos antes:

```javascript
const input = document.getElementById("input");
const resultado = document.getElementById("resultado");
const form = document.querySelector("form");
form.addEventListener("submit", function(event) {
  event.preventDefault();
  const formula = input.value;
  resultado.innerHTML = `$${formula}$`;
});
```

O `.innerHTML`é para colocar algum conteúdo em algum elemento, no caso o elemento `<p></p>`, você pode pensar como se o `.innerHTML` colocasse algum texto `<p>entre esses elementos</p>`. Ah e lembre-se de colocar dois cifrões e o conteúdo, pode ser entre as crases (lembre-se de que caso você coloque entre crases você precisa colocar dois cifrões `$$`, duas chaves com o nome .da variável que armazena o conteúdo do parágrafo que no meu caso a variável é `formula` `$${formula}` e mais um cifrão `$${formula}$`) ou entre aspas simples ou duplas `'$', 'formula', '$'`.

Por enquanto não acontece muita coisa, então vamos colocar a função `MathJax.Hub.Typeset();`, se você não colocou esse código no seu HTML coloque:

```html
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    tex2jax: {inlineMath: [['$', '$'], ['\\(', '\\)']]}
  });
</script>
```

Ok, vamos completar o nosso código:

```javascript
const input = document.getElementById("input");
const resultado = document.getElementById("resultado");
const form = document.querySelector("form");
form.addEventListener("submit", function(event) {
  event.preventDefault();
  const formula = input.value;
  resultado.innerHTML = `$${formula}$`;
});
MathJax.Hub.Typeset();
```

Vamos fazer o commit no repositório git que criamos, lembre-se, criar um repositório git e fazer o commit é opcional:

```bash
~/Desktop/Projetos/gerador_de_formulas$ git add .
~/Desktop/Projetos/gerador_de_formulas$ git commit -m "Commit inicial"
```

E agora é só rodar o código e ver a mágica acontecer:

![Resultado do nosso código](/img/app_formulas.png)