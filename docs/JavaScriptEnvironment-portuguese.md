---
id: javascript-environment
title: JavaScript Environment
layout: docs
category: Guides
permalink: docs/javascript-environment.html
next: direct-manipulation
previous: gesture-responder-system
---

## Runtime de JavaScript

Quando estiver usando o React Native, você vai estar rodando o seu código em JavaScript em dois ambientes:

* Para emuladores e dispositivos de iOS e Android, o React Native utiliza o [JavaScriptCore](http://trac.webkit.org/wiki/JavaScriptCore), que é o motor de JavaScript que move o Safari. No iOS, o JSC não utiliza JIT devido à ausência de memória executável gravável nos apps para iOS.
* Ao utilizar a depuração do Chrome, ele roda todo o código de JavaScript dentro do próprio Chrome, e se comunica com o código nativo via WebSocket. Logo, você está utilizando o [V8](https://code.google.com/p/v8/).

Ao passo que ambos os ambientes são muito similares, você pode acabar se deparando com algumas inconsistências. Provavelmente iremos experimentar outros motores de JS no futuro; portanto é melhor evitar contar com as particularidades de quaisquer runtimes.

## Transformadores de Sintaxe para JavaScript

Os transformadores de sintaxe faz do ato de escrever código mais aprazível, ao permite-lhe utilizar a nova sintaxe do JavaScript sem ter que aguardar pelo seu suporte para todos os interpretadores.

Desde a sua versão 0.5.0, o React Native vem com o [compilador de JavaScript Babel](https://babeljs.io). Consulte a [documentação do Babel](https://babeljs.io/docs/plugins/#transform-plugins) sobre as transformações suportadas para mais detalhes.

Aqui está uma lista completa das [transformações habilitadas](https://github.com/facebook/react-native/blob/master/babel-preset/configs/main.js#L16) do React Native.

ES5

* Palavras Reservadas: `promise.catch(function() { });`

ES6

* [Arrow functions](http://babeljs.io/docs/learn-es2015/#arrows): `<C onPress={() => this.setState({pressed: true})}`
* [Block scoping](https://babeljs.io/docs/learn-es2015/#let-const): `let greeting = 'hi';`
* [Call spread](http://babeljs.io/docs/learn-es2015/#default-rest-spread): `Math.max(...array);`
* [Classes](http://babeljs.io/docs/learn-es2015/#classes): `class C extends React.Component { render() { return <View />; } }`
* [Constants](https://babeljs.io/docs/learn-es2015/#let-const): `const answer = 42;`
* [Destructuring](http://babeljs.io/docs/learn-es2015/#destructuring): `var {isActive, style} = this.props;`
* [for...of](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of): `for (var num of [1, 2, 3]) {}`
* [Modules](http://babeljs.io/docs/learn-es2015/#modules): `import React, { Component } from 'react';`
* [Computed Properties](http://babeljs.io/docs/learn-es2015/#enhanced-object-literals): `var key = 'abc'; var obj = {[key]: 10};`
* [Object Concise Method](http://babeljs.io/docs/learn-es2015/#enhanced-object-literals): `var obj = { method() { return 10; } };`
* [Object Short Notation](http://babeljs.io/docs/learn-es2015/#enhanced-object-literals): `var name = 'vjeux'; var obj = { name };`
* [Rest Params](https://github.com/sebmarkbage/ecmascript-rest-spread): `function(type, ...args) { }`
* [Template Literals](http://babeljs.io/docs/learn-es2015/#template-strings): ``var who = 'world'; var str = `Hello ${who}`;``

ES7

* [Object Spread](https://github.com/sebmarkbage/ecmascript-rest-spread): `var extended = { ...obj, a: 10 };`
* [Function Trailing Comma](https://github.com/jeffmo/es-trailing-function-commas): `function f(a, b, c,) { }`
* [Async Functions](https://github.com/tc39/ecmascript-asyncawait): `async function doStuffAsync() { const foo = await doOtherStuffAsync(); }`;

Específicos

* [JSX](https://facebook.github.io/react/docs/jsx-in-depth.html): `<View style={{color: 'red'}} />`
* [Flow](http://flowtype.org/): `function foo(x: ?number): string {}`


## Polyfills

Muitas funções padrões estão também disponíveis para todos os runtimes de JavaScript suportados.

Navegador

* [console.{log, warn, error, info, trace, table}](https://developer.chrome.com/devtools/docs/console-api)
* [CommonJS require](https://nodejs.org/docs/latest/api/modules.html)
* [XMLHttpRequest, fetch](docs/network.html#content)
* [{set, clear}{Timeout, Interval, Immediate}, {request, cancel}AnimationFrame](docs/timers.html#content)
* [navigator.geolocation](docs/geolocation.html#content)

ES6

* [Object.assign](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)
* String.prototype.{[startsWith](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/startsWith), [endsWith](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/endsWith), [repeat](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/repeats), [includes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/includes)}
* [Array.from](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/from)
* Array.prototype.{[find](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find), [findIndex](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex), [includes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/includes)}

ES7

* Object.{[entries](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/entries), [values](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/values)}

Específico

* `__DEV__`
