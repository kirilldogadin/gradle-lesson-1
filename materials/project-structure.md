# Структура проекта Gradle

Понимание структуры проекта Gradle является ключевым для эффективной работы с этой системой сборки. В этом документе рассмотрены основные элементы структуры Gradle-проекта.

## Базовая структура проекта

Типичный Gradle-проект имеет следующую структуру:

```
project-root/
├── build.gradle        # Основной файл конфигурации сборки
├── settings.gradle     # Настройки проекта, определение подпроектов
├── gradle/
│   └── wrapper/        # Файлы Gradle Wrapper
│       ├── gradle-wrapper.jar
│       └── gradle-wrapper.properties
├── gradlew             # Скрипт запуска Gradle Wrapper для Unix
├── gradlew.bat         # Скрипт запуска Gradle Wrapper для Windows
├── src/                # Исходный код
│   ├── main/           # Основной код
│   │   ├── java/       # Java-код
│   │   ├── kotlin/     # Kotlin-код (если используется)
│   │   └── resources/  # Ресурсы
│   └── test/           # Тестовый код
│       ├── java/       # Java-тесты
│       ├── kotlin/     # Kotlin-тесты (если используется)
│       └── resources/  # Тестовые ресурсы
└── build/              # Директория с результатами сборки (создается автоматически)
```

## Ключевые файлы и директории

### build.gradle

Основной файл конфигурации сборки, который содержит:
- Плагины
- Репозитории для зависимостей
- Зависимости проекта
- Настройки компиляции
- Задачи (tasks)
- Другие настройки проекта

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

### settings.gradle

Файл настроек проекта, который определяет:
- Имя проекта
- Включенные подпроекты (для многомодульных проектов)

Пример `settings.gradle`:

```groovy
rootProject.name = 'my-gradle-project'
include 'core', 'api', 'web'
```

### gradle/wrapper

Директория с файлами Gradle Wrapper:
- `gradle-wrapper.jar` — JAR-файл, который скачивает и запускает Gradle
- `gradle-wrapper.properties` — настройки Wrapper, включая версию Gradle

Пример `gradle-wrapper.properties`:

```properties
distributionBase=GRADLE_USER_HOME
distributionPath=wrapper/dists
distributionUrl=https\://services.gradle.org/distributions/gradle-8.2-bin.zip
zipStoreBase=GRADLE_USER_HOME
zipStorePath=wrapper/dists
```

### gradlew и gradlew.bat

Скрипты для запуска Gradle Wrapper:
- `gradlew` — для Unix-подобных систем (Linux, macOS)
- `gradlew.bat` — для Windows

### src

Директория с исходным кодом проекта:
- `src/main/java` — основной Java-код
- `src/main/resources` — ресурсы (конфигурационные файлы, изображения и т.д.)
- `src/test/java` — тестовый Java-код
- `src/test/resources` — ресурсы для тестов

### build

Директория с результатами сборки (создается автоматически):
- `build/classes` — скомпилированные классы
- `build/libs` — собранные JAR/WAR файлы
- `build/reports` — отчеты (тесты, анализ кода)
- `build/tmp` — временные файлы
- `build/resources` — обработанные ресурсы

## Многомодульные проекты

Для многомодульных проектов структура выглядит следующим образом:

```
project-root/
├── build.gradle        # Корневой build.gradle
├── settings.gradle     # Определение подпроектов
├── gradle/wrapper/     # Файлы Gradle Wrapper
├── module1/
│   ├── build.gradle    # build.gradle для module1
│   └── src/            # Исходный код module1
├── module2/
│   ├── build.gradle    # build.gradle для module2
│   └── src/            # Исходный код module2
└── module3/
    ├── build.gradle    # build.gradle для module3
    └── src/            # Исходный код module3
```

## Конвенции и соглашения

Gradle следует принципу "соглашение превыше конфигурации" (convention over configuration), что означает:
- Стандартная структура проекта предопределена
- Большинство настроек имеют разумные значения по умолчанию
- Конфигурация требуется только для нестандартных случаев

Это упрощает работу с проектами и делает их более понятными для новых разработчиков.

## Заключение

Понимание структуры проекта Gradle является фундаментальным для эффективной работы с этой системой сборки. Стандартная структура обеспечивает организованный подход к разработке и упрощает понимание проекта для всех участников команды.
