# Задание 1: Создание простого Java-проекта с Gradle

## Цель
Научиться создавать и настраивать простые Java-проекты с использованием Gradle.

## Задание

Создайте простой Java-проект с Gradle, который будет содержать класс для работы со строками и демонстрационное приложение.

### Шаги выполнения

1. Создайте директорию проекта:
   ```bash
   mkdir gradle-string-utils
   cd gradle-string-utils
   ```

2. Инициализируйте Gradle-проект:
   ```bash
   gradle init --type java-application
   ```

3. Выберите следующие опции при инициализации:
   - Язык реализации: Java
   - Система сборки DSL: Groovy
   - Тестовый фреймворк: JUnit Jupiter
   - Имя проекта: gradle-string-utils
   - Имя пакета исходного кода: com.example.stringutils

4. Изучите созданную структуру проекта:
   ```
   gradle-string-utils/
   ├── app/
   │   ├── build.gradle
   │   └── src/
   │       ├── main/
   │       │   └── java/
   │       │       └── com/
   │       │           └── example/
   │       │               └── stringutils/
   │       │                   └── App.java
   │       └── test/
   │           └── java/
   │               └── com/
   │                   └── example/
   │                       └── stringutils/
   │                           └── AppTest.java
   ├── gradle/
   │   └── wrapper/
   │       ├── gradle-wrapper.jar
   │       └── gradle-wrapper.properties
   ├── gradlew
   ├── gradlew.bat
   └── settings.gradle
   ```

5. Создайте класс `StringUtils`:
   ```java
   // app/src/main/java/com/example/stringutils/StringUtils.java
   package com.example.stringutils;

   public class StringUtils {
       /**
        * Переворачивает строку.
        * @param input Входная строка
        * @return Перевернутая строка или null, если input равен null
        */
       public static String reverse(String input) {
           if (input == null) {
               return null;
           }
           return new StringBuilder(input).reverse().toString();
       }
       
       /**
        * Проверяет, является ли строка палиндромом.
        * @param input Входная строка
        * @return true, если строка читается одинаково в обоих направлениях
        */
       public static boolean isPalindrome(String input) {
           if (input == null) {
               return false;
           }
           String cleaned = input.toLowerCase().replaceAll("[^a-zA-Z0-9]", "");
           return cleaned.equals(new StringBuilder(cleaned).reverse().toString());
       }
       
       /**
        * Подсчитывает количество слов в строке.
        * @param input Входная строка
        * @return Количество слов
        */
       public static int countWords(String input) {
           if (input == null || input.trim().isEmpty()) {
               return 0;
           }
           return input.trim().split("\\s+").length;
       }
   }
   ```

6. Модифицируйте класс `App`:
   ```java
   // app/src/main/java/com/example/stringutils/App.java
   package com.example.stringutils;

   public class App {
       public static void main(String[] args) {
           String text = "Gradle is awesome!";
           
           System.out.println("Original text: " + text);
           System.out.println("Reversed: " + StringUtils.reverse(text));
           System.out.println("Word count: " + StringUtils.countWords(text));
           
           String palindrome = "A man, a plan, a canal: Panama";
           System.out.println("\"" + palindrome + "\" is a palindrome: " + 
                             StringUtils.isPalindrome(palindrome));
       }
   }
   ```

7. Добавьте тесты для класса `StringUtils`:
   ```java
   // app/src/test/java/com/example/stringutils/StringUtilsTest.java
   package com.example.stringutils;

   import org.junit.jupiter.api.Test;
   import static org.junit.jupiter.api.Assertions.*;

   class StringUtilsTest {
       @Test
       void testReverse() {
           assertEquals("olleH", StringUtils.reverse("Hello"));
           assertNull(StringUtils.reverse(null));
           assertEquals("", StringUtils.reverse(""));
       }
       
       @Test
       void testIsPalindrome() {
           assertTrue(StringUtils.isPalindrome("A man, a plan, a canal: Panama"));
           assertTrue(StringUtils.isPalindrome("racecar"));
           assertFalse(StringUtils.isPalindrome("hello"));
           assertFalse(StringUtils.isPalindrome(null));
       }
       
       @Test
       void testCountWords() {
           assertEquals(3, StringUtils.countWords("Hello beautiful world"));
           assertEquals(0, StringUtils.countWords(""));
           assertEquals(0, StringUtils.countWords(null));
           assertEquals(1, StringUtils.countWords("SingleWord"));
       }
   }
   ```

8. Модифицируйте файл `build.gradle` для добавления зависимостей:
   ```groovy
   plugins {
       id 'application'
   }

   repositories {
       mavenCentral()
   }

   dependencies {
       implementation 'org.apache.commons:commons-lang3:3.12.0'
       
       testImplementation 'org.junit.jupiter:junit-jupiter:5.8.2'
   }

   application {
       mainClass = 'com.example.stringutils.App'
   }

   tasks.named('test') {
       useJUnitPlatform()
   }
   ```

9. Соберите и запустите проект:
   ```bash
   ./gradlew build
   ./gradlew run
   ```

## Требования к выполнению

1. Проект должен успешно собираться и запускаться
2. Класс `StringUtils` должен содержать как минимум три метода для работы со строками
3. Все методы должны быть покрыты тестами
4. Проект должен использовать хотя бы одну внешнюю зависимость

## Дополнительные задания

1. Добавьте метод для подсчета частоты символов в строке
2. Создайте задачу Gradle для генерации отчета о покрытии кода тестами
3. Настройте проект для создания исполняемого JAR-файла с зависимостями

## Критерии оценки

- Правильность структуры проекта
- Корректность работы методов
- Качество кода и тестов
- Выполнение дополнительных заданий

## Сдача задания

Загрузите проект в ваш личный репозиторий и предоставьте ссылку преподавателю.
