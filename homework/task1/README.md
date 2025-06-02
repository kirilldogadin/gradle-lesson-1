# Задание 1: Создание многомодульного проекта

## Цель
Научиться создавать и настраивать многомодульные проекты в Gradle.

## Задание

Создайте Gradle-проект с двумя модулями:
- `core` — содержит базовую функциональность
- `app` — использует функциональность из модуля `core`

### Шаги выполнения

1. Создайте корневую директорию проекта:
   ```bash
   mkdir gradle-multimodule
   cd gradle-multimodule
   ```

2. Инициализируйте Gradle-проект:
   ```bash
   gradle init --type basic
   ```

3. Создайте директории для модулей:
   ```bash
   mkdir -p core/src/main/java/com/example/core
   mkdir -p core/src/test/java/com/example/core
   mkdir -p app/src/main/java/com/example/app
   mkdir -p app/src/test/java/com/example/app
   ```

4. Создайте файл `settings.gradle` в корневой директории:
   ```groovy
   rootProject.name = 'gradle-multimodule'
   include 'core', 'app'
   ```

5. Создайте файл `build.gradle` в корневой директории:
   ```groovy
   plugins {
       id 'java'
   }

   allprojects {
       repositories {
           mavenCentral()
       }
   }

   subprojects {
       apply plugin: 'java'
       
       sourceCompatibility = '11'
       targetCompatibility = '11'
       
       dependencies {
           testImplementation 'junit:junit:4.13.2'
       }
   }
   ```

6. Создайте файл `core/build.gradle`:
   ```groovy
   dependencies {
       implementation 'org.apache.commons:commons-lang3:3.12.0'
   }
   ```

7. Создайте файл `app/build.gradle`:
   ```groovy
   plugins {
       id 'application'
   }

   dependencies {
       implementation project(':core')
   }

   application {
       mainClass = 'com.example.app.App'
   }
   ```

8. Создайте класс `StringUtils` в модуле `core`:
   ```java
   // core/src/main/java/com/example/core/StringUtils.java
   package com.example.core;

   public class StringUtils {
       public static String reverse(String input) {
           if (input == null) {
               return null;
           }
           return new StringBuilder(input).reverse().toString();
       }
   }
   ```

9. Создайте класс `App` в модуле `app`:
   ```java
   // app/src/main/java/com/example/app/App.java
   package com.example.app;

   import com.example.core.StringUtils;

   public class App {
       public static void main(String[] args) {
           String original = "Hello, Gradle!";
           String reversed = StringUtils.reverse(original);
           
           System.out.println("Original: " + original);
           System.out.println("Reversed: " + reversed);
       }
   }
   ```

10. Соберите и запустите проект:
    ```bash
    ./gradlew build
    ./gradlew run
    ```

## Требования к выполнению

1. Проект должен успешно собираться и запускаться
2. Модуль `app` должен зависеть от модуля `core`
3. Модуль `core` должен содержать как минимум один утилитный класс
4. Модуль `app` должен использовать функциональность из модуля `core`
5. Добавьте тесты для обоих модулей

## Дополнительные задания

1. Добавьте третий модуль `api`, который будет зависеть от `core` и предоставлять REST API
2. Настройте общие зависимости для всех модулей в корневом `build.gradle`
3. Добавьте плагин для генерации документации (Javadoc) и настройте его для всех модулей

## Критерии оценки

- Правильность структуры проекта
- Корректность настройки зависимостей между модулями
- Качество кода и тестов
- Выполнение дополнительных заданий

## Сдача задания

Загрузите проект в ваш личный репозиторий и предоставьте ссылку преподавателю.
