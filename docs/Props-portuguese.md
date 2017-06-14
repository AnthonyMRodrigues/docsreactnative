---
id: props
title: Props
layout: docs
category: The Basics
permalink: docs/props.html
next: state
previous: tutorial
---

A maioria dos componentes podem ser customizados quando são criados, usando diferentes parâmetros. Estes parâmetros na criação são chamados de `props`.

Por exemplo, um componente básico no React Native é o `Image`. Quando você
cria uma imagem, você pode usar uma prop chamada `source` para controlar o que a imagem mostra.

```ReactNativeWebPlayer
import React, { Component } from 'react';
import { AppRegistry, Image } from 'react-native';

export default class Bananas extends Component {
  render() {
    let pic = {
      uri: 'https://upload.wikimedia.org/wikipedia/commons/d/de/Bananavarieties.jpg'
    };
    return (
      <Image source={pic} style={{width: 193, height: 110}}/>
    );
  }
}

// skip this line if using Create React Native App
AppRegistry.registerComponent('AwesomeProject', () => Bananas);
```

Note que `{pic}` é envolto por chaves para inserir a variável `pic` dentro do JSX. Você pode pôr qualquer expressão de JavaScript dentro de chaves no JSX.

Os seus próprios componentes podem também usar `props`. Isto permite-lhe criar um componente simples, que é então usado em muitos lugares diferentes no seu app, com propriedades ligeiramente diferentes em cada lugar. Apenas refira ao `this.props` na sua função `render`. Aqui está um exemplo:

```ReactNativeWebPlayer
import React, { Component } from 'react';
import { AppRegistry, Text, View } from 'react-native';

class Greeting extends Component {
  render() {
    return (
      <Text>Hello {this.props.name}!</Text>
    );
  }
}

export default class LotsOfGreetings extends Component {
  render() {
    return (
      <View style={{alignItems: 'center'}}>
        <Greeting name='Rexxar' />
        <Greeting name='Jaina' />
        <Greeting name='Valeera' />
      </View>
    );
  }
}

// skip this line if using Create React Native App
AppRegistry.registerComponent('AwesomeProject', () => LotsOfGreetings);
```

Usando `name` como uma prop permite-nos customizar o componente `Greeting`; daí podemos reutilizar esse componente para cada greeting nosso. Este exemplo usa também o componente `Greeting` no JSX como se fosse componentes embutidos. O poder de se fazer isto é o que faz do React tão massa - se você se achar desejando que tivesse uma seleção diferente de primitivos de UI com que trabalhar, você simplesmente inventa novos!

A outra novidade acontecendo aqui é o componente [`View`](docs/view.html). Um [`View`](docs/view.html) é útil
como um contêiner para outros componentes, para ajudar a controlar o estilo e o layout.

Com `props` e os componentes básicos [`Text`](docs/text.html), [`Image`](docs/image.html) e [`View`](docs/view.html), você pode
desenvolver uma ampla variedade de telas estáticas. Para aprender como fazer o seu app mudar com o tempo, você necessita [aprender sobre State](docs/state.html).
