# Понятие classpath

Classpath — это важное понятие в Java и Gradle, которое определяет, где JVM ищет классы и ресурсы при компиляции и выполнении программы. В этом документе рассмотрены основные аспекты classpath и его роль в Gradle.

## Что такое classpath?

Classpath — это параметр, который указывает JVM, где искать классы и ресурсы при выполнении программы. Classpath может включать:
- Директории с .class файлами
- JAR-файлы
- ZIP-файлы
- Модули (в Java 9+)

## Типы classpath в Gradle

В Gradle есть несколько типов classpath, каждый из которых используется на разных этапах сборки:

### 1. Compile Classpath

Compile classpath используется при компиляции исходного кода. Он включает:
- Классы из директории `src/main/java` после компиляции
- Зависимости, объявленные как `implementation`, `api`, `compileOnly`
- Аннотационные процессоры

```groovy
dependencies {
    implementation 'com.google.guava:guava:31.1-jre'
    compileOnly 'org.projectlombok:lombok:1.18.24'
}
```

### 2. Runtime Classpath

Runtime classpath используется при выполнении программы. Он включает:
- Классы из директории `src/main/java` после компиляции
- Ресурсы из директории `src/main/resources`
- Зависимости, объявленные как `implementation`, `api`, `runtimeOnly`

```groovy
dependencies {
    implementation 'com.google.guava:guava:31.1-jre'
    runtimeOnly 'org.slf4j:slf4j-simple:2.0.5'
}
```

### 3. Test Compile Classpath

Test compile classpath используется при компиляции тестового кода. Он включает:
- Compile classpath
- Классы из директории `src/test/java` после компиляции
- Зависимости, объявленные как `testImplementation`, `testCompileOnly`

```groovy
dependencies {
    testImplementation 'junit:junit:4.13.2'
    testCompileOnly 'org.mockito:mockito-core:4.8.0'
}
```

### 4. Test Runtime Classpath

Test runtime classpath используется при выполнении тестов. Он включает:
- Runtime classpath
- Классы из директории `src/test/java` после компиляции
- Ресурсы из директории `src/test/resources`
- Зависимости, объявленные как `testImplementation`, `testRuntimeOnly`

```groovy
dependencies {
    testImplementation 'junit:junit:4.13.2'
    testRuntimeOnly 'org.mockito:mockito-core:4.8.0'
}
```

## Конфигурации зависимостей в Gradle

Gradle использует различные конфигурации для управления зависимостями и их влиянием на classpath:

### implementation

Зависимости, необходимые для компиляции и выполнения. Не экспортируются в API проекта.

```groovy
dependencies {
    implementation 'com.google.guava:guava:31.1-jre'
}
```

### api

Зависимости, необходимые для компиляции и выполнения. Экспортируются в API проекта.

```groovy
dependencies {
    api 'org.apache.commons:commons-lang3:3.12.0'
}
```

### compileOnly

Зависимости, необходимые только для компиляции, но не для выполнения.

```groovy
dependencies {
    compileOnly 'org.projectlombok:lombok:1.18.24'
}
```

### runtimeOnly

Зависимости, необходимые только для выполнения, но не для компиляции.

```groovy
dependencies {
    runtimeOnly 'org.slf4j:slf4j-simple:2.0.5'
}
```

### testImplementation

Зависимости, необходимые для компиляции и выполнения тестов.

```groovy
dependencies {
    testImplementation 'junit:junit:4.13.2'
}
```

## Просмотр classpath в Gradle

Gradle предоставляет задачи для просмотра classpath:

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

## Управление classpath

### Исключение зависимостей

```groovy
dependencies {
    implementation('org.springframework.boot:spring-boot-starter-web') {
        exclude group: 'org.springframework.boot', module: 'spring-boot-starter-tomcat'
    }
}
```

### Принудительные версии

```groovy
configurations.all {
    resolutionStrategy {
        force 'com.google.guava:guava:31.1-jre'
    }
}
```

### Транзитивные зависимости

По умолчанию Gradle включает транзитивные зависимости. Их можно отключить:

```groovy
dependencies {
    implementation('com.google.guava:guava:31.1-jre') {
        transitive = false
    }
}
```

## Лучшие практики

1. **Используйте правильные конфигурации**
   - `implementation` для большинства зависимостей
   - `api` только для зависимостей, которые должны быть видны потребителям
   - `compileOnly` для зависимостей, которые предоставляются средой выполнения
   - `runtimeOnly` для зависимостей, которые нужны только во время выполнения

2. **Минимизируйте использование `api`**
   - Чрезмерное использование `api` может привести к "загрязнению" classpath
   - Используйте `implementation` везде, где это возможно

3. **Регулярно анализируйте зависимости**
   - Используйте `./gradlew dependencies` для анализа зависимостей
   - Исключайте ненужные транзитивные зависимости

4. **Разрешайте конфликты версий**
   - Используйте `resolutionStrategy` для разрешения конфликтов версий
   - Документируйте причины выбора конкретных версий

## Заключение

Понимание classpath и конфигураций зависимостей в Gradle является ключевым для эффективного управления зависимостями и оптимизации процесса сборки. Правильное использование конфигураций зависимостей помогает создавать более модульные и поддерживаемые проекты.
