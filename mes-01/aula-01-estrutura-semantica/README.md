# Aula 1: Estrutura de documento e HTML semântico

> **Meta do dia:** entender o que cada linha do "esqueleto" HTML faz e por que tags semânticas importam no mercado.

---

## 0. Aquecimento (15 min, sem consultar nada)

Antes de ler o resto, abra um arquivo vazio e escreva **de memória** a estrutura mínima de uma página HTML.
Pode errar. O objetivo é descobrir o que você ainda lembra do curso do Guanabara. Depois compare com a seção 1.

---

## 1. O esqueleto, linha por linha

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Seu Nome | Desenvolvedor Front-End</title>
  <meta name="description" content="Portfólio de desenvolvedor front-end.">
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <!-- conteúdo visível -->
  <script src="script.js" defer></script>
</body>
</html>
```

| Linha | O que faz | Por que importa |
|---|---|---|
| `<!DOCTYPE html>` | Avisa ao navegador que é HTML5 | Sem ele, o navegador entra no *quirks mode*, imita navegadores antigos e o CSS passa a se comportar de forma estranha |
| `lang="pt-BR"` | Declara o idioma | O leitor de tela pronuncia com a voz certa, o Google entende o idioma e o tradutor automático funciona |
| `charset="UTF-8"` | Codificação de caracteres | Sem ele, "ação" pode aparecer como "aÃ§Ã£o" |
| `viewport` | Faz o celular usar a largura real da tela | Sem ele, o celular finge ter 980px e o site fica minúsculo. **Responsividade começa aqui** |
| `<title>` | Texto da aba e título no Google | SEO e usabilidade: é o que aparece no histórico e nos favoritos |
| `description` | Resumo exibido no Google | Aumenta a taxa de clique nos resultados |
| `defer` | Baixa o JS em paralelo e só executa depois que o HTML foi lido | O JS não trava a renderização e já encontra o DOM pronto. É o padrão moderno |

> 💡 **Atalho do VS Code:** digite `!` e aperte Tab. Mas só use depois de saber escrever tudo sozinho.

---

## 2. HTML semântico: o porquê

Compare estes dois trechos. Os dois ficam **idênticos na tela**:

```html
<!-- ❌ "div soup" -->
<div class="topo">
  <div class="menu">...</div>
</div>
<div class="conteudo">
  <div class="post">...</div>
</div>
<div class="rodape">...</div>
```

```html
<!-- ✅ semântico -->
<header>
  <nav>...</nav>
</header>
<main>
  <article>...</article>
