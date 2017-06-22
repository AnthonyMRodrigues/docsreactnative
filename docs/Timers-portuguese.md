---
id: timers
title: Timers
layout: docs
category: Guides
permalink: docs/timers.html
next: debugging
previous: accessibility
---

Os temporizadores são uma parte importante dum aplicativo e o React Native implementa os [temporizadores do navegador](https://developer.mozilla.org/en-US/Add-ons/Code_snippets/Timers).

## Temporizadores (Timers)

- setTimeout, clearTimeout
- setInterval, clearInterval
- setImmediate, clearImmediate
- requestAnimationFrame, cancelAnimationFrame

`requestAnimationFrame(fn)` não é o mesmo que `setTimeout(fn, 0)` - o anterior disparará depois que todo o quadro tiver se escoado; ao passo que o último disparará tão rapidamente quanto possível (acima de 1000x por segundo num iPhone 5S).

`setImmediate` é executado ao final do bloco de execução corrente do JavaScript, imediadamente antes de mandar a resposta em lote de volta ao nativo. Note que se você chamar `setImmediate` de dentro duma callback de `setImmediate`, ela será executada imediatamente, não cederá de volta ao nativo entre os intervalos.

A implementação `Promise` utiliza `setImmediate` como o seu primitivo de assincronicidade.


## Gerenciador de Interações (InteractionManager)

Uma razão do porquê dos apps nativos bem produzidos sentem-se tão fluidos é por evitarem operações pesadas durante as interações e animações. No React Native, atualmente temos uma limitação de que existe somente um único thread de execução no JS; mas você pode utilizar `InteractionManager` para assegurar que os trabalhos de execução com longa duração sejam agendados para iniciarem-se após quaisquer interações/animações tenham se finalizados.

Aplicativos podem agendar tarefas para rodarem após as interações com o seguinte:

```javascript
InteractionManager.runAfterInteractions(() => {
   // ...long-running synchronous task...
});
```

Compare isto com as outras alternativas de agendamento:

- requestAnimationFrame(): para código que anima uma visualização ao longo do tempo.
- setImmediate/setTimeout/setInterval(): roda o código mais tarde; notando que isto pode retardar as animações.
- runAfterInteractions(): roda o código mais tarde, mas sem retardar as animações ativas.

O sistema para manejo de toques considera que um ou mais toques ativos sejam uma 'interaction', e protelará os callbacks de `runAfterInteractions()` até que todos os toques tenham terminado ou sido cancelados.

O InteractionManager permite igualmente aos aplicativos registrarem animações ao criar um 'handle' de interação no começo da animação, e então limpá-lo uma vez concluído:

```javascript
var handle = InteractionManager.createInteractionHandle();
// run animation... (`runAfterInteractions` tasks are queued)
// later, on animation completion:
InteractionManager.clearInteractionHandle(handle);
// queued tasks run if all handles were cleared
```


## Mixin de Temporizadores (TimerMixin)

Descobrimos que a causa primária das fatalidades nos apps criados com React Native era devido aos temporizadores dispararem após um componente ter sido desmontado. Para resolver esta questão recorrente, introduzimos o `TimerMixin`. Se você incluir o `TimerMixin`, então você pode substituir as suas chamadas ao `setTimeout(fn, 500)` com o `this.setTimeout(fn, 500)` (apenas adicione `this.` na frente) e tudo será adequadamente arrumado para você quando o componente se desmontar.

Esta biblioteca não acompanha o React Native - de modo que para usá-la no seu projeto, você necessitará de instalá-la com `npm i react-timer-mixin --save` a partir do diretório do projeto.

```javascript
import TimerMixin from 'react-timer-mixin';

var Component = React.createClass({
  mixins: [TimerMixin],
  componentDidMount: function() {
    this.setTimeout(
      () => { console.log('I do not leak!'); },
      500
    );
  }
});
```

Isto eliminará muito do trabalho árduo de rastrear os bugs, tais como os travamentos causados por timeouts disparando após um componente ter sido desmontado.

Tenha em mente que se você utizar classes do ES6 para os seus componentes React [não existe API integrado para mixins](https://facebook.github.io/react/blog/2015/01/27/react-v0.13.0-beta-1.html#mixins). Para utilizar `TimerMixin` com classes do ES6, recomendamos o [react-mixin](https://github.com/brigand/react-mixin).
