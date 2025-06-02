# GROOVY УРОК 1: Основы Gradle и структура проекта

## Введение в Gradle

Gradle — это современная система автоматизации сборки, которая объединяет лучшие практики из других систем сборки и предлагает гибкий подход на основе Groovy или Kotlin DSL.

### Что такое система сборки?

Система сборки — это инструмент, который автоматизирует процесс создания исполняемого приложения из исходного кода. Этот процесс включает:

- Компиляцию исходного кода
- Связывание с зависимостями
- Тестирование
- Упаковку в исполняемые файлы (JAR, WAR и т.д.)
- Развертывание

### Почему Gradle?

Gradle объединяет гибкость Ant с мощными возможностями управления зависимостями Maven, добавляя:

- **Декларативный подход** — описание того, что нужно сделать, а не как
- **Программируемость** — использование полноценного языка программирования (Groovy/Kotlin)
- **Инкрементальные сборки** — выполнение только необходимых задач
- **Управление зависимостями** — автоматическое разрешение и загрузка зависимостей
- **Расширяемость** — богатая экосистема плагинов и возможность создания собственных

### Сравнение с другими системами сборки

| Характеристика | Ant | Maven | Gradle |
|----------------|-----|-------|--------|
| Язык конфигурации | XML | XML | Groovy/Kotlin DSL |
| Управление зависимостями | Нет (требует Ivy) | Да | Да |
| Конвенции | Нет | Да | Да, но гибкие |
| Расширяемость | Сложная | Через плагины | Через плагины и скрипты |
| Инкрементальные сборки | Ограниченные | Ограниченные | Продвинутые |
| Параллельное выполнение | Нет | Ограниченное | Да |

## Установка Gradle и Gradle Wrapper

### Первоначальная установка Gradle vs Gradle Wrapper: разрешение противоречия

В мире Gradle существует важный нюанс, который может вызвать путаницу у новичков: **мы рекомендуем всегда использовать Gradle Wrapper (gradlew), но для его первоначального создания нужен установленный Gradle**.

Давайте разберемся с этой "проблемой курицы и яйца":

#### Правильная последовательность действий:

1. **Первоначальная установка Gradle** (выполняется только один раз):
   - Установите Gradle локально одним из способов, описанных ниже
   - Это единственный случай, когда вам понадобится глобальная установка Gradle

2. **Создание Gradle Wrapper** (для каждого проекта):
   - После установки Gradle выполните в корне проекта:
   ```bash
   gradle wrapper
   ```
   - Эта команда создаст файлы Gradle Wrapper (gradlew, gradlew.bat и директорию gradle/wrapper)

3. **Дальнейшее использование** (всегда):
   - После создания Wrapper, всегда используйте `./gradlew` вместо `gradle`
   - Добавьте файлы Wrapper в систему контроля версий
   - Другим разработчикам и CI-системам не потребуется устанавливать Gradle

#### Альтернативные способы получения Gradle Wrapper (без установки Gradle):

Если вы не хотите устанавливать Gradle даже для первоначального создания Wrapper, есть альтернативные подходы:

