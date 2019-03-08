---
id: debugging
title: Debugging
layout: docs
category: Guides
permalink: docs/debugging.html
next: performance
previous: timers
---

Ativando Atalhos do Teclado

## Ferramentas para desenvolvedores do Chrome

Para depurar o código JavaScript no Chrome, selecione "Depurar JS Remotamente" no Menu do Desenvolvedor. Isso abrirá uma nova guia em [http://localhost:8081/debugger-ui](http://localhost:8081/debugger-ui).

Selecione Ferramentas → Ferramentas do Desenvolvedor no menu do Chrome para abrir as [Ferramentas de desenvolvimento](https://developer.chrome.com/devtools). Você também pode acessar o DevTools usando atalhos de teclado (`⌘⌥I` no macOS, 'Ctrl''Shift''I' no Windows).  Você também pode querer ativar  [Pausar ao detectar exceções](http://stackoverflow.com/questions/2233339/javascript-is-there-a-way-to-get-chrome-to-break-on-all-errors/17324511#17324511) para uma melhor experiência durante a depuração.

> Nota: A extensão no Google Chorme "React Developer Tools"  não funciona com o React Native, mas você pode usar sua versão autônoma. Leia [está seção](docs/debugging.html#react-developer-tools) para saber como.

### Debugando usando um depurador JavaScript personalizado

Para usar um depurador JavaScript personalizado no lugar das Ferramentas do desenvolvedor do Chrome, defina a variável de ambiente  `REACT_DEBUGGER` como um comando que iniciará seu depurador personalizado. Você pode então selecionar "Depurar JS Remotamente" no Menu do Desenvolvedor para iniciar a depuração.

O depurador receberá uma lista de todas as raízes do projeto, separadas por um espaço. Por exemplo, se você definir o `REACT_DEBUGGER="node /path/to/launchDebugger.js --port 2345 --type ReactNative"`, então o comando `node /path/to/launchDebugger.js --port 2345 --type ReactNative /path/to/reactNative/app` será usado para iniciar seu depurador.

> Comandos de depuração personalizados executados dessa maneira devem ser processos de curta duração e não devem produzir mais de 200 kilobytes de saída.

## Ferramenta para Desenvolvedores React

Você pode usar [a versão independente da Ferramenta para Desenvolvedores React](https://github.com/facebook/react-devtools/tree/master/packages/react-devtools) para depurar a hierarquia do componente React.  Para usá-lo, instale o pacote `react-devtools` globalmente:

```
npm install -g react-devtools
```

Agora execute o `react-devtools` do terminal para iniciar o aplicativo DevTools autônomo:

```
react-devtools
```

![React DevTools](img/ReactDevTools.png)

Ele deve se conectar ao seu simulador dentro de alguns segundos.

> Nota: se você preferir evitar instalações globais, você pode adicionar `react-devtools` como uma dependência do projeto. Adicione o pacote `react-devtools` ao seu projeto usando `npm install --save-dev react devtools`, depois adicione `"react-devtools":"react-devtools"` ao `scripts` em seu `package.json` e depois execute `npm run react-devtools` na pasta do seu projeto para abrir o DevTools.

### Integração com o React Native Inspector

Abra o menu do desenvolvedor no aplicativo e escolha "Show Inspector". Ele exibirá uma sobreposição que permite tocar em qualquer elemento da interface do usuário e ver informações sobre ele:

![React Native Inspector](img/Inspector.gif)

No entanto, quando o `react-devtools` estiver em execução, o Inspector entrará em um modo especial e, em vez disso, usará o DevTools como interface principal. Neste modo, clicar em algo no simulador mostrará os componentes relevantes nos DevTools:

![React DevTools Inspector Integration](img/ReactDevToolsInspector.gif)

Você pode escolher "Ocultar inspetor" no mesmo menu para sair desse modo.

### Inspeção de instâncias de componentes

Quando depurar o JavaScript no Chrome, você pode inspecionar os acessórios e o estado dos componentes do React no console do navegador.

Primeiro, siga as instruções para depuração no Chrome para abrir o console do Chrome.

Certifique-se de que a lista suspensa no canto superior esquerdo do console do Chrome está dizendo `debuggerWorker.js`. **Esta etapa é essencial.**

E então, selecione um componente React no React DevTools. Existe uma caixa de pesquisa no topo que ajuda você a encontrar um pelo nome. Assim que você selecioná-lo, ele estará disponível como `$r` no console do Google Chrome, permitindo que você inspecione suas propriedades, estado e instância.

![React DevTools Chrome Console Integration](img/ReactDevToolsDollarR.gif)

## Monitor de Desempenho

Você pode habilitar uma sobreposição de desempenho para ajudá-lo a depurar problemas de desempenho selecionando "Perf Monitor" no Menu do Desenvolvedor.

<hr style="margin-top:25px; margin-bottom:25px;"/>

#  Depuração em aplicativos ejetados

<div class="banner-crna-ejected" style="margin-top:25px">
  <h3>Projetos com somente código nativo</h3>
  <p>
   O restante deste guia aplica-se apenas a projetos feitos com <code>react-native init</code>
    ou para aqueles feitos com Create React Native App, que já foram ejetados. Para
    mais informações sobre ejetar, por favor, veja <a href="https://github.com/react-community/create-react-native-app/blob/master/EJECTING.md" target="_blank">guide</a> em
    o repositório React Native App.
  </p>
</div>

## Accessing console logs

You can display the console logs for an iOS or Android app by using the following commands in a terminal while the app is running:

```
$ react-native log-ios
$ react-native log-android
```

You may also access these through `Debug → Open System Log...` in the iOS Simulator or by running `adb logcat *:S ReactNative:V ReactNativeJS:V` in a terminal while an Android app is running on a device or emulator.

> If you're using Create React Native App, console logs already appear in the same terminal output as the packager.

## Debugging on a device with Chrome Developer Tools

> If you're using Create React Native App, this is configured for you already.

On iOS devices, open the file [`RCTWebSocketExecutor.m`](https://github.com/facebook/react-native/blob/master/Libraries/WebSocket/RCTWebSocketExecutor.m) and change "localhost" to the IP address of your computer, then select "Debug JS Remotely" from the Developer Menu.

On Android 5.0+ devices connected via USB, you can use the [`adb` command line tool](http://developer.android.com/tools/help/adb.html) to setup port forwarding from the device to your computer:

`adb reverse tcp:8081 tcp:8081`

Alternatively, select "Dev Settings" from the Developer Menu, then update the "Debug server host for device" setting to match the IP address of your computer.

> If you run into any issues, it may be possible that one of your Chrome extensions is interacting in unexpected ways with the debugger. Try disabling all of your extensions and re-enabling them one-by-one until you find the problematic extension.

### Debugging with [Stetho](http://facebook.github.io/stetho/) on Android

1. In ```android/app/build.gradle```, add these lines in the `dependencies` section:

   ```gradle
   compile 'com.facebook.stetho:stetho:1.3.1'
   compile 'com.facebook.stetho:stetho-okhttp3:1.3.1'
   ```

2. In ```android/app/src/main/java/com/{yourAppName}/MainApplication.java```, add the following imports:

   ```java
   import com.facebook.react.modules.network.ReactCookieJarContainer;
   import com.facebook.stetho.Stetho;
   import okhttp3.OkHttpClient;
   import com.facebook.react.modules.network.OkHttpClientProvider;
   import com.facebook.stetho.okhttp3.StethoInterceptor;
   import java.util.concurrent.TimeUnit;
   ```

3. In ```android/app/src/main/java/com/{yourAppName}/MainApplication.java``` add the function:
   ```java
   public void onCreate() {
         super.onCreate();
         Stetho.initializeWithDefaults(this);
         OkHttpClient client = new OkHttpClient.Builder()
         .connectTimeout(0, TimeUnit.MILLISECONDS)
         .readTimeout(0, TimeUnit.MILLISECONDS)
         .writeTimeout(0, TimeUnit.MILLISECONDS)
         .cookieJar(new ReactCookieJarContainer())
         .addNetworkInterceptor(new StethoInterceptor())
         .build();
         OkHttpClientProvider.replaceOkHttpClient(client);
   }
   ```

4. Run  ```react-native run-android ```

5. In a new Chrome tab, open: ```chrome://inspect```, then click on 'Inspect device' (the one followed by "Powered by Stetho").

## Debugging native code

When working with native code, such as when writing native modules, you can launch the app from Android Studio or Xcode and take advantage of the native debugging features (setting up breakpoints, etc.) as you would in case of building a standard native app.
