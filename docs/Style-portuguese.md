---
id: style
title: Style
layout: docs
category: The Basics
permalink: docs/style.html
next: height-and-width
previous: state
---

Com o React Native, você não usa nenhuma linguagem ou sintaxe especiais para definir estilos. Você simplesmente estiliza as suas aplicações usando o JavaScript. Todos os componentes-base aceitam uma prop chamada `style`. Os nomes e [valores](docs/colors.html) de estilo normalmente coincidem com o funcionamento do CSS na web, com a exceção de que os nomes são escritos usando minúscula/maiúscula em camelo; e.g. `backgroundColor` ao invés de `background-color`.

A prop de `style` pode ser um objeto de JavaScript comum de sempre. Esse é o mais simples e o que nós geralmente utilizamos como código dos exemplos. Você pode igualmente passar um array de estilos - o último estilo no array tem precedência, então você pode utilizar isto para herdar estilos.

À medida em que um componente cresce em complexidade, freqüentemente é mais limpo utilizar `StyleSheet.create` para definir vários estilos em um só lugar. Aqui está um exemplo:

```ReactNativeWebPlayer
import React, { Component } from 'react';
import { AppRegistry, StyleSheet, Text, View } from 'react-native';

export default class LotsOfStyles extends Component {
  render() {
    return (
      <View>
        <Text style={styles.red}>just red</Text>
        <Text style={styles.bigblue}>just bigblue</Text>
        <Text style={[styles.bigblue, styles.red]}>bigblue, then red</Text>
        <Text style={[styles.red, styles.bigblue]}>red, then bigblue</Text>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  bigblue: {
    color: 'blue',
    fontWeight: 'bold',
    fontSize: 30,
  },
  red: {
    color: 'red',
  },
});

// skip this line if using Create React Native App
AppRegistry.registerComponent('AwesomeProject', () => LotsOfStyles);
```

Um padrão bem comum é fazer com que o seu componente aceite uma prop de `style`, que por sua vez é usada para estilizar os subcomponentes. Você pode utilizar isto para fazer os estilos "descerem em cascata" do mesmo jeito que eles ocorrem no CSS.

Há ainda muito mais maneiras para se customizar estilos de texto. Confira a [Referência para Componentes de Texto](docs/text.html) para uma lista completa.

Agora você pode fazer que o seu texto fique bonito. O próximo passo em se tornar um mestre dos estilos é [aprender como controlar o tamanho dos componentes](docs/height-and-width.html).
