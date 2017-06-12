---
id: quick-start-getting-started
title: Getting Started
layout: docs
category: The Basics
permalink: docs/getting-started.html
next: tutorial
---

<style>
  .toggler li {
    display: inline-block;
    position: relative;
    top: 1px;
    padding: 10px;
    margin: 0px 2px 0px 2px;
    border: 1px solid #05A5D1;
    border-bottom-color: transparent;
    border-radius: 3px 3px 0px 0px;
    color: #05A5D1;
    background-color: transparent;
    font-size: 0.99em;
    cursor: pointer;
  }
  .toggler li:first-child {
    margin-left: 0;
  }
  .toggler li:last-child {
    margin-right: 0;
  }
  .toggler ul {
    width: 100%;
    display: inline-block;
    list-style-type: none;
    margin: 0;
    border-bottom: 1px solid #05A5D1;
    cursor: default;
  }
  @media screen and (max-width: 960px) {
    .toggler li,
    .toggler li:first-child,
    .toggler li:last-child {
      display: block;
      border-bottom-color: #05A5D1;
      border-radius: 3px;
      margin: 2px 0px 2px 0px;
    }
    .toggler ul {
      border-bottom: 0;
    }
  }
  .toggler a {
    display: inline-block;
    padding: 10px 5px;
    margin: 2px;
    border: 1px solid #05A5D1;
    border-radius: 3px;
    text-decoration: none !important;
  }
  .display-guide-quickstart .toggler .button-quickstart,
  .display-guide-native .toggler .button-native,
  .display-os-mac .toggler .button-mac,
  .display-os-linux .toggler .button-linux,
  .display-os-windows .toggler .button-windows,
  .display-platform-ios .toggler .button-ios,
  .display-platform-android .toggler .button-android {
    background-color: #05A5D1;
    color: white;
  }
  block { display: none; }
  .display-guide-quickstart.display-platform-ios.display-os-mac .quickstart.ios.mac,
  .display-guide-quickstart.display-platform-ios.display-os-linux .quickstart.ios.linux,
  .display-guide-quickstart.display-platform-ios.display-os-windows .quickstart.ios.windows,
  .display-guide-quickstart.display-platform-android.display-os-mac .quickstart.android.mac,
  .display-guide-quickstart.display-platform-android.display-os-linux .quickstart.android.linux,
  .display-guide-quickstart.display-platform-android.display-os-windows .quickstart.android.windows,    .display-guide-native.display-platform-ios.display-os-mac .native.ios.mac,
  .display-guide-native.display-platform-ios.display-os-linux .native.ios.linux,
  .display-guide-native.display-platform-ios.display-os-windows .native.ios.windows,
  .display-guide-native.display-platform-android.display-os-mac .native.android.mac,
  .display-guide-native.display-platform-android.display-os-linux .native.android.linux,
  .display-guide-native.display-platform-android.display-os-windows .native.android.windows {
    display: block;
  }
</style>

Essa página irpa ajudar você a instalar e buildar a sua primeira aplicação React Natuve. Se você já tem o React Native instalado, você pode ir direto para o [Tutorial](docs/tutorial.html).


<div class="toggler">
  <ul role="tablist" >
    <li id="quickstart" class="button-quickstart" aria-selected="false" role="tab" tabindex="0" aria-controls="quickstarttab" onclick="displayTab('guide', 'quickstart')">
      Inicio Rápido.
    </li>
    <li id="native" class="button-native" aria-selected="false" role="tab" tabindex="-1" aria-controls="nativetab" onclick="displayTab('guide', 'native')">
      Criando o seu projeto com código nativo.
    </li>
  </ul>
</div>

<block class="quickstart mac windows linux ios android" />

