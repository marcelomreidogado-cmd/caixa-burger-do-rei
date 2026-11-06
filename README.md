# Caixa Burger do Rei

Sistema de caixa diário, visão gerencial e pagamentos de motoboy, com salvamento e sincronização pelo Firebase.

**Acesso:** https://marcelomreidogado-cmd.github.io/caixa-burger-do-rei/

## Atualizações

O GitHub Pages publica o conteúdo da raiz da branch `main`. Alterações enviadas a essa branch atualizam o site automaticamente. Não é necessário publicar pelo Firebase Hosting.

`index.html` é o único arquivo do aplicativo. `.nojekyll` mantém a publicação estática direta. A versão atual é a v10.2, com 99Food após iFood no Caixa Diário, total por plataforma e inclusão no faturamento e nos gráficos. Permanecem os 12 botões de meses, o layout responsivo e a navegação entre anos.

A 99Food usa o campo `vendas.food99`, salvo por célula. Dias antigos sem esse campo exibem zero; não há migração ou regravação do histórico. Novos dias já incluem o canal. Os repasses ocorrem às quartas-feiras, mas falta confirmar o período de fechamento das vendas: por isso, a Agenda Financeira mostra o valor mensal da 99Food com essa informação, fora das datas e totais de recebimentos previstos até a confirmação.

## Dados e sincronização

O aplicativo mantém o projeto Firebase `studio-1719325280-f2519` (Caixa Burger) e as coleções usadas pela v10. O GitHub hospeda a interface; o Firestore mantém os lançamentos e a sincronização entre computadores.

Os dados são carregados do Firestore. Não há cópia dos lançamentos nem importação automática incorporada ao HTML. Atualizar o site não reinicia nem substitui os dados do banco. As regras e permissões existentes do Firebase foram mantidas.

## Validação

A alteração passou por 16 verificações locais: navegação pelos 12 meses e por anos, meses vazios, seis larguras de tela entre 320 e 1440 px, seleção por teclado, seis abas, inclusão e exclusão, pagamentos de motoboy e duas sessões com edição concorrente de células distintas no Firestore Emulator. Os testes mantêm o banco de produção separado.

A v10.2 acrescentou 11 verificações para a 99Food: compatibilidade com dias antigos, ordem e alinhamento da coluna, valores com vírgula decimal, somas, gráficos e percentuais, dia com venda somente na plataforma, gravação concorrente com iFood, recarregamento, novo dia, valor zerado e apresentação dos repasses sem período de fechamento confirmado.

## Reverter uma atualização

Reverta o commit correspondente na branch `main`. O GitHub Pages publicará novamente a versão anterior da interface. A reversão do site não altera os lançamentos do Firestore.

[Funcionamento da publicação automática no GitHub Pages](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site).
