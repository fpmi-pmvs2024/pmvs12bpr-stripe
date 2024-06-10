<h1 align="center">ToDoCompose</h1>

<p align="center">  
🗡️ ToDoApp demonstrates modern Android development with Hilt, Coroutines, Flow, Jetpack (Room, ViewModel), and Material Design based on MVVM architecture.
</p>
</br>

<p align="center">
<img src="https://user-images.githubusercontent.com/4821464/216806197-48c4f8bc-bf33-4816-9860-6825cc7ff6d7.png"/>
<img src="https://user-images.githubusercontent.com/4821464/216806201-cd683b6a-c86e-4d66-9d71-b12ee78d96f5.png"/>
</p>

## Цели лабораторной работы
- Выбрать предметную область и сформулировать постановку задачи для реализации мобильного приложения.
- Разработать приложение, состоящее из нескольких фрагментов и/или активностей (если необходимо), реализующего многооконный интерфейс, элементы тач-интерфейса, хранение данных в базе данных, многопоточность, взаимодействие с внешними API.
- Для построения интерфейса приложения желательно использовать библиотеку Jetpack Compose.
- Для хранения данных рекомендуется база данных SQLite или Room. Если в проекте требуется документоориентированная база данных, то рекомендуется Realm.

## Задачи лабораторной работы
- Разработать собственное приложение с применением функционала, изученного в рамках курса ПВМС.
- Распределить работы между участниками группы и управлять проектом разработки, используя Github Projects.
- Для контроля версий использовать git, разместив проект на GitHub в репозитории для команды.
- Документировать проект в Readme, wiki репозитория и GitHub Pages согласно требованиям, представленным ниже.
- Непрерывная сборка проекта с помощью GitHub Actions, которая включает выполнение автоматических тестов.
- Настроить unit-тесты и UI-тесты с помощью локальных библиотек или Firebase Test Lab и реализовать их вызов в рабочем процессе GitHub Actions.
- Для непрерывной сборки может быть использован контейнер Docker с эмулятором Android.

