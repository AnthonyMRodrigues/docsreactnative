---
id: using-a-scrollview
title: Using a ScrollView
layout: docs
category: The Basics
permalink: docs/using-a-scrollview.html
next: using-a-listview
previous: handling-touches
---

O [ScrollView](docs/scrollview.html) é um contêiner genérico para rolagem que pode hospedar múltiplos componentes e visualizadores. Os itens roláveis não precisam ser homogênios, e você pode rolar tanto verticalmente quanto horizontalmente (ao definir a propriedade `horizontal`).

Este exemplo cria um `ScrollView` vertical misturando imagens e textos juntos.

```ReactNativeWebPlayer
import React, { Component } from 'react';
import { AppRegistry, ScrollView, Image, Text } from 'react-native';

export default class IScrolledDownAndWhatHappenedNextShockedMe extends Component {
  render() {
      return (
        <ScrollView>
          <Text style={{fontSize:96}}>Scroll me plz</Text>
          <Image source={require('./img/favicon.png')} />
          <Image source={require('./img/favicon.png')} />
          <Image source={require('./img/favicon.png')} />
          <Image source={require('./img/favicon.png')} />
          <Image source={require('./img/favicon.png')} />
          <Text style={{fontSize:96}}>If you like</Text>
          <Image source={require('./img/favicon.png')} />
          <Image source={require('./img/favicon.png')} />
          <Image source={require('./img/favicon.png')} />
          <Image source={require('./img/favicon.png')} />
          <Image source={require('./img/favicon.png')} />
          <Text style={{fontSize:96}}>Scrolling down</Text>
          <Image source={require('./img/favicon.png')} />
          <Image source={require('./img/favicon.png')} />
          <Image source={require('./img/favicon.png')} />
          <Image source={require('./img/favicon.png')} />
          <Image source={require('./img/favicon.png')} />
          <Text style={{fontSize:96}}>What's the best</Text>
          <Image source={require('./img/favicon.png')} />
          <Image source={require('./img/favicon.png')} />
          <Image source={require('./img/favicon.png')} />
          <Image source={require('./img/favicon.png')} />
          <Image source={require('./img/favicon.png')} />
          <Text style={{fontSize:96}}>Framework around?</Text>
          <Image source={require('./img/favicon.png')} />
          <Image source={require('./img/favicon.png')} />
          <Image source={require('./img/favicon.png')} />
          <Image source={require('./img/favicon.png')} />
          <Image source={require('./img/favicon.png')} />
          <Text style={{fontSize:80}}>React Native</Text>
        </ScrollView>
    );
  }
}

// skip these lines if using Create React Native App
AppRegistry.registerComponent(
  'AwesomeProject',
  () => IScrolledDownAndWhatHappenedNextShockedMe);
```

ScrollViews podem ser configurados para permitir paginação através de visualizadores que usam gestos de deslizamento ao usarmos as propriedades `pagingEnabled`. Deslizar horizontalmente por entre visualizadores pode também ser implementado no Android usando o componente [ViewPagerAndroid](docs/viewpagerandroid.html).

Um ScrollView num item individual pode ser usado para permitir ao usuário dar zoom no conteúdo. Configure as propriedades `maximumZoomScale` e `minimumZoomScale` e o seu usuário será capaz de usar os gestos expandir e beliscar para aumentar e diminuir o zoom.

O ScrollView funciona melhor para apresentar uma quantidade pequena de coisas com tamanhos limitados. Todos os elementos e visualizadores de um `ScrollView` são renderizados, mesmo quando não estiverem sendo mostrados na tela. Se você tiver uma lista longa com mais itens que conseguem caber na tela, você deveria usar uma `FlatList` no lugar. Portanto vamos [aprender sobre visualizadores de listas](docs/using-a-listview.html) em seguida.