1. **Использование генераторов проектов**:
   - [Spring Initializr](https://start.spring.io/) - для Spring проектов
   - [IntelliJ IDEA](https://www.jetbrains.com/idea/) - при создании нового Gradle проекта
   - [Android Studio](https://developer.android.com/studio) - для Android проектов

2. **Клонирование существующего проекта с Wrapper**:
   - Клонируйте любой открытый проект с Gradle Wrapper
   - Скопируйте файлы Wrapper в свой проект
   - Обновите версию Gradle при необходимости: `./gradlew wrapper --gradle-version=8.2`

### Требования

- JDK 8 или выше
- Переменная окружения JAVA_HOME

### Способы установки Gradle

#### 1. Ручная установка

1. Скачайте последнюю версию с [официального сайта](https://gradle.org/releases/)
2. Распакуйте архив
3. Добавьте путь к директории `bin` в переменную PATH

#### 2. SDKMAN (Linux/macOS)

```bash
sdk install gradle
```

#### 3. Homebrew (macOS)

```bash
brew install gradle
```

#### 4. Chocolatey (Windows)

```bash
choco install gradle
```

### Проверка установки

```bash
gradle --version
```

## Gradle Wrapper

Gradle Wrapper — это рекомендуемый способ запуска Gradle. Он позволяет запускать Gradle без предварительной установки.

### Преимущества Wrapper

- Гарантирует использование одной и той же версии Gradle всеми разработчиками
- Упрощает настройку CI/CD
- Не требует предварительной установки Gradle

### Структура Wrapper

- `gradle/wrapper/gradle-wrapper.jar` — JAR-файл для скачивания Gradle
- `gradle/wrapper/gradle-wrapper.properties` — настройки Wrapper
- `gradlew` — скрипт для Unix-подобных систем
- `gradlew.bat` — скрипт для Windows

### Создание Wrapper

```bash
gradle wrapper
```

### Использование Wrapper

```bash
./gradlew build  # Unix-подобные системы
gradlew.bat build  # Windows
```

### Обновление версии Gradle в Wrapper

```bash
./gradlew wrapper --gradle-version=8.2
```

## Структура проекта Gradle

### Базовая структура

```
project-root/
├── build.gradle        # Скрипт сборки
├── settings.gradle     # Настройки проекта
├── gradle/             # Директория для Gradle Wrapper
│   └── wrapper/
│       ├── gradle-wrapper.jar
│       └── gradle-wrapper.properties
├── gradlew             # Скрипт Gradle Wrapper для Unix
├── gradlew.bat         # Скрипт Gradle Wrapper для Windows
├── src/                # Исходный код
│   ├── main/           # Основной код
│   │   ├── java/       # Java-код
│   │   ├── resources/  # Ресурсы
│   │   └── groovy/     # Groovy-код (опционально)
│   └── test/           # Тестовый код
│       ├── java/       # Java-тесты
│       ├── resources/  # Тестовые ресурсы
│       └── groovy/     # Groovy-тесты (опционально)
└── build/              # Директория для сборки (создается автоматически)
```

### Конвенции

Gradle использует конвенции для упрощения конфигурации:

- Исходный код в `src/main/java`
- Тесты в `src/test/java`
- Ресурсы в `src/main/resources`
- Результаты сборки в `build/`

### Файл build.gradle

Основной файл конфигурации проекта, содержащий:

- Плагины
- Репозитории
- Зависимости
- Задачи
- Настройки

Пример простого `build.gradle`:

```groovy
plugins {
    id 'java'
    id 'application'
}

repositories {
    mavenCentral()
}

dependencies {
    implementation 'com.google.guava:guava:31.1-jre'
    testImplementation 'junit:junit:4.13.2'
}

application {
    mainClass = 'com.example.App'
}
```

### Файл settings.gradle

Определяет настройки проекта, включая:

- Имя проекта
- Включенные подпроекты (для многомодульных проектов)

Пример `settings.gradle`:

```groovy
rootProject.name = 'my-gradle-project'
```

## Жизненный цикл сборки Gradle

### Три фазы сборки

1. **Инициализация** — определение проектов для сборки
2. **Конфигурация** — создание и настройка объектов задач
3. **Выполнение** — запуск выбранных задач

### Задачи (Tasks)

Задачи — это основные единицы работы в Gradle. Каждая задача представляет собой атомарную часть работы.

#### Анатомия задачи

- Имя
- Действия (actions)
- Входные данные (inputs)
- Выходные данные (outputs)
- Зависимости (dependencies)

#### Создание задачи

```groovy
task hello {
    description 'Prints a greeting'
    group 'Custom'
    
    doLast {
        println 'Hello, Gradle!'
    }
}
```

#### Зависимости между задачами

```groovy
task taskA {
    doLast {
        println 'Task A'
    }
}

task taskB {
    dependsOn taskA
    doLast {
        println 'Task B'
    }
}
```

#### Стандартные задачи

- `build` — собирает проект
- `clean` — удаляет директорию сборки
- `test` — запускает тесты
- `assemble` — собирает артефакты
- `check` — запускает проверки
- `jar` — создает JAR-файл

## Управление зависимостями

### Репозитории

Репозитории — это источники зависимостей. Gradle поддерживает различные типы репозиториев:

```groovy
repositories {
    mavenCentral()
    google()
    jcenter()
    maven {
        url "https://repo.spring.io/release"
    }
}
```

### Конфигурации зависимостей

Конфигурации определяют, как зависимости используются в проекте:

- `implementation` — зависимости для компиляции и выполнения
- `compileOnly` — зависимости только для компиляции
- `runtimeOnly` — зависимости только для выполнения
- `testImplementation` — зависимости для тестов

```groovy
dependencies {
    implementation 'com.google.guava:guava:31.1-jre'
    compileOnly 'org.projectlombok:lombok:1.18.24'
    runtimeOnly 'org.slf4j:slf4j-simple:2.0.5'
    testImplementation 'junit:junit:4.13.2'
}
```

### Транзитивные зависимости

Gradle автоматически разрешает транзитивные зависимости. Можно управлять ими:

```groovy
dependencies {
    implementation('com.example:library:1.0') {
        exclude group: 'org.unwanted', module: 'module'
    }
}
```

### Разрешение конфликтов версий

По умолчанию Gradle выбирает наибольшую версию. Можно переопределить это поведение:

```groovy
configurations.all {
    resolutionStrategy {
        force 'com.google.guava:guava:31.1-jre'
    }
}
```

## Плагины

Плагины расширяют функциональность Gradle, добавляя задачи, конфигурации и конвенции.

### Типы плагинов

- **Встроенные плагины** — поставляются с Gradle
- **Плагины из Gradle Plugin Portal** — сторонние плагины
- **Пользовательские плагины** — созданные разработчиками

### Применение плагинов

#### Декларативный синтаксис (рекомендуется)

```groovy
plugins {
    id 'java'
    id 'org.springframework.boot' version '3.0.0'
}
```

#### Императивный синтаксис (устаревший)

```groovy
apply plugin: 'java'
```

### Популярные плагины

- `java` — добавляет поддержку Java
- `application` — для запускаемых приложений
- `war` — для веб-приложений
- `spring-boot` — для Spring Boot приложений
- `kotlin` — для Kotlin-проектов

## Понятие classpath

Classpath — это параметр, который указывает JVM, где искать классы и ресурсы.

### Типы classpath в Gradle

- **Compile classpath** — для компиляции исходного кода
- **Runtime classpath** — для выполнения программы
- **Test compile classpath** — для компиляции тестов
- **Test runtime classpath** — для выполнения тестов

### Просмотр classpath

```groovy
task printClasspath {
    doLast {
        println "Compile classpath:"
        configurations.compileClasspath.each { println it }
    }
}
```

## Практические примеры

### Пример 1: Простое Java-приложение

```groovy
plugins {
    id 'java'
    id 'application'
}

repositories {
    mavenCentral()
}

dependencies {
    implementation 'com.google.guava:guava:31.1-jre'
    testImplementation 'junit:junit:4.13.2'
}

application {
    mainClass = 'com.example.App'
}
```

### Пример 2: Настройка версии Java

```groovy
plugins {
    id 'java'
}

java {
    sourceCompatibility = JavaVersion.VERSION_11
    targetCompatibility = JavaVersion.VERSION_11
}
```

### Пример 3: Создание собственной задачи

```groovy
task createFile {
    description 'Creates a file with current timestamp'
    group 'Custom'
    
    def destFile = file("$buildDir/generated/timestamp.txt")
    
    inputs.property 'timestamp', System.currentTimeMillis()
    outputs.file destFile
    
    doLast {
        destFile.parentFile.mkdirs()
        destFile.text = "File created on: ${new Date()}"
    }
}
```

## Лучшие практики

1. **Всегда используйте Gradle Wrapper**
   - Включайте его в систему контроля версий
   - Используйте `./gradlew` вместо `gradle`
   - Помните, что для первоначального создания Wrapper нужен установленный Gradle или генератор проектов

2. **Следуйте конвенциям**
   - Размещайте код в стандартных директориях
   - Используйте стандартные задачи

3. **Управляйте зависимостями правильно**
   - Используйте `implementation` вместо `compile`
   - Указывайте версии зависимостей

4. **Оптимизируйте сборки**
   - Используйте кэширование
   - Включайте параллельное выполнение

5. **Документируйте сборки**
   - Добавляйте описания к задачам
   - Группируйте задачи

## Заключение

Gradle — это мощная и гибкая система сборки, которая объединяет лучшие практики из других систем и предлагает программируемый подход к автоматизации сборки. Понимание основ Gradle и структуры проекта является фундаментом для эффективной работы с этим инструментом.

## Дополнительные ресурсы

- [Официальная документация Gradle](https://docs.gradle.org/)
- [Руководство по Gradle для начинающих](https://gradle.org/guides/#getting-started)
- [Gradle Wrapper](https://docs.gradle.org/current/userguide/gradle_wrapper.html)
- [Управление зависимостями в Gradle](https://docs.gradle.org/current/userguide/dependency_management.html)