[Criando o aplicativo Reactive Native](https://github.com/react-community/create-react-native-app) é a maneira mais fácil de iniciar a criar uma nova aplicação React Native. Isso permite você iniciar um projeto sem instalar ou configurar qualquer ferramenta para buildar código nativo - sem Xcode ou instalação necessária de Android Studio (veja[Caveats](docs/getting-started.html#caveats))

Assumindo que você já tenha o [Node](https://nodejs.org/en/download/) instalado, você pode usar o NPM para instalar o `create-react-native-app` usando a linha de comando: 


```
npm install -g create-react-native-app
```

Então rode o seguinte comando para criar um novo projeto React Native chamado "AwesomeProject":


```
create-react-native-app AwesomeProject

cd AwesomeProject
npm start
```
Isso irá iniciar um servidor de desenvolvimento para você, e printar um QR code no seu terminal.

## Rodando sua aplicação React Native

Instale o aplicativo [Expo](https://expo.io) no seu iOS ou Android e conecte a mesma rede sem fio do seu computador. Usando o aplicativo do Expo, escaneie o QR code do seu terminal e abra o seu projeto. 

### Modificando o seu aplicativo

Agora que você já teve sucesso em rodar o seu aplicativo, vamos modifica-lo. Abra o `App.js` no seu editor de texto preferido e edite algumas linhas. A aplicação ira reiniciar automáticamente assim que você salvar as suas mudanças.


### É isso!

Parabéns! Você rodou e modificou com sucesso o seu primeiro app em React Native.

<center><img src="img/react-native-congratulations.png" width="150"></img></center>

## E agora?

- Criando a aplicação em React Native também tem o [guia do usuário](https://github.com/react-community/create-react-native-app/blob/master/react-native-scripts/template/README.md) você pode referencia-lo caso tenha alguma pergunta especifica sobre a ferramenta.

- Se você não conseguir, veja a sessão [Problemas](https://github.com/react-community/create-react-native-app/blob/master/react-native-scripts/template/README.md#troubleshooting) no Readme para a criação de uma aplicação React Native.

Se você está curioso em aprender mais sobre o React Native continue no [Tutorial](docs/tutorial.html).

### Rodando seu aplicativo em um simulador virtual.

Criar a sua aplicação React Native fica mais fácil rodar o aplicativo em um dispositivo fisico sem configurar um ambiente de desenvolvimento. Se você desejar rodar o seu aplicativo em um simulador iOS ou um dispositivo virtual android, por favor vá nas instruções para buildar projetos com códigps nativos para aprender como instalar o Xcode e configurar o seu ambiente de desenvolvimento Android.

Uma vez que você tenha configurado, você pode lançar seu aplicativo em um dispositivo virtual Android rodando o comando `npm run android`, ou em um simulador iOS rodando o comando `npm run ios` (Somente no macOS).


### Ressalvas - Confirmar se está correto

Como você não constrói qualquer código nativo usando o "Creat React Native App" para criar um projeto, não é possível incluir um módulo nativo customizado além das APIs do React Native e componentes que estão disponiveis no aplicativo Expo.

Se você sabe o que será necessário incluir no seu código nativo, 'Create React Native App' ainda é um bom jeito de começar. Nesse caso você só irá precisar eventualmente "[ejetar](https://github.com/react-community/create-react-native-app/blob/master/react-native-scripts/template/README.md#ejecting-from-create-react-native-app)" para criar suas próprias builds nativas. Se você ejetar, as instruções do "Criando projeto com código nativo" serão requeridas para você continuar trabalhando no seu projeto.

Para criar uma aplicação com React Native você precisa configurar seu projeto com a mais recenter versão que é suportada pelo aplicativo Expo. O aplicativo Expo normalmente ganha suporte a uma nova versão do React Native uma semana após a release e estabilidade serem lançadas. Você pode checar [essa documentação](https://github.com/react-community/create-react-native-app/blob/master/VERSIONS.md) para encontrar quais versões são suportadas.

Se você está integrando o React Native em um projeto existente, você precisa deixar a parte "Criando seu aplicativo React Native" e ir direto para as configurações de ambiente de criação de nativos. Selecione "Criando projetos com código nativo" para instruções de configurações para buildar nativos do React Native.

<block class="native mac windows linux ios android" />

<p>Siga essas instruções se você precisa construir código nativo no seu projeto. Por exemplo, se você está integrando o React Native em uma aplicação já existente ou se você precisa "ejetar" [Criando aplicação React Native](#getting-started-portuguese) tudo que você precisa está nessa seção</p>

Essa instrução é um pouco diferente dependendo do sistema operacional que você está usando para desenvolver, e se você está inciando o desenvolvimento para Android ou iOS. Se você deseja desenvolver para ambos os sistemas, está tudo bem - você só precisa escolher um pra começar, já que as configurações são um pouco diferentes.

<div class="toggler">
  <span>Sistema operacional usado para o desenvolvimento:</span>
  <a href="javascript:void(0);" class="button-mac" onclick="displayTab('os', 'mac')">macOS</a>
  <a href="javascript:void(0);" class="button-windows" onclick="displayTab('os', 'windows')">Windows</a>
  <a href="javascript:void(0);" class="button-linux" onclick="displayTab('os', 'linux')">Linux</a>
  <span>Sistema escolhido para desenvolver:</span>
  <a href="javascript:void(0);" class="button-ios" onclick="displayTab('platform', 'ios')">iOS</a>
  <a href="javascript:void(0);" class="button-android" onclick="displayTab('platform', 'android')">Android</a>
</div>

<block class="native linux windows ios" />

## Sem suporte

<blockquote><p> Um Mac é necessário para buildar projetos em código nativo para iOS. Você pode seguir até <a href="docs/getting-started.html" onclick="displayTab('guide', 'quickstart')">Rápido Inicio</a> para aprender a criar aplicativos usando o React Native.</p></blockquote>

<block class="native mac ios" />

## Instalando dependencias.

Você irá precisar do Node, Watchman, comandos do React Native, e Xcode.

Enquanto isso você pode usar o editor de texto de sua escolha para desenvolver, você só precisa do Xcode instalado para configurações necessárias para buildar o seu aplicativo em React Native para iOS.

<block class="native mac android" />

## Instalando dependencias.

Você irá precisar do Node, Watchman, comandos do React Native, a JDK, e Android Studio.

<block class="native linux android" />

## Instalando dependencias.

Você irá precisar do Node, Watchman, comandos do React Native, a JDK, e Android Studio.

<block class="native windows android" />

## Instalando dependencias.

Você irá precisar do Node, Watchman, comandos do React Native, Python2, a JDK, e Android Studio.

<block class="native mac windows linux android" />

Enquanto isso você pode usar o editor de texto de sua escolha para desenvolver, você só precisa do Android Studio instalado para configurações necessárias para buildar o seu aplicativo em React Native para Android.

<block class="native mac ios android" />

### Node, Watchman

Nós recomendamos instalar o Node e Watchman usando o [Homebrew](http://brew.sh/). Rode os seguintes comandos no termminal após terminal a instalação do Homebrew:

```
brew install node
brew install watchman
```

Se você já tem o Node istalado no seu sistema, tenha certeza que está na versão 4 ou mais recente.

[Watchman](https://facebook.github.io/watchman) é uma ferramenta do Facebook para acompanhar mudanças em seu sistema. É altamente recomendado você instalar para ter uma melhor perfomance.

<block class="native linux android" />

### Node

Siga as [instruções de instalação para sua distribuição linux](https://nodejs.org/en/download/package-manager/) para instalar a versão 6 ou mais recente do Node.

<block class='native windows android' />

### Node, Python2, JDK

Nós recomendamos a instalação do Node e Python2 via [Chocolatey](https://chocolatey.org) um gerenciador de pacotes para Windows popular. 

React Native também requer uma versão recente do [Java SE Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) assim como a do Python 2. Ambos podem ser instalados usando o Chocolatey.

Abra o Prompt de comando em modo Administrador (botão direto no Prompt de comando e selecione "Rode como Administrador"), então rode os seguintes comandos:

```powershell
choco install nodejs.install
choco install python2
choco install jdk8
```
Se você já tem o Node instalado no seu sistema, tenha certeza que está na versão 4 ou mais recente. Se você já tem o JDK em seu sistema, tenha certeza que está na versão ou mais recente.

> Você pode achar opções de instalações adicionais na [Página de Downloads do Node](https://nodejs.org/en/download/).

<block class="native mac ios android" />

### O React Native CLI

Node vem com NPM, o que deixa instalar o CLI do React Native.

Rode os seguintes comandos no seu terminal:

```
npm install -g react-native-cli
```
> Se você receber uma mensagem de erro tipo `Cannot find module 'npmlog'`, tente instalar o NPM diretamente: `curl -0 -L https://npmjs.org/install.sh | sudo sh`.

<block class="native windows linux android" />

### O React Native CLI

Node vem com NPM, o que deixa instalar o CLI do React Native.

Rode os seguintes comandos no seu Prompt de comando:

```powershell
npm install -g react-native-cli
```

> Se você receber uma mensagem de erro tipo `Cannot find module 'npmlog'`, tente instalar o NPM diretamente: `curl -0 -L https://npmjs.org/install.sh | sudo sh`.

<block class="native mac ios" />

### Xcode

A maneira mais fácil de instalar o Xcode é via [Mac App Store](https://itunes.apple.com/us/app/xcode/id497799835?mt=12). Instalando o Xcode também será instalado o simulador de iOS e todas as ferramentas necessárias para buildar o seu aplicativo em iOS.

Se você já tem o Xcode instalado no seu sistema, tenha certeza que está na versão 8 ou superior.

#### Ferrmantas de linha de comando

Você também precisa instalar as ferramentas de linha de comando do Xcode. Abra o Xcode, então no menu do Xcode vá em "Preferências...". Vá no painel de localização e instale as ferramentas, selecionando as mais recentes versões de ferramentas de linha de comando.

![Ferramenta de linha de comando Xcode](img/XcodeCommandLineTools.png)

<block class="native mac linux android" />

### Java Development Kit

React Native precisa da mais recente versão do Java SE Development Kit (JDK). Caso necessário faça [Download e instale o JDK 8 ou mais recente](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).

<block class="native mac linux windows android" />

### Ambiente de desenvolvimento Android

Configurar o seu ambiente de desenvolvimento pode ser tedioso se você é novo no desenvolvimento Android. Se você já está familiarizado com o desenvolvimento Android então serão poucas coisas que terá que configurar. Em todo caso, por favor siga corretamente e com cuidado os próximos passos.

<block class="native mac windows linux android" />

#### 1. Instale o Android Studio

[Download e instalação do Android Studio](https://developer.android.com/studio/index.html). Escolha a opção de configuração "Custom/Customizada" quando a caixa de seleção do tipo de instalação aparecer, Tenha certeza de marcar as seguintes opções.

<block class="native mac windows android" />

- `Android SDK`
- `Android SDK Platform`
- `Performance (Intel ® HAXM)`
- `Android Virtual Device`

<block class="native linux android" />

- `Android SDK`
- `Android SDK Platform`
- `Android Virtual Device`

<block class="native mac windows linux android" />

Então clique em "Next/Próximo" para instalar todos esses componentes.

> Se as caixas de seleção (checkboxes) estiverem cinza, você terá a chance de instalar os componentes depois.

Uma vez que a configuração tenha terminado, você irá para a tela Inicial, siga o próximo passo.

#### 2. Instale o Android SDK

O Android Studio instala somente a versão mais recente do Android SDK por padrão. Para criar uma aplicação React Native com código nativo, precisará do `SDK Android 6.0 (Marshmallow)` em especifico, Androids SDKs podem ser instaladas pelo SDK Manager do Android Studio.

O SDK Manager pode ser acessado pela tela inicial do Android Studio. Clique em Configuração, então selecione "SDK Manager".

<block class="native mac android" />

![Tela Inicial Android Studio](img/AndroidStudioWelcomeMacOS.png)

<block class="native windows android" />

![Tela inicial Android Studio](img/AndroidStudioWelcomeWindows.png)

<block class="native mac windows linux android" />

> O SDK Manager também pode ser encontrado no Android Studio pelo caminho "Preferences", dentro de **Appearance & Behavior** → **System Settings** → **Android SDK**.

Selecione as "SDK Platforms" do SDK Manager, então marque o checkbox próximo ao "Show Package Details" no canto inferior direito. Olhe para a expansão e selecione o `Android 6.0 (Marshmallow)`, então tenha certeza que todos os itens foram marcados.

- `Google APIs`
- `Android SDK Platform 23`
- `Intel x86 Atom_64 System Image`
- `Google APIs Intel x86 Atom_64 System Image`

<block class="native mac android" />

![Android SDK Manager](img/AndroidSDKManagerMacOS.png)

<block class="native windows android" />

![Android SDK Manager](img/AndroidSDKManagerWindows.png)

<block class="native windows mac linux android" />

Next, select the "SDK Tools" tab and check the box next to "Show Package Details" here as well. Look for and expand the "Android SDK Build-Tools" entry, then make sure that `23.0.1` is selected.

<block class="native mac android" />

![Android SDK Manager - 23.0.1 Build Tools](img/AndroidSDKManagerSDKToolsMacOS.png)

<block class="native windows android" />

![Android SDK Manager - 23.0.1 Build Tools](img/AndroidSDKManagerSDKToolsWindows.png)

<block class="native windows mac linux android" />

Finally, click "Apply" to download and install the Android SDK and related build tools.

<block class="native mac android" />

![Android SDK Manager - Installs](img/AndroidSDKManagerInstallsMacOS.png)

<block class="native windows android" />

![Android SDK Manager - Installs](img/AndroidSDKManagerInstallsWindows.png)

<block class="native mac windows linux android" />

#### 3. Configure the ANDROID_HOME environment variable

The React Native tools require some environment variables to be set up in order to build apps with native code.

<block class="native mac linux android" />

Add the following lines to your `$HOME/.bash_profile` config file:

<block class="native mac android" />

```
export ANDROID_HOME=$HOME/Library/Android/sdk
export PATH=$PATH:$ANDROID_HOME/tools
export PATH=$PATH:$ANDROID_HOME/platform-tools
```

<block class="native linux android" />

```
export ANDROID_HOME=$HOME/Android/Sdk
export PATH=$PATH:$ANDROID_HOME/tools
export PATH=$PATH:$ANDROID_HOME/platform-tools
```

<block class="native mac linux android" />

> `.bash_profile` is specific to `bash`. If you're using another shell, you will need to edit the appropriate shell-specific config file.

Type `source $HOME/.bash_profile` to load the config into your current shell. Verify that ANDROID_HOME has been added to your path by running `echo $PATH`.

> Please make sure you use the correct Android SDK path. You can find the actual location of the SDK in the Android Studio "Preferences" dialog, under **Appearance & Behavior** → **System Settings** → **Android SDK**.

<block class="native windows android" />

Open the System pane under **System and Security** in the Control Panel, then click on **Change settings...**. Open the **Advanced** tab and click on **Environment Variables...**. Click on **New...** to create a new `ANDROID_HOME` user variable that points to the path to your Android SDK:

![ANDROID_HOME Environment Variable](img/AndroidEnvironmentVariableANDROID_HOME.png)

The SDK is installed, by default, at the following location:

```powershell
c:\Users\YOUR_USERNAME\AppData\Local\Android\Sdk
```

You can find the actual location of the SDK in the Android Studio "Preferences" dialog, under **Appearance & Behavior** → **System Settings** → **Android SDK**.

Open a new Command Prompt window to ensure the new environment variable is loaded before proceeding to the next step.

<block class="native linux android" />

### Watchman (optional)

Follow the [Watchman installation guide](https://facebook.github.io/watchman/docs/install.html#build-install) to compile and install Watchman from source.

> [Watchman](https://facebook.github.io/watchman/docs/install.html) is a tool by Facebook for watching
changes in the filesystem. It is highly recommended you install it for better performance, but it's alright to skip this if you find the process to be tedious.

<block class="native mac ios" />

## Creating a new application

Use the React Native command line interface to generate a new React Native project called "AwesomeProject":

```
react-native init AwesomeProject
```

This is not necessary if you are integrating React Native into an existing application, if you "ejected" from Create React Native App, or if you're adding iOS support to an existing React Native project (see [Platform Specific Code](docs/platform-specific-code.html)).

<block class="native mac windows linux android" />

## Creating a new application

Use the React Native command line interface to generate a new React Native project called "AwesomeProject":

```
react-native init AwesomeProject
```

This is not necessary if you are integrating React Native into an existing application, if you "ejected" from Create React Native App, or if you're adding Android support to an existing React Native project (see [Platform Specific Code](docs/platform-specific-code.html)).

<block class="native mac windows linux android" />

## Preparing the Android device

You will need an Android device to run your React Native Android app. This can be either a physical Android device, or more commonly, you can use an Android Virtual Device which allows you to emulate an Android device on your computer.

Either way, you will need to prepare the device to run Android apps for development.

### Using a physical device

If you have a physical Android device, you can use it for development in place of an AVD by plugging it in to your computer using a USB cable and following the instructions [here](docs/running-on-device.html).

### Using a virtual device

You can see the list of available Android Virtual Devices (AVDs) by opening the "AVD Manager" from within Android Studio. Look for an icon that looks like this:

![Android Studio AVD Manager](img/react-native-tools-avd.png)

If you have just installed Android Studio, you will likely need to [create a new AVD](https://developer.android.com/studio/run/managing-avds.html). Select "Create Virtual Device...", then pick any Phone from the list and click "Next".

<block class="native windows android" />

![Android Studio AVD Manager](img/CreateAVDWindows.png)

<block class="native mac android" />

![Android Studio AVD Manager](img/CreateAVDMacOS.png)

<block class="native mac windows linux android" />

Select the "x86 Images" tab, then look for the **Marshmallow** API Level 23, x86_64 ABI image with a Android 6.0 (Google APIs) target.

<block class="native linux android" />

> We recommend configuring [VM acceleration](https://developer.android.com/studio/run/emulator-acceleration.html#vm-linux) on your system to improve performance. Once you've followed those instructions, go back to the AVD Manager.

<block class="native windows android" />

![Install HAXM](img/CreateAVDx86Windows.png)

> If you don't have HAXM installed, click on "Install HAXM" or follow [these instructions](https://software.intel.com/en-us/android/articles/installation-instructions-for-intel-hardware-accelerated-execution-manager-windows) to set it up, then go back to the AVD Manager.

![AVD List](img/AVDManagerWindows.png)

<block class="native mac android" />

![Install HAXM](img/CreateAVDx86MacOS.png)

> If you don't have HAXM installed, follow [these instructions](https://software.intel.com/en-us/android/articles/installation-instructions-for-intel-hardware-accelerated-execution-manager-mac-os-x) to set it up, then go back to the AVD Manager.

![AVD List](img/AVDManagerMacOS.png)

<block class="native mac windows linux android" />

Click "Next" then "Finish" to create your AVD. At this point you should be able to click on the green triangle button next to your AVD to launch it, then proceed to the next step.

<block class="native mac ios" />

## Running your React Native application

Run `react-native run-ios` inside your React Native project folder:

```
cd AwesomeProject
react-native run-ios
```

You should see your new app running in the iOS Simulator shortly.

![AwesomeProject on iOS](img/iOSSuccess.png)

`react-native run-ios` is just one way to run your app. You can also run it directly from within Xcode or [Nuclide](https://nuclide.io/).

> If you can't get this to work, see the [Troubleshooting](docs/troubleshooting.html#content) page.

### Running on a device

The above command will automatically run your app on the iOS Simulator by default. If you want to run the app on an actual physical iOS device, please follow the instructions [here](docs/running-on-device.html).

<block class="native mac windows linux android" />

## Running your React Native application

Run `react-native run-android` inside your React Native project folder:

```
cd AwesomeProject
react-native run-android
```

If everything is set up correctly, you should see your new app running in your Android emulator shortly.

<block class="native mac android" />

![AwesomeProject on Android](img/AndroidSuccessMacOS.png)

<block class="native windows android" />

![AwesomeProject on Android](img/AndroidSuccessWindows.png)

<block class="native mac windows linux android" />

`react-native run-android` is just one way to run your app - you can also run it directly from within Android Studio or [Nuclide](https://nuclide.io/).

> If you can't get this to work, see the [Troubleshooting](docs/troubleshooting.html#content) page.

<block class="native mac ios android" />

### Modifying your app

Now that you have successfully run the app, let's modify it.

<block class="native mac ios" />

- Open `index.ios.js` in your text editor of choice and edit some lines.
- Hit `⌘R` in your iOS Simulator to reload the app and see your changes!

<block class="native mac android" />

- Open `index.android.js` in your text editor of choice and edit some lines.
- Press the `R` key twice or select `Reload` from the Developer Menu (`⌘M`) to see your changes!

<block class="native windows linux android" />

### Modifying your app

Now that you have successfully run the app, let's modify it.

- Open `index.android.js` in your text editor of choice and edit some lines.
- Press the `R` key twice or select `Reload` from the Developer Menu (`⌘M`) to see your changes!

<block class="native mac ios android" />

### That's it!

Congratulations! You've successfully run and modified your first React Native app.

<center><img src="img/react-native-congratulations.png" width="150"></img></center>

<block class="native windows linux android" />

### That's it!

Congratulations! You've successfully run and modified your first React Native app.

<center><img src="img/react-native-congratulations.png" width="150"></img></center>

<block class="native mac ios" />

## Now what?

- Turn on [Live Reload](docs/debugging.html#reloading-javascript) in the Developer Menu. Your app will now reload automatically whenever you save any changes!

- If you want to add this new React Native code to an existing application, check out the [Integration guide](docs/integration-with-existing-apps.html).

If you're curious to learn more about React Native, continue on
to the [Tutorial](docs/tutorial.html).

<block class="native windows linux mac android" />

## Now what?

- Turn on [Live Reload](docs/debugging.html#reloading-javascript) in the Developer Menu. Your app will now reload automatically whenever you save any changes!

- If you want to add this new React Native code to an existing application, check out the [Integration guide](docs/integration-with-existing-apps.html).

If you're curious to learn more about React Native, continue on
to the [Tutorial](docs/tutorial.html).


<script>
function displayTab(type, value) {
  var container = document.getElementsByTagName('block')[0].parentNode;
  container.className = 'display-' + type + '-' + value + ' ' +
    container.className.replace(RegExp('display-' + type + '-[a-z]+ ?'), '');
  event && event.preventDefault();
}
</script>
