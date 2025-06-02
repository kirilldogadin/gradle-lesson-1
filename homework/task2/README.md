# Задание 2: Исследование classpath

## Цель
Понять, как Gradle управляет classpath и различия между compile classpath и runtime classpath.

## Задание

Добавьте в проект задачу, которая выводит:
- Compile classpath
- Runtime classpath

Проанализируйте различия между ними и объясните, почему они отличаются.

### Шаги выполнения

1. Создайте новый Gradle-проект:
   ```bash
   mkdir gradle-classpath
   cd gradle-classpath
   gradle init --type java-application
   ```

2. Добавьте несколько зависимостей разных типов в `build.gradle`:
   ```groovy
   dependencies {
       implementation 'com.google.guava:guava:31.1-jre'
       compileOnly 'org.projectlombok:lombok:1.18.24'
       runtimeOnly 'org.slf4j:slf4j-simple:2.0.5'
       testImplementation 'junit:junit:4.13.2'
   }
   ```

3. Добавьте задачу для вывода classpath:
   ```groovy
   task printClasspaths {
       doLast {
           println "Compile classpath:"
           println "----------------"
           configurations.compileClasspath.each { println it }
           
           println "\nRuntime classpath:"
           println "----------------"
           configurations.runtimeClasspath.each { println it }
       }
   }
   ```

4. Запустите задачу:
   ```bash
   ./gradlew printClasspaths
   ```

5. Проанализируйте вывод и определите:
   - Какие зависимости присутствуют в compile classpath
   - Какие зависимости присутствуют в runtime classpath
   - Какие зависимости присутствуют в обоих classpath
   - Какие зависимости отсутствуют в одном из classpath

6. Напишите отчет, объясняющий:
   - Различия между compile classpath и runtime classpath
   - Почему некоторые зависимости присутствуют только в одном classpath
   - Как конфигурации зависимостей (`implementation`, `compileOnly`, `runtimeOnly`) влияют на classpath

## Требования к выполнению

1. Создайте проект с различными типами зависимостей
2. Реализуйте задачу для вывода classpath
3. Напишите подробный отчет с анализом результатов
4. Включите примеры и объяснения для каждого типа зависимости

## Дополнительные задания

1. Добавьте транзитивные зависимости и проанализируйте их влияние на classpath
2. Исследуйте, как исключение зависимостей влияет на classpath
3. Создайте визуальное представление зависимостей (например, с помощью GraphViz)

## Критерии оценки

- Полнота анализа classpath
- Правильность объяснения различий между compile classpath и runtime classpath
- Качество отчета и примеров
- Выполнение дополнительных заданий

## Сдача задания

Загрузите проект и отчет в ваш личный репозиторий и предоставьте ссылку преподавателю.
