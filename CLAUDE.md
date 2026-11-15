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
