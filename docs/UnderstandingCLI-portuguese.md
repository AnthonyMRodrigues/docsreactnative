---
id: understanding-cli
title: Understanding the CLI
layout: docs
category: Guides
permalink: docs/understanding-cli.html
banner: ejected
next: native-modules-ios
previous: testing
---

Embora você possa ter instalado o `react-native-cli` via npm como um módulo separado, ele é um shell para accessar o CLI integrado
ao React Native de cada projeto. Os seus comandos e os efeitos deles são dependentes da versão do módulo do `react-native`
no contexto do projeto. Este guia dará uma breve visão geral do CLI no módulo.

# O CLI local

O React Native tem uma pasta [`local-cli`](https://github.com/facebook/react-native/tree/master/local-cli) com um arquivo chamado
[`cliEntry.js`](https://github.com/facebook/react-native/blob/master/local-cli/cliEntry.js). Daqui, os comandos são lidos
do `commands.js` e adicionados como possíveis comandos de CLI. Como por exemplo o comando `react-native link` existe na pasta [`react-native/local-cli/link`](https://github.com/facebook/react-native/blob/master/local-cli/link/), e é
requisitado em `commands.js`, o qual o registrará como um comando documentado a ser exposto ao CLI.

# Definições dos comandos

No final de cada entrada de comando tem um export. O export é um objeto com uma função para executar, a descrição do comando, e o nome do comando. A estrutura do objeto para o comando `link` parece assim:

```js
module.exports = {
  func: link,
  description: 'links all native dependencies',
  name: 'link [packageName]',
};
```

### Parâmetros

O nome do comando identifica os parâmetros que um comando esperaria. Quando o parâmetro do comando estiver envolto pelos símbolos maior-que e menor-que `< >`, isto indica que o parâmetro é esperado. Quando um parâmetro do comando estiver envolto por colchetes `[ ]`, isto indica que o parâmetro é opcional.
