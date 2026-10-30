# Caixa Burger do Rei

Sistema de caixa diário, visão gerencial e pagamentos de motoboy, com salvamento e sincronização pelo Firebase.

**Acesso:** https://marcelomreidogado-cmd.github.io/caixa-burger-do-rei/

## Atualizações

O GitHub Pages publica o conteúdo da raiz da branch `main`. Alterações enviadas a essa branch atualizam o site automaticamente. Não é necessário publicar pelo Firebase Hosting.

`index.html` é o único arquivo do aplicativo. `.nojekyll` mantém a publicação estática direta. A versão atual é a v10.1, com 12 botões de meses no Caixa Diário, destaque do mês selecionado, layout responsivo e navegação entre anos.

## Dados e sincronização

O aplicativo mantém o projeto Firebase `studio-1719325280-f2519` (Caixa Burger) e as coleções usadas pela v10. O GitHub hospeda a interface; o Firestore mantém os lançamentos e a sincronização entre computadores.

Os dados são carregados do Firestore. Não há cópia dos lançamentos nem importação automática incorporada ao HTML. Atualizar o site não reinicia nem substitui os dados do banco. As regras e permissões existentes do Firebase foram mantidas.

## Validação

A alteração passou por 16 verificações locais: navegação pelos 12 meses e por anos, meses vazios, seis larguras de tela entre 320 e 1440 px, seleção por teclado, seis abas, inclusão e exclusão, pagamentos de motoboy e duas sessões com edição concorrente de células distintas no Firestore Emulator. Os testes mantêm o banco de produção separado.

## Reverter uma atualização

Reverta o commit correspondente na branch `main`. O GitHub Pages publicará novamente a versão anterior da interface. A reversão do site não altera os lançamentos do Firestore.

[Funcionamento da publicação automática no GitHub Pages](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site).
