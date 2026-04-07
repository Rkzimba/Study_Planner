# Avaliação Parcial 1 (AP1) - Aplicações Front-End

Olá! 👋 

Este é o repositório base para o trabalho da **AP1 (Avaliação Parcial 1)** da disciplina de Aplicações Front-End. Aqui você encontrará os arquivos HTML e CSS já prontos. A sua missão é **escrever a lógica em JavaScript** no arquivo `assets/js/script.js` para dar vida à aplicação, deixando-a com o comportamento ideal esperado.

## 🎯 Objetivo
Você deve construir uma "Lista de Estudos" dinâmica, onde o usuário consegue:
1. Adicionar itens manualmente (com validações de formulário).
2. Buscar sugestões de atividades consumindo a API externa `JSONPlaceholder`.
3. Deletar itens da lista.
4. Recarregar a última busca feita na API.

Tudo isso utilizando manipulação de DOM, Eventos, e JavaScript Assíncrono (`fetch`, `async`/`await`).

---

## 🛠️ Passo a Passo para o Desenvolvimento (Guia Didático)

Siga a recomendação de passos abaixo. Construa uma etapa de cada vez e vá validando no navegador:

### Passo 1: Selecionar e Mapear Elementos do HTML
Antes de dar vida à tela, selecione os elementos no JavaScript. No arquivo `script.js`:
- Use `document.querySelector` ou `document.getElementById` para referenciar os dois formulários (Manual e da API), os botões, os inputs de texto e número, a lista `<ul id="study-list">`, e as tags de mensagens (`#feedback`, `#api-feedback`, `#status-message`, `#empty-state`).
- Guarde tudo em variáveis (ex: `const studyForm = document.getElementById('study-form');`).
- Teste com `console.log()` para ter a certeza de que capturaram as tags corretamente.

### Passo 2: Funcionalidade de Adicionar Item Manualmente
1. Adicione um evento (`addEventListener`) do tipo `submit` no formulário manual.
2. Sempre use `event.preventDefault()` para evitar o recarregamento natural da página.
3. Valide o que foi digitado:
   - Se estiver vazio ou tiver menos de 3 letras, exiba a mensagem de erro na tag de feedback, insira classes de estilo erro (se existirem no CSS) e **interrompa** a execução (use um `return`).
   - Se for válido: Siga o fluxo, chame a função para criar o item na lista (descrita no passo abaixo), limpe o campo e esconda o texto de "estado vazio" (`#empty-state`).

### Passo 3: Criação de um Novo Item na Lista
Crie uma função genérica e isolada – por exemplo, `createStudyItem(titulo)` – para ser reaproveitada sempre que precisar colocar algo na tela (seja do input manual ou da API).
1. Na função, utilize `document.createElement('li')`.
2. Adicione o texto (título do elemento `li`).
3. Crie internamente outro elemento de botão para "Remover".
4. Junte as duas tags e anexe na lista `<ul>` usando `appendChild()` ou `append()`.

### Passo 4: Delegação de Eventos para Remoção
Em listas dinâmicas, se usarmos `.addEventListener('click')` direto em cada botão de excluir recém-criado, a performance é afetada. Use o conceito de Delegação:
1. Adicione o evento de `click` direto na sua lista pai (`<ul>`).
2. Quando ocorrer um clique, verifique quem originou a ação lendo a propriedade `event.target`.
3. Se o elemento clicado condizer ao "*botão de remover*", identifique qual é o seu "Pai" (a tag `<li>`) e use o método `.remove()` no próprio HTML para apagá-lo!
4. Valide se a lista ficou "sem filhos". Se sim, retorne a exibir o parágrafo escondido *"Nenhum item na lista ainda"*.

### Passo 5: Consumo de API Externa e Assincronismo
1. Crie o ouvinte (`submit`) no segundo formulário (Sugestões da API) para tratar o clique.
2. Resgate o valor inserido no campo User ID.
3. Em uma função assíncrona (`async`), exiba a mensagem visual *"Carregando sugestões da API..."*.
4. Use a função nativa `fetch()` na URL `https://jsonplaceholder.typicode.com/todos`. Se houver o ID preenchido pelo usuário, aplique um parâmetro (exemplo de template string na URL: `?userId=${seuUserIdAQUI}`). Aguarde o retorno com `await fetch...`.
5. Extraia o `JSON` (`await response.json()`).
6. Remova a mensagem visual de carregamento.
7. Com os objetos que a API devolveu prontos num Array, passe as informações por um `forEach()` (ou laço `for` simples) chamando cada item encontrado na função `createStudyItem(titulo)` que você criou mais cedo!

### Passo 6: "Recarregar última busca"
No bloco cabeçalho da seção inferior existe um botão: "Recarregar ultima busca".
- Crie um comportamento simples para ele: Apenas salve a última URL ou últimos parâmetros validados, guardando-os numa variável global (`let`).
- Crie um clique (`click`) nesse botão `#reload-button` para efetuar exatamente a mesma Requisição do item 5 usando estes mesmos dados guardados.

---

## 🚀 Como Postar no GitHub a sua Entrega (Tutorial)

Tudo funcionando perfeitamente igual ao esperado? É hora de entregar o seu código hospendando-o no [GitHub](https://github.com/):

1. Vá para o GitHub, faça o *Log-In* e encontre o ícone de botão verde para novo repositório ou pelo **"+" -> New repository**.
2. **Repository Name:** Dê o nome de sua preferência (`ex: ap1-frontend`).
3. Marque a opção de Acesso como **Public** (*Não use Private ou seu repositório não constará como visível para ser avaliado!*).
4. Confirme para **Create Repository**.

### Subindo os Arquivos
Você pode escolher a forma mais familiar de subir seus arquivos da AP1:

**Maneira A: O jeito rápido pelo Site (Upload)**
1. Na tela do projeto recém-gerado, procure pelo Hyperlink chamado *"uploading an existing file"* no meio do site.
2. Arraste do seu computador todos os seus arquivos editados (a pasta inteira do workspace, com `index.html` e a raiz que envelopa todos os assets), de modo a deixar a arvore limpa na raiz.
3. Confirme em _Commit Changes_.

**Maneira B: O jeito Dev (Local via Terminal Git)**
Abra seu terminal na própria pasta `TDE04` do VSCode e mande a clássica sequência Git:
```bash
git init
git add .
git commit -m "Entrega da primeira versao AP1"
git branch -M main
git remote add origin SUA_URL_DO_REPOSITORIO_GIT.git
git push -u origin main
```

### Finalizando a Entrega
- Quando a pasta subir e você avistar os arquivos e este `README.md` estilizado na página do seu Repositório do GitHub, copie o link na barra de Endereço (URL). Exemplo: `https://github.com/SeuNomePessoal/ap1-frontend`
- Insira esse link na plataforma oficial do Professor como a **Sua Entrega da AP1**.

**(Bônus)** Vá na aba **Settings** do repósitorio > **Pages**, escolha sua branch `main` e aguarde alguns minutos, o próprio GitHub vai soltar um link do seu site "no Ar"! Pode colocar na entrega do seu trabalho junto!

😎 Bom código e divirta-se!
