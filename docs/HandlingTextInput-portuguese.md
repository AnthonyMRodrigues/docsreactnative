---
id: handling-text-input
title: Handling Text Input
layout: docs
category: The Basics
permalink: docs/handling-text-input.html
next: handling-touches
previous: flexbox
---

O [`TextInput`](docs/textinput.html#content) é um componente básico que permite ao usuário entrar com textos. Ele tem uma prop `onChangeText` que aceita uma função a ser chamada toda vez que o texto mudar, e uma prop `onSubmitEditing` que aceita uma função a ser chamada quando o texto for submetido.

Por exemplo, digamos que à medida que o usuário digita, você esteja traduzindo suas palavras em uma língua diferente. Neste novo idioma, cada palavra individual é escrita da mesma maneira: 🍕. Portanto a sentença "Hello there Bob" seria traduzida como "🍕🍕🍕".

```ReactNativeWebPlayer
import React, { Component } from 'react';
import { AppRegistry, Text, TextInput, View } from 'react-native';

export default class PizzaTranslator extends Component {
  constructor(props) {
    super(props);
    this.state = {text: ''};
  }

  render() {
    return (
      <View style={{padding: 10}}>
        <TextInput
          style={{height: 40}}
          placeholder="Type here to translate!"
          onChangeText={text => this.setState({text})}
        />
        <Text style={{padding: 10, fontSize: 42}}>
          {this.state.text.split(' ').map(word => word && '🍕').join(' ')}
        </Text>
      </View>
    );
  }
}

// skip this line if using Create React Native App
AppRegistry.registerComponent('AwesomeProject', () => PizzaTranslator);
```

Neste exemplo, armazenamos o `text` no `state`, porque ele muda com o tempo.

Tem muito mais coisas que você poderia querer fazer com um input de texto. Por exemplo, você poderia validar o texto dentro enquanto o usuário digita. Para mais exemplos detalhados, visite os [docs de React sobre componentes controlados](https://facebook.github.io/react/docs/forms.html), ou os [docs de referência para TextInput](docs/textinput.html).

Entrada de textos é provavelmente o exemplo mais simples dum componente cujo estado muda naturalmente com o tempo. A seguir, vamos dar uma olhada em um outro tipo de componente assim como este que controla o layout, e [aprender sobre o ScrollView](docs/using-a-scrollview.html).
