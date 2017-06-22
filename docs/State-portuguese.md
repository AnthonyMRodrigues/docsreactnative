---
id: state
title: State
layout: docs
category: The Basics
permalink: docs/state.html
next: style
previous: props
---

Existem dois tipos de dados que controlam um componente: `props` e `state`. `props` são definidos pelo progenitor e mantêm-se fixos durante todo o tempo de existência dum componente. Para os dados que vão se modificar, temos que utilizar `state`.

Em geral, você deve inicializar o `state` no construtor, e então chamar `setState` quando quiser modificá-lo.

Por exemplo, digamos que desejemos criar textos que pisquem o tempo todo. O texto em si é configurado uma vez só quando o componente de piscagem for criado; portanto o texto é em si uma `prop`. O "se acaso o texto esteje no momento ligado ou desligado" modifica-se com o tempo; logo isso deve ser guardado em `state`.

```ReactNativeWebPlayer
import React, { Component } from 'react';
import { AppRegistry, Text, View } from 'react-native';

class Blink extends Component {
  constructor(props) {
    super(props);
    this.state = {showText: true};

    // Toggle the state every second
    setInterval(() => {
      this.setState(previousState => {
        return { showText: !previousState.showText };
      });
    }, 1000);
  }

  render() {
    let display = this.state.showText ? this.props.text : ' ';
    return (
      <Text>{display}</Text>
    );
  }
}

export default class BlinkApp extends Component {
  render() {
    return (
      <View>
        <Blink text='I love to blink' />
        <Blink text='Yes blinking is so great' />
        <Blink text='Why did they ever take this out of HTML' />
        <Blink text='Look at me look at me look at me' />
      </View>
    );
  }
}

// skip this line if using Create React Native App
AppRegistry.registerComponent('AwesomeProject', () => BlinkApp);
```

Num aplicativo de verdade, você provavelmente não estará a ajustar o estado com um temporizador. Você poderia ajustar o estado quando você tivesse novos dados chegando do servidor, ou de entradas do usuário. Você pode também utilizar um contêiner de estados tais como o [Redux](http://redux.js.org/index.html) para controlar o seu fluxo de dados. Nesse caso você utilizaria o Redux para modificar o seu estado no lugar de chamar o `setState` diretamente.

Quando o setState for chamado, BlinkApp re-renderizará o seu Component. Ao invocar setState de dentro do Timer, o componente re-renderizará toda vez que o Timer der tique-taque.

O estado funciona da mesma forma como acontece no React; então para mais detalhes em como lidar com o estado, você pode dar uma olhada no [API do React.Component](https://facebook.github.io/react/docs/component-api.html).
Nesta altura, você poderia estar chateado que a maioria dos nossos exemplos até agora utilizam monótonos textos pretos default. Para deixar as coisas mais bonitas, você terá que [aprender sobre Style](docs/style.html).
