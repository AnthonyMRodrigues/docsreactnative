

## Texto Aninhado

Tanto iOS quanto Android permitem a exibição de texto formatado anotando os intervalos de uma sequência com formatação específica, como um texto em negrito ou colorido (`NSAttributedString` no iOS,` SpannableString` no Android). Na prática, este trabalho é muito tedioso. Para o React Native, decidimos usar um paradigma web para isso, onde você pode aninhar texto para conseguir o mesmo efeito.

```ReactNativeWebPlayer
import React, { Component } from 'react';
import { AppRegistry, Text } from 'react-native';

export default class BoldAndBeautiful extends Component {
  render() {
    return (
      <Text style={{fontWeight: 'bold'}}>
        I am bold
        <Text style={{color: 'red'}}>
          and red
        </Text>
      </Text>
    );
  }
}

// pule esta linha se estiver usando Create React Native App
AppRegistry.registerComponent('AwesomeProject', () => BoldAndBeautiful);
```

Por detrás das cortinas, o React Native converte isto para `NSAttributedString` ou `SpannableString` que contém a seguinte informação:

```javascript
"I am bold and red"
0-9: bold
9-17: bold, red
```

## Views Aninhadas (apenas iOS)

No iOS, é possível aninhar views dentro do componente Text. Segue um exemplo:

```ReactNativeWebPlayer
import React, { Component } from 'react';
import { AppRegistry, Text, View } from 'react-native';

export default class BlueIsCool extends Component {
  render() {
    return (
      <Text>
        There is a blue square
        <View style={{width: 50, height: 50, backgroundColor: 'steelblue'}} />
        in between my text.
      </Text>
    );
  }
}

// pule esta linha se estiver usando Create React Native App
AppRegistry.registerComponent('AwesomeProject', () => BlueIsCool);
```

> Para usar esta feature, você deve indicar para a view um `width` e um `height`.

## Containers

O elemento `<Text>` tem um comportamento especial em relação ao layout: tudo o que está aninhado dele não está mais usando o layout flexbox, mas sim o layout de texto. Isso significa que os elementos dentro de um ` <Text> `não são mais retângulos, e quebram quando vêem o final da linha.

```javascript
<Text>
  <Text>First part and </Text>
  <Text>second part</Text>
</Text>
// Text container: todo o texto segue como se fosse único
// |First part |
// |and second |
// |part       |

<View>
  <Text>First part and </Text>
  <Text>second part</Text>
</View>
// View container: cada texto é um bloco único
// |First part |
// |and        |
// |second part|
```

## Herança de Estilo Limitada

Em desenvolvimento Web, a maneira usual de definir família e tamanho de fonte para todo o documento é tirar proveito das propriedades CSS herdadas, como:

```css
/* CSS, *not* React Native */
html {
  font-family: 'lucida grande', tahoma, verdana, arial, sans-serif;
  font-size: 11px;
  color: #141823;
}
```

Todos os elementos no documento herdam esta fonte a não ser que eles ou um elemento pai especifiquem novas regras.

No React Native, somos mais rigorosos quanto a isso: ** você deve agrupar todos os nós de texto dentro de um componente `<Text>` **; você não pode ter um nó de texto diretamente aninhado dentro de um `<View>`.

```javascript
// RUIM: vai gerar uma exception, não é permitido texto dentro de uma <View>
<View>
  Some text
</View>

// BOM
<View>
  <Text>
    Some text
  </Text>
</View>
```

Você também perde a capacidade de configurar uma fonte padrão para uma subárvore inteira. A maneira recomendada de usar fontes e tamanhos consistentes em seu aplicativo é criar um componente `MyAppText` que os inclua e usar esse componente em seu aplicativo. Você também pode usar esse componente para criar componentes mais específicos, como `MyAppHeaderText`, para outros tipos de texto.

```javascript
<View>
  <MyAppText>Texto estilizado com a fonte padrão para toda a aplicação</MyAppText>
  <MyAppHeaderText>Texto estilizado como um header</MyAppHeaderText>
</View>
```

Supondo que `MyAppText` é um componente que simplesmente transforma seus filhos em um componente `Text` com estilo, então `MyAppHeaderText` pode ser definido da seguinte forma:

```javascript
class MyAppHeaderText extends Component {
  render() {
    <MyAppText>
      <Text style={{fontSize: 20}}>
        {this.props.children}
      </Text>
    </MyAppText>
  }
}
```

A composição de `MyAppText` dessa maneira garante que tenhamos os estilos de um componente de nível superior, mas nos deixa a capacidade de adicioná-los / substituí-los em casos de uso específicos.

O React Native ainda tem o conceito de herança de estilo, mas limitado a subárvores de texto. Nesse caso, a segunda parte será em negrito e vermelho.

```javascript
<Text style={{fontWeight: 'bold'}}>
  I am bold
  <Text style={{color: 'red'}}>
    and red
  </Text>
</Text>
```

Acreditamos que essa maneira mais restrita de estilizar o texto produzirá aplicativos melhores:

- (Desenvolvedor) Os componentes do React são projetados com forte isolamento em mente: você deve poder inserir um componente em qualquer lugar do seu aplicativo, confiando que, desde que os acessórios sejam os mesmos, eles terão a mesma aparência e comportamento. As propriedades de texto que poderiam ser herdadas de fora dos elementos pai quebrariam esse isolamento.

- (Implementador) A implementação do React Native também é simplificada. Não precisamos ter um campo `fontFamily` em cada elemento, e não precisamos percorrer a árvore até a raiz toda vez que exibirmos um nó de texto. A herança de estilo é codificada apenas dentro do componente de texto nativo e não vaza para outros componentes ou para o próprio sistema.
