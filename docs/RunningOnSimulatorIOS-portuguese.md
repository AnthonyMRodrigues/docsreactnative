---
id: running-on-simulator-ios
title: Running On Simulator
layout: docs
category: Guides (iOS)
permalink: docs/running-on-simulator-ios.html
banner: ejected
next: communication-ios
previous: linking-libraries-ios
---

## Iniciando o simulador

Tão logo tenha iniciado o seu projeto em React Native, você já pode executar `react-native run-ios` dentro do diretório do projeto recém-criado. Se tudo estiver configurado corretamente, você deve de ver o seu novo app rodando no iOS Simulator logo em breve.

## Especificando um dispositivo

Você pode especificar o dispositivo que o simulador deveria rodar com a flag `--simulator`, seguido pelo nome do dispositivo como um string. O default é `"iPhone 6"`. Se você desejar rodar o seu app num iPhone 4s, apenas execute `react-native run-ios --simulator="iPhone 4s"`.

Os nomes de dispositivo correspondem à lista de dispositivos disponíveis no Xcode. Você pode verificar os seus dispositivos disponíveis ao executar `xcrun simctl list devices` a partir do console.
