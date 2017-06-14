---
id: height-and-width
title: Height and Width
layout: docs
category: The Basics
permalink: docs/height-and-width.html
next: flexbox
previous: style
---

O width e o height de um componente determina o seu tamanho na tela.

#### Dimensões Fixas

A maneira mais simples para definir as dimensões dum componente é adicionando `width` e `height` fixas ao estilo. Todas as dimensões no React Native não possuem unidades de medida, e representam tão somente pixels com densidade autônoma.

```ReactNativeWebPlayer
import React, { Component } from 'react';
import { AppRegistry, View } from 'react-native';

export default class FixedDimensionsBasics extends Component {
  render() {
    return (
      <View>
        <View style={{width: 50, height: 50, backgroundColor: 'powderblue'}} />
        <View style={{width: 100, height: 100, backgroundColor: 'skyblue'}} />
        <View style={{width: 150, height: 150, backgroundColor: 'steelblue'}} />
      </View>
    );
  }
}

// skip this line if using Create React Native App
AppRegistry.registerComponent('AwesomeProject', () => FixedDimensionsBasics);
```

Definir dimensões desta forma é comum para componentes que devem sempre renderizar com exatamente o mesmo tamanho, independentemente das dimensões da tela.

#### Dimensões Flex

Use `flex` num estilo de componente para fazer com que o componente expanda-se e encolha-se dinamicamente baseado no espaço disponível. Normalmente você utilizará `flex: 1`, que diz a um componente para ocupar todo o espaço disponível, repartido uniformemente por entre cada outro componente com o mesmo progenitor. Quanto maior o `flex` dado, mais elevado a proporção de espaço que um componente tomará em relação aos seus irmãos.

> Um componente pode somente se expandir para preencher o espaço disponível se o seu progenitor tiver dimensões maiores do que 0. Se um progenitor não tiver nem o `width` e o `height` fixos nem o `flex`, este progenitor terá as dimensões de 0 e os seus filhos `flex` não serão visíveis.

```ReactNativeWebPlayer
import React, { Component } from 'react';
import { AppRegistry, View } from 'react-native';

export default class FlexDimensionsBasics extends Component {
  render() {
    return (
      // Try removing the `flex: 1` on the parent View.
      // The parent will not have dimensions, so the children can't expand.
      // What if you add `height: 300` instead of `flex: 1`?
      <View style={{flex: 1}}>
        <View style={{flex: 1, backgroundColor: 'powderblue'}} />
        <View style={{flex: 2, backgroundColor: 'skyblue'}} />
        <View style={{flex: 3, backgroundColor: 'steelblue'}} />
      </View>
    );
  }
}

// skip this line if using Create React Native App
AppRegistry.registerComponent('AwesomeProject', () => FlexDimensionsBasics);
```

Logo que você conseguir controlar o tamanho de um componente, o próximo passo é [aprender como posicioná-lo na tela](docs/flexbox.html).
