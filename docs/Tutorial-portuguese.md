---
id: tutorial
title: Tutorial
layout: docs
category: The Basics
permalink: docs/tutorial.html
next: props
previous: getting-started
---

React Native é como React; mas ele usa componentes nativos no lugar de componentes web como elementos fundamentais. Assim, para compreender a estrutura básica dum app de React Native, você necessita entender alguns dos conceitos básicos de React, tais como JSX, componentes, `state` e `props`. Se você já conhece React, você ainda precisa aprender algumas paradas específicas de React Native, tais como os seus componentes nativos. Este tutorial é voltado para todas as audiências, tenha você experiência com React ou não.

Vamos lá fazer este treco!

## Alô Mundo (Hello World)

Em conformidade com as tradições antigas de nosso povo, devemos primeiro desenvolver um app que não faça nada exceto dizer "Hello world". Aqui está ele:

```ReactNativeWebPlayer
import React, { Component } from 'react';
import { AppRegistry, Text } from 'react-native';

export default class HelloWorldApp extends Component {
  render() {
    return (
      <Text>Hello world!</Text>
    );
  }
}

// skip this line if using Create React Native App
AppRegistry.registerComponent('AwesomeProject', () => HelloWorldApp);
```

Se você estiver se sentindo curioso, você já pode brincar com o programa-exemplo diretamente nos simuladores de web. Você pode igualmente colá-lo dentro do seu arquivo `App.js`, `index.ios.js`, ou `index.android.js` para criar um app de verdade na sua máquina local.

## O que está se passando aqui?

Algumas das coisas daqui podem não parecer muito com JavaScript pra você. Não se desespere! _Isto é o futuro_.

Primeiro de tudo, o ES2015 (também conhecido como ES6) é um conjunto de melhoramentos para o JavaScript que é agora parte do padrão oficial, mas não ainda supportado por todos os navegadores, que muitas das vezes ainda não se é usado no desenvolvimento web. React Native vem acompanhado com suporte a ES2015; portanto você pode usar todo este material sem se preocupar sobre compatibilidade. `import`, `from`, `class`, `extends` e a sintaxe `() =>` no exemplo acima são todos funcionalidades do ES2015. Se você ainda não estiver familiarizado com o ES2015, você pode provavelmente assimilá-lo apenas por ler atentamente exemplos de código como este tutorial possui. Se quiser, [esta página](https://babeljs.io/learn-es2015/) tem um bom apanhado das funcionalidades do ES2015.

A outra coisa inusitada neste exemplo de código é `<Text>Hello world!</Text>`. Este é o JSX - uma sintaxe para incorporar XML dentro do JavaScript. Muitos frameworks usam uma linguagem especial de templates que lhe permite inserir códigos dentro da linguagem de markup. Em React, isto é o reverso. O JSX permite que você escreva a sua linguagem de markup dentro do programa. Parece igual HTML na web, exceto que no lugar de coisas de web como `<div>` or `<span>`, você usa componentes React. Neste caso, `<Text>` é um componente embutido que apenas exibe algum texto.

## Componentes

Então este programa está definindo o `HelloWorldApp`, um `Component` novo. Quando você estiver desenvolvendo um app em React Native, você estará criando novos componentes abundantemente. Qualquer coisa que você enxergar na tela é algum tipo de componente. Um componente pode ser bastante simples - a única coisa que é exigida é uma função para `render`, a qual retorna algum JSX para renderizar.

## Projetos só com código nativo

No exemplo particular acima, o `HelloWorldApp` está registrado com o `AppRegistry`. O `AppRegistry` apenas diz ao React Native qual componente é a raiz para a aplicação inteira. Está incluído nestes exemplos; portanto você pode colar a coisa toda dentro do seu arquivo `index.ios.js` ou `index.android.js` e tê-la já rodando. Se você tiver um projeto de Create React Native App, isto é gerido automaticamente para você e não é necessário chamar `AppRegistry` no seu programa.

## Este app não faz muitíssimo

Boa observação! Para fazer os componentes produzirem coisas mais interessantes, você necessita [aprender sobre Props](docs/props.html).
