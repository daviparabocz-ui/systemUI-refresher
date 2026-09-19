# SystemUI Refresh

App mínimo: ao abrir, mata o processo `com.android.systemui` via `su` e fecha sozinho
(sem tela visível, só um toast). Como é um processo persistente do framework,
o `system_server` reinicia ele automaticamente — na prática funciona como um
"refresh" da SystemUI.

## Por que não veio um .apk pronto

Este ambiente não tem acesso ao repositório Maven do Google (`dl.google.com`),
que o Android Gradle Plugin precisa para compilar — por isso só dá pra gerar o
código-fonte aqui, não o APK final. Com seu setup de build de AOSP/Termux isso
deve compilar sem drama.

## Build

Abrindo no Android Studio:
1. `File > Open` nesta pasta — ele gera o `gradlew` sozinho.
2. `Build > Build Bundle(s) / APK(s) > Build APK(s)`.

Via linha de comando (se já tiver o wrapper ou o Gradle instalado):
```
gradle wrapper          # gera o gradlew, se não existir
./gradlew assembleDebug
```
O APK sai em `app/build/outputs/apk/debug/app-debug.apk`.

## Uso

Instala, abre o ícone "SystemUI Refresh", aceita o pedido de root na primeira vez
(Magisk/SuperSU) e pronto — cada toque reinicia a SystemUI.

Se quiser sem ícone/launcher, dá pra disparar direto por ADB depois de instalado:
```
adb shell am start -n com.davi.systemuirefresh/.MainActivity
```
