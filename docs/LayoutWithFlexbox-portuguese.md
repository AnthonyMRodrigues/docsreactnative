---
id: flexbox
title: Layout with Flexbox
layout: docs
category: The Basics
permalink: docs/flexbox.html
next: handling-text-input
previous: height-and-width
---

Os componentes podem especificar o layout dos seus descendentes usando o algoritmo flexbox. O Flexbox é projetado para prover um layout consistente para diferentes tamanhos de tela.

Você normalmente utilizará uma combinação de `flexDirection`, `alignItems`, e `justifyContent` para se chegar ao layout correto.

> O Flexbox funciona da mesma forma no React Native quanto no CSS na web, com algumas poucas exceções. Os defaults são diferentes; com o `flexDirection` predefinido com `column` ao invés de `row`, e o parâmetro `flex` com suporte apenas de um só número.

#### Direcionamento Flex

Adicionar `flexDirection` a um `style` do componente determina o **eixo primário** de seu layout. É para os descendentes serem organizados horizontalmente (`row`) ou verticalmente (`column`)? O default é `column`.

```ReactNativeWebPlayer
import React, { Component } from 'react';
import { AppRegistry, View } from 'react-native';

export default class FlexDirectionBasics extends Component {
  render() {
    return (
      // Try setting `flexDirection` to `column`.
      <View style={{flex: 1, flexDirection: 'row'}}>
        <View style={{width: 50, height: 50, backgroundColor: 'powderblue'}} />
        <View style={{width: 50, height: 50, backgroundColor: 'skyblue'}} />
        <View style={{width: 50, height: 50, backgroundColor: 'steelblue'}} />
      </View>
    );
  }
};

// skip this line if using Create React Native App
AppRegistry.registerComponent('AwesomeProject', () => FlexDirectionBasics);
```

#### Justificar Conteúdo

Adicionar `justifyContent` a um `style` do componente determina a **distribuição** dos descendentes ao longo do **eixo primário**. É para os descendentes serem distribuídos pelo começo, pelo centro, pelo final, ou espaçados uniformemente? As opções disponíveis são `flex-start`, `center`, `flex-end`, `space-around`, e `space-between`.

```ReactNativeWebPlayer
import React, { Component } from 'react';
import { AppRegistry, View } from 'react-native';

export default class JustifyContentBasics extends Component {
  render() {
    return (
      // Try setting `justifyContent` to `center`.
      // Try setting `flexDirection` to `row`.
      <View style={{
        flex: 1,
        flexDirection: 'column',
        justifyContent: 'space-between',
      }}>
        <View style={{width: 50, height: 50, backgroundColor: 'powderblue'}} />
        <View style={{width: 50, height: 50, backgroundColor: 'skyblue'}} />
        <View style={{width: 50, height: 50, backgroundColor: 'steelblue'}} />
      </View>
    );
  }
};

// skip this line if using Create React Native App
AppRegistry.registerComponent('AwesomeProject', () => JustifyContentBasics);
```

#### Alinhar Itens

Adicionar `alignItems` a um `style` do componente determina o **alinhamento** dos descendentes ao longo do **eixo secundário** (se o eixo primário for `row`, então o secundário é `column`, e vice-versa). É para os descendentes serem alinhados pelo começo, pelo centro, pelo final, or alargados para ocupar tudo? As opções disponíveis são `flex-start`, `center`, `flex-end`, e `stretch`.

> Para que o `stretch` tenha algum efeito, os descendentes não devem ter dimensão fixa ao longo do eixo secundário. No exemplo a seguir, definir `alignItems: stretch` não faz nada até que o `width: 50` seja removido dos descendentes.

```ReactNativeWebPlayer
import React, { Component } from 'react';
import { AppRegistry, View } from 'react-native';

export default class AlignItemsBasics extends Component {
  render() {
    return (
      // Try setting `alignItems` to 'flex-start'
      // Try setting `justifyContent` to `flex-end`.
      // Try setting `flexDirection` to `row`.
      <View style={{
        flex: 1,
        flexDirection: 'column',
        justifyContent: 'center',
        alignItems: 'center',
      }}>
        <View style={{width: 50, height: 50, backgroundColor: 'powderblue'}} />
        <View style={{width: 50, height: 50, backgroundColor: 'skyblue'}} />
        <View style={{width: 50, height: 50, backgroundColor: 'steelblue'}} />
      </View>
    );
  }
};

// skip this line if using Create React Native App
AppRegistry.registerComponent('AwesomeProject', () => AlignItemsBasics);
```

#### Indo Mais Fundo

Cobrimos o básico; porém há muitos outros estilos que você pode precisar para os layouts. A lista completa das props que controlam o layout está documentada [aqui](./docs/layout-props.html).

Estamos já chegando perto de sermos capazes de desenvolver um aplicativo de verdade. Uma coisa que ainda está nos faltando é uma maneira de pegar o input do usuário; então vamos prosseguir para [aprendermos como operar a entrada de textos com o componente TextInput](docs/handling-text-input.html).
