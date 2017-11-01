---
id: accessibility
title: Accessibility
layout: docs
category: Guides
permalink: docs/accessibility.html
next: timers
previous: animations
---

## Acessibilidade nos Aplicativos Nativos (iOS e Android)
Tanto o iOS como o Android oferecem APIs para tornar os aplicativos acessíveis para pessoas com deficiências. Além disso, ambas as plataformas fornecem tecnologias assistidas integradas, como os leitores de tela VoiceOver (iOS) e TalkBack (Android) para deficientes visuais. De modo similar, no React Native incluímos APIs projetados para fornecer aos desenvolvedores suporte para tornar os aplicativos mais acessíveis. Observe porém, que o iOS e o Android diferem ligeiramente em suas abordagens, e portanto, as implementações do React Native podem variar de acordo com a plataforma.

Além desta documentação, você pode achar [esta postagem de blog](https://code.facebook.com/posts/435862739941212/making-react-native-apps-accessible/) sobre acessibilidade em React Native seja útil.

## Tornando os Aplicativos Acessíveis

### Propriedades de Acessibilidade

#### accessible (iOS, Android)

Quando `true`, indica que a view é um elemento de acessibilidade. Quando uma view for um elemento de acessibilidade, ela agrupa os seus filhos em um único componente selecionável. Por padrão, todos os elementos tocáveis são acessíveis.

No Android, a propriedade ‘acessible={true}’ para uma View react-native será traduzida em ‘focusable={true}’ nativo.

```javascript
<View accessible={true}>
  <Text>texto um</Text>
  <Text>texto dois</Text>
</View>
```

No exemplo acima, não podemos obter o foco de acessibilidade separadamente em 'texto um' e 'texto dois'. Em vez disso obtemos foco numa view pai com a propriedade 'accessible'.



#### accessibilityLabel (iOS, Android)

Quando uma view é marcada como acessível, é uma boa prática definir uma accessibilityLabel na view, para que as pessoas que usarem o VoiceOver saibam qual o elemento que selecionaram. O VoiceOver lerá esta string quando um usuário selecionar o elemento associado.

Para usar, defina a propriedade `accessibilityLabel` com uma string personalizada na sua View:

```javascript
<TouchableOpacity accessible={true} accessibilityLabel={'Tap me!'} onPress={this._onPress}>
  <View style={styles.button}>
    <Text style={styles.buttonText}>Press me!</Text>
  </View>
</TouchableOpacity>
```

No exemplo acima, o `accessibilityLabel` no elemento TouchableOpacity predefiniria-se em "Press me!". O rótulo é construído pela concatenação de todos os filhos de nó de Text separados por espaços.

#### accessibilityTraits (iOS)

Os traços de acessibilidade indicam a uma pessoa usando o VoiceOver que tipo de elemento que selecionaram. Esse elemento é um rótulo? Um botão? Um cabeçalho? Essas questões são respondidas por `accessTraits`.

Para usar, defina a propriedade `accessibilityTraits` com uma das (ou um array de) strings de traços de acessibilidade:

* **none** Usado quando o elemento não possui traços.
* **button** Usado quando o elemento deve ser tratado como um botão.
* **link** Usado quando o elemento deve ser tratado como um link.
* **header** Usado quando um elemento age como um cabeçalho para uma seção de conteúdos (por exemplo, o título de uma barra de navigação).
* **search** Usado quando o elemento do campo de texto também deve ser tratado como um campo de pesquisa.
* **image** Usado quando o elemento deve ser tratado como uma imagem. Pode ser combinado com um botão ou link, por exemplo.
* **selected**  Usado quando o elemento é selecionado. Por exemplo, uma linha selecionada em uma tabela ou um botão selecionado dentro de um controle segmentado.
* **plays** Usado quando o elemento reproduz seu próprio som quando ativado.
* **key** Usado quando o elemento atua como uma tecla de teclado.
* **text** Usado quando o elemento deve ser tratado como texto estático que não pode ser alterado.
* **summary** Usado quando um elemento pode ser usado para fornecer um resumo rápido das condições atuais no aplicativo quando o aplicativo é iniciado pela primeira vez. Por exemplo, quando o Tempo inicia pela 1ª vez, o elemento com as condições climáticas de hoje é marcado com este traço.
* **disabled** Usado quando o controle não está ativado e não responde à entrada do usuário.
* **frequentUpdates** Usado quando o elemento atualiza freqüentemente seu rótulo ou valor, mas demasiado demais para se enviar notificações. Permite que um cliente de acessibilidade repetidamente verifique por alterações. Um cronômetro seria um exemplo.
* **startsMedia** Usado quando a ativação de um elemento inicia uma sessão de mídia (por exemplo, reproduzindo um filme, gravando áudio) que não devem ser interrompidos pela saída de uma tecnologia assistiva, como o VoiceOver.
* **adjustable** Usado quando um elemento pode ser "ajustado" (por exemplo, um controle deslizante).
* **allowsDirectInteraction** Usado quando um elemento permite interação direta aos toques para usuários do VoiceOver (por exemplo, uma view que representa um teclado de piano).
* **pageTurn** Informa ao VoiceOver que ele deve rolar para a próxima página quando terminar de ler o conteúdo do elemento.

#### accessibilityViewIsModal (iOS)

Um valor booleano que indica se o VoiceOver deve ignorar os elementos dentro das views que são irmãs da receptora.

Por exemplo, em uma janela que contém views irmãs `A` e `B`, definir `accessibilityViewIsModal` para `true` na view `B` faz com que o VoiceOver ignore os elementos na view `A`.
Por outro lado, se a view `B` contiver uma view filha `C` e você definir `accessibilityViewIsModal` para `true` na view `C`, o VoiceOver não ignora os elementos na view `A`

#### onAccessibilityTap (iOS)

Use esta propriedade para atribuir uma função personalizada a ser chamada quando alguém ativar um elemento acessível, tocando duas vezes, enquanto estiver selecionado.

#### onMagicTap (iOS)

Atribua esta propriedade a uma função personalizada que será chamada quando alguém executar o gesto de "toque mágico", que é um toque duplo com dois dedos. Uma função de toque mágico deve executar a ação mais relevante que um usuário pode tomar em um componente. No aplicativo Telefone no iPhone, uma batida mágica responde a uma chamada telefônica, ou termina a atual. Se o elemento selecionado não tiver uma função `onMagicTap`, o sistema irá percorrer a hierarquia de views até encontrar uma view que tiver.

#### accessibilityComponentType (Android)

Em alguns casos, também queremos alertar o usuário final do tipo de componente selecionado (isto é, que é um "botão"). Se estivéssemos usando botões nativos, isto funcionaria automaticamente. Como estamos usando o JavaScript, precisamos prover um pouco mais de contexto para o TalkBack. Para fazer isto, você deve especificar a propriedade 'accessibilityComponentType' para qualquer componente de UI. Como exemplos, temos suporte a 'button', 'radiobutton_checked' e 'radiobutton_unchecked' e assim por diante.

```javascript
<TouchableWithoutFeedback accessibilityComponentType='button' onPress={this._onPress}>
  <View style={styles.button}>
    <Text style={styles.buttonText}>Press me!</Text>
  </View>
</TouchableWithoutFeedback>
```

No exemplo acima, o TouchableWithoutFeedback está sendo anunciado pelo TalkBack como um Button nativo.

#### accessibilityLiveRegion (Android)

Quando os componentes mudam dinamicamente, queremos que o TalkBack alerte o usuário final. Isso é possível pela propriedade 'accessibilityLiveRegion'. Ela pode ser definida com 'none', 'polite' e 'assertive':

* **none** Os serviços de acessibilidade não devem anunciar alterações nesta view.
* **polite** Os serviços de acessibilidade devem anunciar mudanças nesta view.
* **assertive** Os serviços de acessibilidade devem interromper a fala em andamento para anunciar imediatamente mudanças nesta view.

```javascript
<TouchableWithoutFeedback onPress={this._addOne}>
  <View style={styles.embedded}>
    <Text>Click me</Text>
  </View>
</TouchableWithoutFeedback>
<Text accessibilityLiveRegion='polite'>
  Clicked {this.state.count} times
</Text>
```

No método de exemplo acima _addOne muda a variável state.count. Assim que um usuário final clicar no TouchableWithoutFeedback, o TalkBack lê texto na exibição de texto por causa da propriedade 'accessibilityLiveRegion = "polite".

#### importantForAccessibility (Android)

No caso de dois componentes de UI sobrepostos com o mesmo pai, o foco de acessibilidade padrão pode ter um comportamento imprevisível. A propriedade 'importanteForAccessibility' resolverá isso controlando se uma view dispara eventos de acessibilidade e se é relatado para serviços de acessibilidade. Pode ser definido como 'auto', 'yes', 'no' e 'no-hide-descendants' (o último valor forçará os serviços de acessibilidade a ignorar o componente e todos os seus filhos).

```javascript
<View style={styles.container}>
  <View style={{position: 'absolute', left: 10, top: 10, right: 10, height: 100,
    backgroundColor: 'green'}} importantForAccessibility=”yes”>
    <Text> First layout </Text>
  </View>
  <View style={{position: 'absolute', left: 10, top: 10, right: 10, height: 100,
    backgroundColor: 'yellow'}} importantForAccessibility=”no-hide-descendants”>
    <Text> Second layout </Text>
  </View>
</View>
```

No exemplo acima, o layout amarelo e seus descendentes são completamente invisíveis ao TalkBack e a todos os outros serviços de acessibilidade. Então podemos usar facilmente views sobrepostas com o mesmo pai sem confundir o TalkBack.

### Checar se um Leitor de Tela está Ativado

A API `AccessibilityInfo` permite que você determine se um leitor de tela está ou não ativado. Veja a documentação [AccessibilityInfo documentation](docs/accessibilityinfo.html) para obter detalhes.

### Enviando Eventos de Acessibilidade (Android)

Às vezes é útil desencadear um evento de acessibilidade em um componente UI (ou seja, quando uma view personalizada aparecer em uma tela ou um botão de rádio personalizado for selecionado). O módulo Native UIManager expõe um método 'sendAccessibilityEvent' para este propósito. É preciso dois argumentos: etiqueta de view e um tipo de um evento.

```javascript
_onPress: function () {
  this.state.radioButton = this.state.radioButton === 'radiobutton_checked'? 'radiobutton_unchecked' : 'radiobutton_checked';
  if (this.state.radioButton === 'radiobutton_checked') {
    RCTUIManager.sendAccessibilityEvent(
      ReactNative.findNodeHandle(this),
      RCTUIManager.AccessibilityEventTypes.typeViewClicked);
  }
}

<CustomRadioButton
  accessibleComponentType={this.state.radioButton}
  onPress={this._onPress}/>
```

No exemplo acima, criamos um botão de opção personalizado que agora se comporta como um nativo. Mais especificamente, TalkBack agora anuncia corretamente mudanças na seleção do botão de rádio.


## Testando o Suporte ao VoiceOver (iOS)

Para habilitar o VoiceOver, vá para o aplicativo Configurações em seu dispositivo iOS. Toque Geral, depois Acessibilidade. Lá você encontrará muitas ferramentas que as pessoas usam para tornar seus dispositivos mais utilizáveis, como texto com mais negrito, contraste aumentado e VoiceOver.

Para habilitar o VoiceOver, toque no VoiceOver debaixo de "Visão" e alterne o interruptor que aparece no topo.

Na parte inferior das configurações de acessibilidade, há um "Atalho de Acessibilidade". Você pode usar isso para alternar o VoiceOver clicando três vezes no botão Início.
