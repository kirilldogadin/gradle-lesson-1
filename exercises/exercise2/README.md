# Упражнение 2: Изучение структуры build.gradle

## Цель
Понять основные компоненты файла build.gradle и их назначение через практическое применение.

## Необходимые инструменты
- Проект, созданный в Упражнении 1
- Текстовый редактор

## Шаги выполнения

### 1. Открытие файла build.gradle
Откройте файл `build.gradle` в текстовом редакторе. Если вы не выполнили Упражнение 1, вы можете использовать шаблон файла из этой директории.

### 2. Анализ основных секций

Найдите и изучите следующие секции:

#### Секция plugins
```groovy
plugins {
    id 'application'
    id 'java'
}
```
Эта секция определяет, какие плагины используются в проекте. Плагины добавляют функциональность в ваш проект.

#### Секция repositories
```groovy
repositories {
    mavenCentral()
}
```
Эта секция указывает, откуда Gradle будет загружать зависимости.

#### Секция dependencies
```groovy
dependencies {
    implementation 'com.google.guava:guava:31.1-jre'
    testImplementation 'junit:junit:4.13.2'
}
```
Эта секция определяет зависимости проекта.

#### Секция application
```groovy
application {
    mainClass = 'com.example.App'
}
```
Эта секция содержит настройки для плагина application.

### 3. Практическое изменение конфигурации

Внесите следующие изменения в файл build.gradle и проанализируйте их влияние:

#### 3.1. Добавление нового репозитория

Добавьте репозиторий Google в секцию repositories:

```groovy
repositories {
    mavenCentral()
    google()
}
```

#### 3.2. Добавление новых зависимостей

Добавьте несколько новых зависимостей разных типов:

```groovy
dependencies {
    implementation 'com.google.guava:guava:31.1-jre'
    implementation 'org.apache.commons:commons-lang3:3.12.0'
    
    // Зависимость только для компиляции
    compileOnly 'org.projectlombok:lombok:1.18.24'
    
    // Зависимость только для выполнения
    runtimeOnly 'org.slf4j:slf4j-simple:2.0.5'
    
    testImplementation 'junit:junit:4.13.2'
}
```

#### 3.3. Настройка версии Java

Добавьте настройки для версии Java:

```groovy
java {
    sourceCompatibility = JavaVersion.VERSION_11
    targetCompatibility = JavaVersion.VERSION_11
}
```

#### 3.4. Создание собственной задачи

Добавьте простую задачу, которая выводит информацию о проекте:

```groovy
task projectInfo {
    description 'Displays information about the project'
    group 'Help'
    
    doLast {
        println "Project: ${project.name}"
        println "Version: ${project.version ?: 'Not specified'}"
        println "Java compatibility: ${java.sourceCompatibility}"
        println "Dependencies:"
        configurations.implementation.dependencies.each {
            println "  - ${it.group}:${it.name}:${it.version}"
        }
    }
}
```

### 4. Проверка изменений

Выполните следующие команды для проверки внесенных изменений:

```bash
# Просмотр доступных задач
./gradlew tasks

# Запуск созданной задачи
./gradlew projectInfo

# Сборка проекта с новыми зависимостями
./gradlew build
```

### 5. Анализ результатов

Проанализируйте результаты выполнения команд:
- Какие новые задачи появились после добавления плагинов?
- Как изменился вывод команды `./gradlew tasks` после добавления собственной задачи?
- Какие файлы были созданы в директории `build/` после сборки проекта?

## Вопросы для обсуждения

1. На что похожа структура файла build.gradle?
2. Почему Gradle использует код на Groovy/Kotlin вместо XML (как в Maven)?
3. Какие преимущества даёт программный подход к конфигурации сборки?
4. Как вы думаете, что произойдет, если удалить секцию repositories?
5. В чем разница между зависимостями типа `implementation`, `compileOnly` и `runtimeOnly`?

## Связь с уроком

Это упражнение демонстрирует:
- Структуру файла build.gradle
- Основные секции конфигурации Gradle
- Как модифицировать конфигурацию сборки
- Создание собственных задач

## Дополнительные задания

1. Добавьте плагин для проверки стиля кода (например, Checkstyle)
2. Настройте проект для создания исполняемого JAR-файла с зависимостями
3. Создайте задачу, которая генерирует текстовый файл с информацией о проекте

## Следующий шаг

После выполнения этого упражнения переходите к [Упражнению 3: Обновление Gradle Wrapper](../exercise3/README.md)
