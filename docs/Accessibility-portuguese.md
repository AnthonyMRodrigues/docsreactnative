---
id: accessibility
title: Accessibility
layout: docs
category: Guides
permalink: docs/accessibility.html
next: timers
previous: animations
---

## Acessibilidade na aplicação nativa (iOS e Android)
Tanto o iOS como o Android oferecem APIs para tornar acessíveis aplicativos para pessoas com deficiência. Além disso, ambas as plataformas fornecem tecnologias assistidas, como os leitores de tela VoiceOver (iOS) e TalkBack (Android) para deficientes visuais. Da mesma forma, no React Native incluímos APIs projetadas para fornecer aos desenvolvedores suporte para tornar os aplicativos mais acessíveis. Tome nota, iOS e Android diferem ligeiramente em suas abordagens e, portanto, as implementações do Reative Native podem variar de acordo com a plataforma.

Além desta documentação, você pode encontrar [esta postagem do blog](https://code.facebook.com/posts/435862739941212/making-react-native-apps-accessible/) sobre a acessibilidade do React Native para ser útil.

## Fazendo aplicativos acessíveis

### Propriedades de acessibilidade

#### acessível (iOS, Android)

Quando `true`, indica que a view é um elemento de acessibilidade. Quando uma view é um elemento de acessibilidade, agrupa seus filhos em um único componente selecionável. Por padrão, todos os elementos tocáveis ​​estão acessíveis.

No Android, a propriedade 'acessible = {true}' para uma proprieda react-native será traduzida para nativo 'focusable = {true}'.

```javascript
<View accessible={true}>
  <Text>texto um</Text>
  <Text>texto dois</Text>
</View>
```

No exemplo acima, não podemos obter o foco de acessibilidade separadamente em 'texto um' e 'texto dois'. Em vez disso, ficamos focados em uma visão pai com propriedade "acessível".



#### accessibilityLabel (iOS, Android)

Quando uma exibição é marcada como acessível, é uma boa prática definir uma Classificação de acessibilidade na vista, para que as pessoas que usam o VoiceOver saibam qual o elemento que selecionaram. O VoiceOver irá ler essa string quando um usuário selecionar o elemento associado.

Para usar, defina a propriedade `accessibilityLabel` como uma string personalizada na sua view:

```javascript
<TouchableOpacity accessible={true} accessibilityLabel={'Tap me!'} onPress={this._onPress}>
  <View style={styles.button}>
    <Text style={styles.buttonText}>Press me!</Text>
  </View>
</TouchableOpacity>
```

No exemplo acima, o `accessibilityLabel` no elemento TouchableOpacity seria padrão para" Press me! ". A label é construída pela concatenação de todos os filhos do nó de texto separados por espaços.

#### accessibilityTraits (iOS)

As características de acessibilidade indicam a uma pessoa usando o VoiceOver que tipo de elemento eles selecionaram. Esse elemento é um rótulo? Um botão? Um cabeçalho? Essas questões são respondidas por `accessTraits`.

Para usar, defina a propriedade `accessibilityTraits` como uma das (ou uma array de) seqüências de caracteres de acessibilidade:

* **none** Usado quando o elemento não possui traços.
* **button** Usado quando o elemento deve ser tratado como um botão.
* **link** Usado quando o elemento deve ser tratado como um link.
* **header** Usado quando um elemento age como um cabeçalho para uma seção de conteúdo (por exemplo, o título de um navigation bar).
* **search** Usado quando o elemento do campo de texto também deve ser tratado como um campo de pesquisa.
* **image** Usado quando o elemento deve ser tratado como uma imagem. Pode ser combinado com um botão ou link, por exemplo.
* **selected**  Usado quando o elemento é selecionado. Por exemplo, uma linha selecionada em uma tabela ou um botão selecionado dentro de um controle segmentado.
* **plays** Usado quando o elemento reproduz seu próprio som quando ativado.
* **key** Usado quando o elemento atua como uma tecla de teclado.
* **text** Usado quando o elemento deve ser tratado como texto estático que não pode ser alterado.
* **summary** Usado quando um elemento pode ser usado para fornecer um resumo rápido das condições atuais no aplicativo quando o aplicativo é iniciado pela primeira vez. Por exemplo, quando o Tempo inicia, o elemento com as condições climáticas de hoje é marcado com essa característica.
* **disabled** Usado quando o controle não está ativado e não responde à entrada do usuário.
* **frequentUpdates** Usado quando o elemento atualiza freqüentemente seu rótulo ou valor, mas muitas vezes para enviar notificações. Permite que um cliente de acessibilidade solicite alterações. Um cronômetro seria um exemplo..
* **startsMedia** Usado quando a ativação de um elemento inicia uma sessão de mídia (por exemplo, reproduzindo um filme, gravando áudio) que não devem ser interrompidos pela saída de uma tecnologia assistiva, como o VoiceOver.
* **adjustable** Usado quando um elemento pode ser "ajustado" (por exemplo, um controle deslizante).
* ** allowsDirectInteraction ** Usado quando um elemento permite interação de toque direto para usuários do VoiceOver (por exemplo, uma exibição que representa um teclado de piano).
* ** pageTurn ** Informa ao VoiceOver que ele deve rolar para a próxima página quando terminar de ler o conteúdo do elemento.

#### accessibilityViewIsModal (iOS)

Um valor booleano que indica se o VoiceOver deve ignorar os elementos dentro das vistas que são irmãos do receptor.

Por exemplo, em uma janela que contém exibições irmãs `A` e` B`, configurar `accessibilityViewIsModal` para` true` na vista `B` faz com que o VoiceOver ignore os elementos na vista` A`.
Por outro lado, se a vista `B 'contiver uma visão secundária` C` e você definir `accessibilityViewIsModal` para` true` na vista `C`, o VoiceOver não ignora os elementos na vista` A`

#### onAccessibilityTap (iOS)

Use esta propriedade para atribuir uma função personalizada a ser chamada quando alguém ativa um elemento acessível, tocando duas vezes, enquanto estiver selecionado.

#### onMagicTap (iOS)

Atribua esta propriedade a uma função personalizada que será chamada quando alguém executa o gesto de "toque mágico", que é um toque duplo com dois dedos. Uma função de toque mágica deve executar a ação mais relevante que um usuário pode assumir em um componente. No aplicativo Telefone no iPhone, uma batida mágica responde a uma chamada telefônica ou termina a atual. Se o elemento selecionado não tiver uma função `onMagicTap`, o sistema irá percorrer a hierarquia de exibição até encontrar uma visão que faça.

#### accessibilityComponentType (Android)

Em alguns casos, também queremos alertar o usuário final do tipo de componente selecionado (isto é, que é um "botão"). Se estivéssemos usando botões nativos, isso funcionaria automaticamente. Como estamos usando o javascript, precisamos fornecer um pouco mais de contexto para o TalkBack. Para fazer isso, você deve especificar a propriedade 'accessibilityComponentType' para qualquer componente de UI. Por exemplo, apoiamos 'botão', 'radiobutton_checked' e 'radiobutton_unchecked' e assim por diante.

```javascript
<TouchableWithoutFeedback accessibilityComponentType=”button”
  onPress={this._onPress}>
  <View style={styles.button}>
    <Text style={styles.buttonText}>Press me!</Text>
  </View>
</TouchableWithoutFeedback>
```

In the above example, the TouchableWithoutFeedback is being announced by TalkBack as a native Button.

#### accessibilityLiveRegion (Android)

Quando os componentes mudam dinamicamente, queremos o TalkBack para alertar o usuário final. Isso é possível pela propriedade 'accessibilityLiveRegion'. Pode ser definido como 'none', 'polite' e 'assertive':

* **none** Os serviços de acessibilidade não devem anunciar alterações nesta visualização.
* **polite** Os serviços de acessibilidade devem anunciar mudanças nesta visão.
* **assertive** Os serviços de acessibilidade devem interromper o discurso em andamento para anunciar imediatamente mudanças nesta visão.

```javascript
<TouchableWithoutFeedback onPress={this._addOne}>
  <View style={styles.embedded}>
    <Text>Click me</Text>
  </View>
</TouchableWithoutFeedback>
<Text accessibilityLiveRegion="polite">
  Clicked {this.state.count} times
</Text>
```

No método de exemplo acima _addOne muda a variável state.count. Assim que um usuário final clica no TouchableWithoutFeedback, o TalkBack lê texto na exibição de texto por causa da propriedade 'accessibilityLiveRegion = "polite".

#### importantForAccessibility (Android)

No caso de dois componentes de UI sobrepostos com o mesmo pai, o foco de acessibilidade padrão pode ter um comportamento imprevisível. A propriedade 'importanteForAccessibility' resolverá isso controlando se uma exibição dispara eventos de acessibilidade e se for relatado para serviços de acessibilidade. Pode ser definido como 'auto', 'sim', 'não' e 'não-esconder-descendentes' (o último valor forçará os serviços de acessibilidade a ignorar o componente e todos os seus filhos).

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

No exemplo acima, o layout amarelo e seus descendentes são completamente invisíveis para TalkBack e todos os outros serviços de acessibilidade. Então, podemos usar facilmente vistas sobrepostas com o mesmo pai sem confundir o TalkBack.

### Checking if a Screen Reader is Enabled

A API `AccessibilityInfo` permite que você determine se um leitor de tela está ou não ativado. Veja a documentação [AcessibilidadeInfo](docs / accessibilityinfo.html) para obter detalhes.

### Sending Accessibility Events (Android)

Às vezes, é útil desencadear um evento de acessibilidade em um componente UI (ou seja, quando uma exibição personalizada aparece em uma tela ou um botão de opção personalizado foi selecionado). O módulo Native UIManager expõe um método 'sendAccessibilityEvent' para este propósito. É preciso dois argumentos: ver tag e um tipo de evento.

```javascript
_onPress: function() {
  this.state.radioButton = this.state.radioButton === “radiobutton_checked” ?
  “radiobutton_unchecked” : “radiobutton_checked”;
  if (this.state.radioButton === “radiobutton_checked”) {
    RCTUIManager.sendAccessibilityEvent(
      ReactNative.findNodeHandle(this),
      RCTUIManager.AccessibilityEventTypes.typeViewClicked);
  }
}

<CustomRadioButton
  accessibleComponentType={this.state.radioButton}
  onPress={this._onPress}/>
```

No exemplo acima, criamos um botão de opção personalizado que agora se comporta como um nativo. Mais especificamente, TalkBack agora anuncia corretamente mudanças na seleção do botão de opção.


## Testando VoiceOver Support (iOS)

Para habilitar o VoiceOver, vá para o aplicativo Configurações em seu dispositivo iOS. Toque Geral, depois Acessibilidade. Lá você encontrará muitas ferramentas que as pessoas usam para tornar seus dispositivos mais utilizáveis, como texto mais ousado, contraste aumentado e VoiceOver.

Para habilitar o VoiceOver, toque no VoiceOver em "Visão" e alternar o interruptor que aparece no topo.

Na parte inferior das configurações de acessibilidade, há um "Atalho de acessibilidade". Você pode usar isso para alternar o VoiceOver clicando três vezes no botão Início.