</main>
<footer>...</footer>
```

Por que o mercado exige a segunda versão:

1. **Acessibilidade:** leitores de tela transformam essas tags em "landmarks". A pessoa cega aperta uma tecla e pula direto para o `<main>` ou para a `<nav>`. Com `<div>`, ela precisa ouvir a página inteira.
2. **SEO:** o Google entende o que é conteúdo principal e o que é menu ou rodapé.
3. **Manutenção:** outro dev abre o arquivo e entende a estrutura sem ler o CSS.
4. **Entrevistas:** "Qual a diferença entre `section`, `article` e `div`?" é uma pergunta clássica de vaga júnior.

### As tags principais

| Tag | Quando usar | Teste rápido |
|---|---|---|
| `<header>` | Cabeçalho da página ou de uma seção/artigo | Introduz algo? |
| `<nav>` | Bloco de **navegação principal** | São links para outras partes do site? |
| `<main>` | Conteúdo principal. **Apenas um por página** | Se eu remover menu e rodapé, é isso que sobra? |
| `<article>` | Conteúdo **independente**, que faria sentido sozinho | Daria para publicar em outro site e ainda fazer sentido? (post, card de produto, comentário) |
| `<section>` | Agrupamento temático **com título** | Tem (ou deveria ter) um `<h2>`/`<h3>`? |
| `<aside>` | Conteúdo relacionado, mas secundário | Se eu remover, o conteúdo principal continua completo? |
| `<footer>` | Rodapé da página ou de um artigo | Créditos, contato, links legais? |
| `<div>` | **Só para estilo/layout**, quando nenhuma tag acima serve | Não tem significado? Então é `div` |

### Hierarquia de títulos

- Um `<h1>` por página: o assunto principal.
- **Nunca pule níveis** (`h2` → `h4`). Leitores de tela usam os títulos como sumário.
- Escolha o título pelo **significado**, nunca pelo tamanho. Tamanho se resolve no CSS.

---

## 3. Erros que eu vejo todo dia em código júnior

| Erro | Por que é ruim | Correção |
|---|---|---|
| `<br><br><br>` para dar espaço | Mistura estrutura com aparência | `margin` no CSS |
| `<img src="foto.jpg">` sem `alt` | Leitor de tela lê o nome do arquivo | `alt="Descrição útil"` ou `alt=""` se for decorativa |
| `<div onclick="...">` como botão | Não recebe foco do teclado e não é anunciado como botão | `<button type="button">` |
| `<h3>` só porque "é menor" | Quebra a hierarquia | Use o nível correto e ajuste o tamanho no CSS |
| `<section>` sem título | Vira uma `div` com nome errado | Adicione um título ou use `div` |

---

## 4. Como um sênior pensa

Antes de escrever qualquer tag, ele **desenha caixas no papel**: "isto é o cabeçalho, isto é navegação, isto é conteúdo principal, cada card é um artigo". O HTML sai depois, e o CSS por último.
**Estrutura → apresentação → comportamento** (HTML → CSS → JS).

---

## 5. Exercícios

Crie cada exercício como arquivo nesta pasta.

### Exercício 1: `ex1-sobre-mim.html` (fixação)
Página "Sobre mim" **só com HTML** (sem CSS), contendo:
- `header` com seu nome (`h1`) e uma `nav` com 3 links âncora (`#sobre`, `#habilidades`, `#contato`)
- `main` com 3 `section`, cada uma com `id` e `h2`
- Uma lista (`ul`) de tecnologias que você quer aprender
- Uma imagem com `alt` adequado (pode ser de https://picsum.photos)
- `footer` com o ano e um link para seu GitHub

### Exercício 2: `ex2-refatoracao.html` (refatoração)
Transforme esta "div soup" em HTML semântico. Justifique **em comentários HTML** cada escolha:

```html
<div class="header">
  <div class="logo">TechNews</div>
  <div class="links">
    <a href="/">Início</a> <a href="/tecnologia">Tecnologia</a>
  </div>
</div>
<div class="content">
  <div class="news">
    <div class="title">React 20 é lançado</div>
    <div class="date">25/11/2026</div>
    <div class="text">A nova versão traz...</div>
  </div>
  <div class="news">
    <div class="title">CSS ganha nova feature</div>
    <div class="text">Agora é possível...</div>
  </div>
  <div class="sidebar">Mais lidas: ...</div>
</div>
<div class="footer">© 2026 TechNews</div>
```

> Dica: pesquise a tag `<time datetime="...">`.

### Desafio: `desafio-blog.html`
Estruture (só HTML) a página de um **post de blog completo**: cabeçalho do site, o post com autor e data, seção de comentários (cada comentário é o quê? 🤔), barra lateral com posts relacionados e rodapé.
Depois valide em https://validator.w3.org/#validate_by_input e corrija tudo o que ele apontar.

---

## 6. Git: seu primeiro commit do curso

No terminal, na pasta `ClaudeTeacher`:

```powershell
git init
```
```powershell
git add .
```
```powershell
git commit -m "feat: aula 01 - estrutura e HTML semântico"
```

> O padrão `feat:`, `fix:`, `docs:` se chama **Conventional Commits** e é usado em muitas empresas. Já comece com ele.

---

## ✅ Checklist de entrega

- [ ] Aquecimento feito de memória
- [ ] Exercícios 1 e 2 feitos
- [ ] Desafio feito e validado no W3C sem erros
- [ ] Commit realizado
- [ ] Me pedir: **"revisa a aula 1"**

### Perguntas de entrevista (responda com suas palavras no `DIARIO.md`)
1. Para que serve a meta tag `viewport`?
2. Qual a diferença entre `article`, `section` e `div`?
3. Por que não usar `div` com `onclick` no lugar de `button`?
