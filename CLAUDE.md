# Caixa Burger do Rei — guia do projeto

Caixa diário, visão gerencial, produção, compras, agenda financeira e pagamentos de motoboy da hamburgueria Burger do Rei. Detalhes funcionais no `README.md`.

## Publicação
- GitHub Pages da branch `main` (https://marcelomreidogado-cmd.github.io/caixa-burger-do-rei/). Push na `main` publica sozinho. `.nojekyll` mantém o site estático.

## Arquitetura
- `index.html` é o app inteiro (~115 KB, sem build). Versão no `<title>` (atual: v10.4).
- Firebase **modular** 10.12.2 (`firebase-app.js`/`firebase-firestore.js`, ES modules), Chart.js 4.4.1.
- Firebase projeto `studio-1719325280-f2519`. Coleções: `caixa`, `motoboys`, `producao`, `compras`, `moedas`, `depositos_caixa`.
- Telas (`data-view`): `cash` (Caixa Diário), `overview` (Visão gerencial), `production`, `purchases`, `motoboy`, `schedule` (Agenda Financeira).
- Gravação **por célula** (não reescreve o dia inteiro) para permitir edição simultânea em vários computadores; edições locais são preservadas até a confirmação do servidor.
- Canais de venda incluem iFood e 99Food (`vendas.food99`; dias antigos sem o campo = 0, sem migração). Repasse 99Food: vendas de seg–dom caem na quarta seguinte.

## Integrações
- O **Financeiro Burger** (repo `financeiro-burgerdorei`) lê a coleção `caixa` e usa travas próprias (`caixa_fechamento_guards`, `caixa_integracao_locks`). Mudanças no formato de `caixa` precisam ser conferidas lá.

## Fluxo de trabalho
- Editar → `node --check` no script extraído → testar contra o Firestore Emulator (nunca no banco de produção) → atualizar versão no título e o README → commit em português.
- Não reescrever o histórico do Firestore; campos novos devem ser opcionais (compatíveis com dias antigos).
- Usuário (Marcelo) trabalha em português do Brasil, no Mac, e prefere soluções simples, sem terminal.

## Padrão visual (obrigatório em toda mudança)
Polimento visual feito em 15/11/2026. Para não regredir (o Compras piorou em 16–17/11 por isso):
- **Não colocar estilo solto (`style="..."`) em linhas de tabela, listas ou cartões.** Criar ou reutilizar classes no bloco de CSS do projeto (indicado abaixo). Estilo inline só para valores dinâmicos (cor de loja, largura de barra).
- **Tabelas compactas:** cada linha de produto/cliente/lançamento cabe em ~2 linhas de texto. Controles extras (marcações, botões) ficam pequenos e na mesma linha; detalhes vão para um modal ou para a dica (`title`).
- **Nada passa da largura da tela**, exceto tabelas largas dentro de um contêiner que desliza (com a coluna de nome fixa à esquerda no celular).
- **Celular primeiro:** conferir em 390 px e em 1440 px. No celular: navegação numa faixa/barra única, filtros e chips em faixa que desliza, indicadores em 2 colunas, textos sem cortar no meio da palavra.
- **Números** com algarismos alinhados (`font-variant-numeric: tabular-nums`), sem fonte monoespaçada; valores com sinal não quebram linha.
- Reaproveitar as cores, raios, botões e chips que o sistema já usa — não criar um estilo novo para cada tela.

### Conferência antes de publicar
1. Abrir o sistema com **dados fictícios** e **sem acesso ao banco real** (veja "Como testar o visual" abaixo).
2. Fotografar as telas alteradas em 390 px e 1440 px (Playwright já instalado no ambiente; Chromium em `/opt/pw-browsers`).
3. Medir que `document.documentElement.scrollWidth` não passa da largura da janela em todas as abas.
4. Mostrar ao Marcelo as fotos de **antes e depois** na resposta e dizer o que não foi testado.

### Onde fica o visual / como testar o visual
- CSS no fim do `<style>` do `index.html` ("POLIMENTO VISUAL (nov/2026)"). Breakpoints usados: 720 px e 480 px.
- Teste: Playwright interceptando `gstatic.com/firebasejs/10.12.2/firebase-app.js` e `firebase-firestore.js` com módulos falsos (`initializeApp`, `getFirestore`, `collection`, `onSnapshot` devolvendo dias fictícios em `caixa`) e servindo o Chart.js 4.4.1 do npm. Navegar clicando nos `[data-view]`.