## Tech stack & Open-source libraries
- Minimum SDK level 21
- [Kotlin](https://kotlinlang.org/) based, [Coroutines](https://github.com/Kotlin/kotlinx.coroutines) + [Flow](https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.flow/) for asynchronous.
- Jetpack
  - Lifecycle: Observe Android lifecycles and handle UI states upon the lifecycle changes.
  - ViewModel: Manages UI-related data holder and lifecycle aware. Allows data to survive configuration changes such as screen rotations.
  - Room: Constructs Database by providing an abstraction layer over SQLite to allow fluent database access.
  - [Hilt](https://dagger.dev/hilt/): for dependency injection.
  - [Jetpack Compose](https://developer.android.com/jetpack/compose?hl=es-419) <img align="right" width="130px" src="https://user-images.githubusercontent.com/24237865/210227682-cbc03479-8625-4213-b907-4f15217f91ba.png"/>
- Architecture
  - MVVM Architecture (View - ViewModel - Model)
  - Repository Pattern
- [Retrofit2 & OkHttp3](https://github.com/square/retrofit): Construct the REST APIs and paging network data.
- [Material-Components](https://github.com/material-components/material-components-android): Material design components for building ripple animation, and CardView.
- [Glide](https://github.com/bumptech/glide), [GlidePalette](https://github.com/florent37/GlidePalette): Loading images from network.

## Architecture
**ToDoApp** is based on the MVVM architecture and the Repository pattern, which follows the [Google's official architecture guidance](https://developer.android.com/topic/architecture).

<img align="right" width="630px" src="https://user-images.githubusercontent.com/4821464/217079002-f0ecb824-7672-4c30-ac67-02d2082ad5e9.jpg"/>

The overall architecture of **ToDoApp** is composed of two layers; the UI layer and the data layer. Each layer has dedicated components and they have each different responsibilities, as defined below:

**ToDoApp** was built with [Guide to app architecture](https://developer.android.com/topic/architecture), so it would be a great sample to show how the architecture works in real-world projects.

### Architecture Overview

- Each layer follows [unidirectional event/data flow](https://developer.android.com/topic/architecture/ui-layer#udf); the UI layer emits user events to the data layer, and the data layer exposes data as a stream to other layers.
- The data layer is designed to work independently from other layers and must be pure, which means it doesn't have any dependencies on the other layers.

With this loosely coupled architecture, you can increase the reusability of components and scalability of your app.
</br></br></br>

### UI Layer

<img align="right" width="330px" src="https://user-images.githubusercontent.com/4821464/216807573-2ecd44c9-6f3e-4bc3-8b9c-04b7d938f028.png"/>

The UI layer consists of UI elements to configure screens that could interact with users and [ViewModel](https://developer.android.com/topic/libraries/architecture/viewmodel) that holds app states and restores data when configuration changes.
- UI elements observe the data flow, which is the most essential part of the MVVM architecture. 

### Data Layer

<img align="right" width="330px" src="https://user-images.githubusercontent.com/4821464/216807578-d55ceb6f-4730-491e-9e2f-0924f7e94153.png"/>

The data Layer consists of repositories, which include business logic, such as querying data from the local database. 

**ToDoApp** is an offline-first app that is able to perform all, or a critical subset of its core functionality without access to the internet. 
So users don't need to be up-to-date on the network resources every time and it will decrease users' data consumption. For further information, you can check out [Build an offline-first app](https://developer.android.com/topic/architecture/data-layer/offline-first).

## Документирование проекта

### Распределение работ
- Артем: Основная архитектура приложения, создание базы данных. Настройка и интеграция GitHub Actions для непрерывной сборки и тестирования.
- Дима: Разработка пользовательского интерфейса с использованием Jetpack Compose. Написание unit-тестов и UI-тестов.

### Контроль версий
Для контроля версий используется git. Проект размещен в репозитории на GitHub. Все изменения проходят через пулреквесты с обязательным код-ревью.

### Непрерывная интеграция
Для непрерывной интеграции настроены GitHub Actions, которые включают автоматическую сборку и тестирование проекта при каждом пуше в основную ветку.

#### Пример workflow файла для GitHub Actions
```yaml
name: Android CI

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout code
      uses: actions/checkout@v2

    - name: Set up JDK 11
      uses: actions/setup-java@v2
      with:
        distribution: 'adopt'
        java-version: '11'

    - name: Grant execute permission for gradlew
      run: chmod +x gradlew

    - name: Build with Gradle
      run: ./gradlew build

    - name: Run unit tests
      run: ./gradlew test

    - name: Run UI tests
      run: ./gradlew connectedAndroidTest
```

### Unit-тесты и UI-тесты
Настроены unit-тесты и UI-тесты с помощью JUnit и Espresso. Тесты автоматически запускаются при сборке проекта с помощью GitHub Actions.

### Пример Dockerfile для Android эмулятора
```dockerfile
FROM ubuntu:20.04

LABEL maintainer="your_email@example.com"

ENV DEBIAN_FRONTEND=noninteractive
ENV ANDROID_SDK_ROOT=/sdk
ENV PATH=$PATH:$ANDROID_SDK_ROOT/tools:$ANDROID_SDK_ROOT/platform-tools:$ANDROID_SDK_ROOT/emulator

# Установка необходимых пакетов
RUN apt-get update && apt-get install -y --no-install-recommends \
    unzip \
    openjdk-11-jdk \
    wget \
    && rm -rf /var/lib/apt/lists/*

# Установка Android SDK
RUN mkdir /sdk
RUN wget https://dl.google.com/android/repository/commandlinetools-linux-6609375_latest.zip -O cmdline-tools.zip
RUN unzip cmdline-tools.zip -d /sdk && rm cmdline-tools.zip
RUN mkdir -p /sdk/cmdline-tools/latest
RUN mv /sdk/cmdline-tools/* /sdk/cmdline-tools/latest/

# Установка необходимых SDK инструментов
RUN yes | sdkmanager --licenses
RUN sdkmanager --update
RUN sdkmanager "platform-tools" "platforms;android-30" "

build-tools;30.0.3" "emulator"

# Настройка эмулятора
RUN sdkmanager "system-images;android-30;google_apis;x86_64"
RUN echo "no" | avdmanager create avd -n test -k "system-images;android-30;google_apis;x86_64"

EXPOSE 5554 5555

CMD /sdk/emulator/emulator -avd test -no-window -no-audio -no-boot-anim -gpu off
```

## Лицензия
Этот проект лицензирован под лицензией MIT.

