---
id: animations
title: Animations
layout: docs
category: Guides
permalink: docs/animations.html
next: accessibility
previous: images
---

As animações são muito importantes para criar uma excelente experiência de usuário.Objetos estacionários devem superar a inércia à medida que começam a se mover. Os objetos em movimento têm impulso e raramente aparecem imediatamente. As animações permitem que você transmita um movimento fisicamente suscetível na sua interface.

O React Native fornece dois sistemas de animação complementares:
[`Animated`](docs/animations.html#animated-api) fpara controle granular e interativo de valores específicos, e
[`LayoutAnimation`](docs/animations.html#layoutanimation) para transações de layout global animado.

## `Animated` API

A API [`Animated`](docs/animated.html) foi projetada para tornar muito fácil expressar sucintamente uma ampla variedade de padrões de animação e interação interessantes de uma forma muito performante.
`Animated` concentra-se em relações declarativas entre entradas e saídas, com transformações configuráveis ​​no meio e métodos simples de 'start` /` stop` para controlar a execução de animação baseada em tempo.

`Animated` exporta quatro tipos de componentes animáveis:` View`, `Text`,` Image` e `ScrollView`, mas você também pode criar o seu próprio 'Animated.createAnimatedComponent ()`.

Por exemplo, uma exibição de contêiner que desaparece quando está montada pode parecer assim:

```SnackPlayer
import React from 'react';
import { Animated, Text, View } from 'react-native';

class FadeInView extends React.Component {
  state = {
    fadeAnim: new Animated.Value(0),  // Initial value for opacity: 0
  }

  componentDidMount() {
    Animated.timing(                  // Animate over time
      this.state.fadeAnim,            // The animated value to drive
      {
        toValue: 1,                   // Animate to opacity: 1 (opaque)
        duration: 10000,              // Make it take a while
      }
    ).start();                        // Starts the animation
  }

  render() {
    let { fadeAnim } = this.state;

    return (
      <Animated.View                 // Special animatable View
        style={{
          ...this.props.style,
          opacity: fadeAnim,         // Bind opacity to animated value
        }}
      >
        {this.props.children}
      </Animated.View>
    );
  }
}

// Você pode então usar o `FadeInView` no lugar de um` View` em seus componentes:
export default class App extends React.Component {
  render() {
    return (
      <View style={{flex: 1, alignItems: 'center', justifyContent: 'center'}}>
        <FadeInView style={{width: 250, height: 50, backgroundColor: 'powderblue'}}>
          <Text style={{fontSize: 28, textAlign: 'center', margin: 10}}>Fading in</Text>
        </FadeInView>
      </View>
    )
  }
}
```

Vamos dividir o que está acontecendo aqui.
No construtor 'FadeInView`, um novo `Animated.Value` chamado` fadeAnim` é inicializado como parte do `state'. A propriedade de opacidade no `View` é mapeada para este valor animado. Por trás das cenas, o valor numérico é extraído e usado para definir a opacidade.

Quando o componente é montado, a opacidade é definida como 0. Então, uma animação facilitadora é iniciada no valor animado `fadeAnim`, que atualizará todos os seus mapeamentos dependentes (neste caso, apenas a opacidade) em cada quadro, pois o valor anima o valor final de 1.

Isso é feito de forma otimizada que é mais rápida do que chamar `setState` e re-rendering.  
Como toda a configuração é declarativa, poderemos implementar otimizações futuras que serializam a configuração e executam a animação em um segmento de alta prioridade.

### Configurando animações

As animações são fortemente configuráveis. Funções de flexibilidade personalizadas e predefinidas, atrasos, durações, fatores de decaimento, constantes de primavera e muito mais podem ser ajustados de acordo com o tipo de animação.

Animated` fornece vários tipos de animação, sendo o mais comum usado [` Animated.timing () `] (docs / animated.html # timing).
Ele suporta a animação de um valor ao longo do tempo usando uma das várias funções de flexibilidade predefinidas, ou você pode usar o seu próprio.
As funções de facilitação são tipicamente usadas em animações para transmitir aceleração e desaceleração gradual de objetos.

Por padrão, `timing` usará uma curva easeInOut que transmite aceleração gradual para a velocidade máxima e conclui gradualmente a desacelerar até uma parada.
Você pode especificar uma função de flexibilidade diferente passando um parâmetro de "facilitação".
A "duração" ou mesmo o "atraso" antes da iniciação da animação também são suportados.

Por exemplo, se quisermos criar uma animação longa de 2 segundos de um objeto que faz uma cópia de segurança leve antes de passar para a posição final:

```javascript
Animated.timing(
  this.state.xPosition,
  {
    toValue: 100,
    easing: Easing.back,
    duration: 2000,
  }                              
).start();  
```

Dê uma olhada na seção  [Configuring animations](docs/animated.html#configuring-animations) da referência da API `Animated` para saber mais sobre todos os parâmetros de configuração suportados pelas animações internas.

### Composição de animações

As animações podem ser combinadas e jogadas em seqüência ou em paralelo.
As animações seqüenciais podem ser reproduzidas imediatamente após a animação anterior terminar,
ou podem começar após uma demora especificada.
A API `Animated` fornece vários métodos, como` sequence () `e` delay () `,
cada um dos quais simplesmente leva uma série de animações para executar e chama automaticamente `start ()` / `stop ()` conforme necessário.

Por exemplo, a seguinte animação pára, depois volta a girar em paralelo:

```javascript
Animated.sequence([            // decay, then spring to start and twirl
  Animated.decay(position, {   // coast to a stop
    velocity: {x: gestureState.vx, y: gestureState.vy}, // velocity from gesture release
    deceleration: 0.997,
  }),
  Animated.parallel([          // after decay, in parallel:
    Animated.spring(position, {
      toValue: {x: 0, y: 0}    // return to start
    }),
    Animated.timing(twirl, {   // and twirl
      toValue: 360,
    }),
  ]),
]).start();                    // start the sequence group
```

Se uma animação for interrompida ou interrompida, todas as outras animações do grupo também serão interrompidas. `Animated.parallel` tem uma opção` stopTogether` que pode ser configurada para `false` para desativá-la.

Você pode encontrar uma lista completa de métodos de composição na seção [Composing animations](docs/animated.html#composing-animations) da referência da API `Animated`.

### Combinando valores animados

Você pode [combinar dois valores animados](docs/animated.html#combining-animated-values) por meio de adição, multiplicação, divisão ou módulo para criar um novo valor animado.

Existem alguns casos em que um valor animado precisa inverter outro valor animado para cálculo.
Um exemplo é inverter uma escala (2x --> 0.5x):

```javascript
const a = Animated.Value(1);
const b = Animated.divide(1, a);

Animated.spring(a, {
  toValue: 2,
}).start();
```

### Interpolação

Cada propriedade pode ser executada através de uma interpolação primeiro.
Uma interpolação mapeia intervalos de entrada para intervalos de saída,
normalmente usando uma interpolação linear, mas também suporta funções de flexibilização.
Por padrão, irá extrapolar a curva para além dos intervalos fornecidos, mas você também pode fazer com que ele coloque o valor de saída.

Um mapeamento simples para converter um intervalo 0-1 para um intervalo 0-100 seria:

```javascript
value.interpolate({
  inputRange: [0, 1],
  outputRange: [0, 100],
});
```

Por exemplo, você pode querer pensar sobre o `Animated.Value` como indo de 0 a 1,
mas anima a posição de 150px para 0px e a opacidade de 0 para 1.
Isso pode ser feito facilmente modificando `style` do exemplo acima, assim:

```javascript
  style={{
    opacity: this.state.fadeAnim, // Binds directly
    transform: [{
      translateY: this.state.fadeAnim.interpolate({
        inputRange: [0, 1],
        outputRange: [150, 0]  // 0 : 150, 0.5 : 75, 1 : 0
      }),
    }],
  }}
```

[`interpolate()`](docs/animated.html#interpolate) também suporta vários segmentos de alcance, o que é útil para definir zonas mortas e outros truques úteis.
Por exemplo, para obter uma relação de negação em -300 que vai para 0 em -100, então volte para 1 em 0 e, em seguida, volte para zero em 100, seguido de uma zona morta que permanece em 0 para tudo além disso, você poderia fazer:

```javascript
value.interpolate({
  inputRange: [-300, -100, 0, 100, 101],
  outputRange: [300,    0, 1,   0,   0],
});
```

Que seria o seguinte:

```
Input | Output
------|-------
  -400|    450
  -300|    300
  -200|    150
  -100|      0
   -50|    0.5
     0|      1
    50|    0.5
   100|      0
   101|      0
   200|      0
```

`interpolate()` também suporta mapeamento em strings, permitindo que você anime cores e valores com unidades. Por exemplo, se você quisesse animar uma rotação, você poderia fazer:

```javascript
value.interpolate({
  inputRange: [0, 360],
  outputRange: ['0deg', '360deg']
})
```

`interpolate()` também suporta funções arbitrárias de flexibilização, muitas das quais já estão implementadas no modulon[`Easing`](docs/easing.html) .
`interpolate()` Também possui um comportamento configurável para extrapolar o `outputRange`.
Você pode definir a extrapolação definindo as opções `extrapolar`,` extrapolarLeft` ou `extrapolarRight‖.
O valor padrão é `extend', mas você pode usar` clamp` para evitar que o valor de saída exceda `outputRange`.

### Rastreamento de valores dinâmicos

Os valores animados também podem acompanhar outros valores.
Basta configurar o `toValue` de uma animação para outro valor animado em vez de um número simples.
Por exemplo, uma animação "Chat Heads" como a usada pelo Messenger no Android poderia ser implementada com um `spring ()` fixado em outro valor animado, ou com `timing ()` e uma 'duração' de 0 para rastreamento rígido .
Eles também podem ser compostos com interpolações:

```javascript
Animated.spring(follower, {toValue: leader}).start();
Animated.timing(opacity, {
  toValue: pan.x.interpolate({
    inputRange: [0, 300],
    outputRange: [1, 0],
  }),
}).start();
```

Os valores animados `leader` e `follower' serão implementados usando `Animated.ValueXY ()`.
`ValueXY` é uma maneira útil de lidar com interações 2D, como panning ou arrastar.
É um invólucro simples que basicamente contém duas instâncias `Animated.Value` e algumas funções auxiliares que o chamam,
fazendo com que "ValueXY" seja uma substituição drop-in para `Value` em muitos casos.
Ele nos permite rastrear os valores x e y no exemplo acima.

### Gestos de rastreamento

Os gestos, como panning ou rolagem, e outros eventos podem ser mapeados diretamente para valores animados usando [`Animated.event`](docs/animated.html#event).
Isso é feito com uma sintaxe de mapa estruturado para que os valores possam ser extraídos de objetos de eventos complexos.
O primeiro nível é uma matriz para permitir o mapeamento em vários args, e essa matriz contém objetos aninhados.

Por exemplo, ao trabalhar com gestos de rolagem horizontal,
você faria o seguinte para mapear `event.nativeEvent.contentOffset.x` para` scrollX` (um `Animated.Value`):

```javascript
 onScroll={Animated.event(
   // scrollX = e.nativeEvent.contentOffset.x
   [{ nativeEvent: {
        contentOffset: {
          x: scrollX
        }
      }
    }]
 )}
```

Ao usar `PanResponder`, você pode usar o seguinte código para extrair as posições x e y de` gestureState.dx` e `gestureState.dy`.
Usamos um `null` na primeira posição da matriz, pois só estamos interessados ​​no segundo argumento passado ao manipulador` PanResponder`,
qual é o 'gestureState`.

```javascript
onPanResponderMove={Animated.event(
  [null, // ignore the native event
  // extract dx and dy from gestureState
  // like 'pan.x = gestureState.dx, pan.y = gestureState.dy'
  {dx: pan.x, dy: pan.y}
])}
```

### Respondendo ao valor atual da animação

Você pode notar que não existe uma maneira óbvia de ler o valor atual durante a animação.
Isso ocorre porque o valor só pode ser conhecido no tempo de execução nativo devido a otimizações.
Se você precisa executar o JavaScript em resposta ao valor atual, há duas abordagens:

- `spring.stopAnimation(callback)` irá parar a animação e invocar `callback` com o valor final. Isso é útil ao fazer transições gestuais.
- `spring.addListener(callback)`invocará `callback 'de forma assíncrona enquanto a animação estiver sendo executada, fornecendo um valor recente.
  Isso é útil para desencadear mudanças de estado,
  por exemplo, estalando um bobble para uma nova opção à medida que o usuário aproxima-lo,
  porque essas mudanças de estado maiores são menos sensíveis a alguns quadros de atraso em comparação com gestos contínuos, como panning, que precisam ser executados em 60 fps.

`Animated` é projetado para ser completamente serializável para que as animações possam ser executadas de forma altamente eficiente, independentemente do loop de eventos JavaScript normal.
Isso influencia a API, então tenha isso em mente quando parece um pouco mais complicado fazer algo em comparação com um sistema totalmente síncrono.
Confira `Animated.Value.addListener` como uma maneira de contornar algumas dessas limitações,
mas use isso com moderação, pois pode ter implicações no desempenho no futuro.

### Usando o driver nativo

A API `Animated` foi projetada para ser serializável.
Ao usar o [native driver](http://facebook.github.io/react-native/blog/2017/02/14/using-native-driver-for-animated.html),nós enviamos tudo sobre a animação para nativo antes de iniciar a animação,permitindo que o código nativo execute a animação no segmento UI sem ter que passar pela ponte em cada quadro.Uma vez iniciada a animação, o segmento JS pode ser bloqueado sem afetar a animação.

Usar o driver nativo para animações normais é bastante simples.
Adicione apenas `useNativeDriver: true` à configuração de animação ao iniciá-lo.

```javascript
Animated.timing(this.state.animatedValue, {
  toValue: 1,
  duration: 500,
  useNativeDriver: true, // <-- Add this
}).start();
```

Os valores animados apenas são compatíveis com um driver, portanto, se você usar o driver nativo ao iniciar uma animação em um valor,
Verifique se todas as animações desse valor também usam o driver nativo.

O driver nativo também funciona com `Animated.event`.
Isto é especialmente útil para animações que seguem a posição de rolagem como sem o driver nativo,
A animação sempre executará um quadro atrás do gesto devido à natureza assíncrona do React Native.

```javascript
<Animated.ScrollView // <-- Use the Animated ScrollView wrapper
  scrollEventThrottle={1} // <-- Use 1 here to make sure no events are ever missed
  onScroll={Animated.event(
    [{ nativeEvent: { contentOffset: { y: this.state.animatedValue } } }],
    { useNativeDriver: true } // <-- Add this
  )}
>
  {content}
</Animated.ScrollView>
```

Você pode ver o driver nativo em ação executando o [RNTester app](https://github.com/facebook/react-native/blob/master/RNTester/),
depois carregando o Exemplo Animado Nativo.
Você também pode dar uma olhada no [source code](https://github.com/facebook/react-native/blob/master/RNTester/js/NativeAnimationsExample.js) para saber como esses exemplos foram produzidos.

#### Ressalvas

Nem tudo o que você pode fazer com `Animated` é atualmente suportado pelo driver nativo.
A principal limitação é que você só pode animar propriedades não relacionadas ao layout:
coisas como 'transformação' e 'opacidade' funcionam, mas as propriedades da pasta flexível e da posição não serão.
Ao usar `Animated.event`, ele só funcionará com eventos diretos e eventos não borbulhantes.
Isso significa que ele não funciona com `PanResponder`, mas funciona com coisas como` ScrollView # onScroll`.

### Exemplos adicionais

O aplicativo RNTester tem vários exemplos de 'Animated` em uso:

- [AnimatedGratuitousApp](https://github.com/facebook/react-native/tree/master/RNTester/js/AnimatedGratuitousApp)
- [NativeAnimationsExample](https://github.com/facebook/react-native/blob/master/RNTester/js/NativeAnimationsExample.js)

## `LayoutAnimation` API

`LayoutAnimation` permite configurar globalmente `create` e` update` das animações que serão usadas para todas as visualizações no próximo ciclo de renderização / layout.
Isso é útil para fazer atualizações de layout do Flexbox sem se preocupar em medir ou calcular propriedades específicas para animá-las diretamente e é especialmente útil quando mudanças no layout podem afetar antepassados, por exemplo, um "ver mais "expansão que também aumenta o tamanho do pai e empurra para baixo o linha abaixo, que, de outro modo, exigiria uma coordenação explícita entre o
componentes para animá-los todos em sincronia.

Observe que, embora o `LayoutAnimation` seja muito poderoso e possa ser bastante útil,
fornece muito menos controle do que Animated e outras bibliotecas de animação, então
você pode precisar usar outra abordagem se você não conseguir fazer o que você quer com "LayoutAnimation" .

Note que, para que isso funcione no ** Android ** você precisa definir as seguintes bandeiras através do `UIManager`:

```javascript
UIManager.setLayoutAnimationEnabledExperimental && UIManager.setLayoutAnimationEnabledExperimental(true);
```

```SnackPlayer
import React from 'react';
import {
  NativeModules,
  LayoutAnimation,
  Text,
  TouchableOpacity,
  StyleSheet,
  View,
} from 'react-native';

const { UIManager } = NativeModules;

UIManager.setLayoutAnimationEnabledExperimental &&
  UIManager.setLayoutAnimationEnabledExperimental(true);

export default class App extends React.Component {
  state = {
    w: 100,
    h: 100,
  };

  _onPress = () => {
    // Animate the update
    LayoutAnimation.spring();
    this.setState({w: this.state.w + 15, h: this.state.h + 15})
  }

  render() {
    return (
      <View style={styles.container}>
        <View style={[styles.box, {width: this.state.w, height: this.state.h}]} />
        <TouchableOpacity onPress={this._onPress}>
          <View style={styles.button}>
            <Text style={styles.buttonText}>Press me!</Text>
          </View>
        </TouchableOpacity>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: 'center',
    justifyContent: 'center',
  },
  box: {
    width: 200,
    height: 200,
    backgroundColor: 'red',
  },
  button: {
    backgroundColor: 'black',
    paddingHorizontal: 20,
    paddingVertical: 15,
    marginTop: 15,
  },
  buttonText: {
    color: '#fff',
    fontWeight: 'bold',
  },
});
```

Este exemplo usa um valor predefinido, você pode personalizar as animações como
você precisa, veja [LayoutAnimation.js](https://github.com/facebook/react-native/blob/master/Libraries/LayoutAnimation/LayoutAnimation.js)
para mais informações.

## Notas Adicionais

### `requestAnimationFrame`

`requestAnimationFrame` é um polyfill do navegador que você pode ser
familiar com. Ele aceita uma função como único argumento e chama isso
Funcione antes do próximo repintado. É um bloco de construção essencial para
animações subjacentes a todas as APIs de animação baseadas em JavaScript. Dentro
geral, você não precisa chamar isso sozinho - as APIs de animação irão
gerenciar atualizações de quadros para você.

### `setNativeProps`

Como mencionado [na seção de Manipulação de Direção](docs/direct-manipulation.html),
`setNativeProps` nos permite modificar propriedades de recursos originais
componentes (componentes que são realmente suportados por visualizações nativas, ao contrário
componentes compostos) diretamente, sem ter que 'setState` e
re-renderizar a hierarquia de componentes.

Poderíamos usar isso no exemplo Rebound para atualizar a escala - isso
pode ser útil se o componente que estamos atualizando estiver profundamente aninhado
e não foi otimizado com `shouldComponentUpdate`.

Se você encontrar suas animações lançando quadros (executando abaixo de 60 quadros
por segundo), procure usar `setNativeProps` ou` shouldComponentUpdate` para
otimize-os. Ou você poderia executar as animações no segmento UI em vez de
o segmento de JavaScript [com a opcao useNativeDriver](http://facebook.github.io/react-native/blog/2017/02/14/using-native-driver-for-animated.html).
Você também pode querer adiar qualquer trabalho computacional intensivo até depois
animações estão completas, usando o [InteractionManager](docs/interactionmanager.html). 
Você pode monitorar a taxa de quadros usando a ferramenta "FPS Monitor" do menu Desenvolvedor no aplicativo.
