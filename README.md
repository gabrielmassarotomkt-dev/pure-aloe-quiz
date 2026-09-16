# Quiz Pure Aloe — Diagnóstico Capilar

Página única (`index.html`), sem dependências externas além da fonte do Google Fonts. Pronta para `diagnostico.purealoe.com.br` via GitHub Pages, na conta `gabrielmassarotomkt-dev` — mesmo esquema já usado em `agendamento.purealoe.com.br`.
O arquivo `CNAME` já vem preenchido com `diagnostico.purealoe.com.br`, então o GitHub configura o domínio customizado sozinho assim que você fizer o primeiro push (não precisa digitar nada em Settings → Pages).

## 1. Criar o repositório no GitHub

Pelo site: [github.com/new](https://github.com/new)
- Owner: `gabrielmassarotomkt-dev`
- Repository name: `pure-aloe-quiz` (ou o nome que preferir — só ajuste no comando abaixo)
- Visibilidade: Public (GitHub Pages grátis exige repositório público, a menos que sua conta tenha GitHub Pro/organização paga)
- Não marque "Add a README" — vamos subir os arquivos já prontos.

## 2. Subir os arquivos

Dentro da pasta `pure-aloe-quiz` (a que você recebeu):

```bash
cd pure-aloe-quiz
git init
git add .
git commit -m "Quiz de diagnóstico capilar Pure Aloe"
git branch -M main
git remote add origin https://github.com/gabrielmassarotomkt-dev/pure-aloe-quiz.git
git push -u origin main
```

Se pedir login, use um Personal Access Token no lugar da senha (GitHub não aceita mais senha comum via git). Se você já usa GitHub Desktop ou o `gh` CLI autenticado na sua máquina, pode criar o repositório e subir por ali também — o resultado final é o mesmo.

## 3. Ativar o GitHub Pages

1. No repositório novo, vá em Settings → Pages.
2. Em "Build and deployment" → Source, selecione Deploy from a branch.
3. Branch: `main`, pasta: `/ (root)`. Salve.
4. Confirme que em "Custom domain" já aparece `diagnostico.purealoe.com.br` (veio do arquivo `CNAME`). Se não aparecer, digite manualmente e salve.
5. Marque Enforce HTTPS assim que a opção ficar disponível (só libera depois que o DNS abaixo propagar).

## 4. Criar o registro de DNS

No mesmo painel de DNS onde está o registro de `agendamento.purealoe.com.br`, adicione um novo registro seguindo o mesmo padrão:

| Tipo  | Nome                          | Valor                                |
|-------|-------------------------------|---------------------------------------|
| CNAME | `diagnostico.purealoe.com.br` | `gabrielmassarotomkt-dev.github.io`   |

(No campo "Nome"/"Host" alguns painéis pedem só `diagnostico`, sem o domínio completo — depende do provedor; siga o mesmo formato que você usou no registro do `agendamento`.)

A propagação costuma levar de minutos a algumas horas. Depois disso, o quiz estará no ar em `https://diagnostico.purealoe.com.br`.

## 5. Editar o número de WhatsApp, textos ou o vídeo de depoimento

Tudo está no arquivo `index.html`:
- Número do WhatsApp: constante `WHATSAPP_NUMBER` no `<script>`.
- Perguntas, opções e pontuação: array `questions`.
- Textos dos resultados: objeto `tierContent`.
- Vídeo de depoimento: atributo `data-video-id` na `<div class="testimonial-video">` (ID do vídeo do YouTube) e o `src` da thumbnail logo abaixo.

Não há build step — é só editar e commitar (`git add . && git commit -m "ajuste" && git push`). O GitHub Pages atualiza sozinho em 1-2 minutos.

## 6. Testar localmente antes de subir

Não abra o `index.html` só com duplo clique — o player de vídeo (e outros recursos que dependem de rede) pode não carregar corretamente em arquivos abertos direto do disco (`file://`). Rode um servidor local:

```bash
cd pure-aloe-quiz
python3 -m http.server 8000
```

E acesse `http://localhost:8000` no navegador. Depois de publicado no GitHub Pages, tudo funciona normalmente.
