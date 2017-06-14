---
id: using-a-listview
title: Using List Views
layout: docs
category: The Basics
permalink: docs/using-a-listview.html
next: network
previous: using-a-scrollview
---

O React Native fornece um conjunto de componentes para apresentação de listas de dados. Geralmente você vai querer usar ou a [FlatList](docs/flatlist.html) ou então a [SectionList](docs/sectionlist.html).

O componente `FlatList` exibe uma lista rolável de dados dinâmicos, mas similarmente estruturados. A `FlatList` funciona bem para as listas de dados longas, onde o número de itens pode mudar com o tempo. Diferente do mais genérico [`ScrollView`](docs/using-a-scrollview.html), a `FlatList` apenas processa os elementos que estão sendo mostrados na tela, não todos os elementos de uma vez.

O componente `FlatList` requer duas propriedades: `data` e `renderItem`. `data` é a fonte da informação para a lista. `renderItem` pega um item da fonte e retorna um componente formatado para renderizar.

Este exemplo cria uma `FlatList` simples com os dados já diretamente inseridos. Cada item nas propriedades de `data` é renderizado como um componente `Text`. O componente `FlatListBasics` então renderiza a `FlatList` e todos os componentes `Text`.

```SnackPlayer?name=FlatList%20Basics
import React, { Component } from 'react';
import { AppRegistry, FlatList, StyleSheet, Text, View } from 'react-native';

export default class FlatListBasics extends Component {
  render() {
    return (
      <View style={styles.container}>
        <FlatList
          data={[
            {key: 'Devin'},
            {key: 'Jackson'},
            {key: 'James'},
            {key: 'Joel'},
            {key: 'John'},
            {key: 'Jillian'},
            {key: 'Jimmy'},
            {key: 'Julie'},
          ]}
          renderItem={({item}) => <Text style={styles.item}>{item.key}</Text>}
        />
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
   flex: 1,
   paddingTop: 22
  },
  item: {
    padding: 10,
    fontSize: 18,
    height: 44,
  },
})

// skip this line if using Create React Native App
AppRegistry.registerComponent('AwesomeProject', () => FlatListBasics);
```

Se você quiser processar um conjunto de dados repartidos em seções lógicas, talvez com cabeçalhos das seções, similar ao `UITableView`s no iOS, então uma [SectionList](docs/sectionlist.html) é o caminho a seguir.

```SnackPlayer?name=SectionList%20Basics
import React, { Component } from 'react';
import { AppRegistry, SectionList, StyleSheet, Text, View } from 'react-native';

export default class SectionListBasics extends Component {
  render() {
    return (
      <View style={styles.container}>
        <SectionList
          sections={[
            {title: 'D', data: ['Devin']},
            {title: 'J', data: ['Jackson', 'James', 'Jillian', 'Jimmy', 'Joel', 'John', 'Julie']},
          ]}
          renderItem={({item}) => <Text style={styles.item}>{item}</Text>}
          renderSectionHeader={({section}) => <Text style={styles.sectionHeader}>{section.title}</Text>}
        />
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
   flex: 1,
   paddingTop: 22
  },
  sectionHeader: {
    paddingTop: 2,
    paddingLeft: 10,
    paddingRight: 10,
    paddingBottom: 2,
    fontSize: 14,
    fontWeight: 'bold',
    backgroundColor: 'rgba(247,247,247,1.0)',
  },
  item: {
    padding: 10,
    fontSize: 18,
    height: 44,
  },
})

// skip this line if using Create React Native App
AppRegistry.registerComponent('AwesomeProject', () => SectionListBasics);
```

Um dos usos mais comuns para um visualizador de listas é exibir os dados que você busca de um servidor. Para fazer isso, você precisará [aprender sobre trabalhos em rede (networking) no React Native](docs/network.html).
