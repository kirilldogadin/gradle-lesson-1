# Упражнение 1: Создание базового Gradle-проекта

## Цель
Познакомиться с базовой структурой Gradle-проекта и Gradle Wrapper.

## Необходимые инструменты
- JDK 11 или выше
- Терминал/командная строка

## Шаги выполнения

### 1. Создание директории проекта
```bash
mkdir gradle-demo
cd gradle-demo
```

### 2. Инициализация Gradle-проекта
```bash
gradle init --type java-application
```

Если у вас не установлен Gradle глобально, вы можете использовать:
```bash
# На Linux/macOS
curl -s "https://get.sdkman.io" | bash
source "$HOME/.sdkman/bin/sdkman-init.sh"
sdk install gradle

# На Windows через PowerShell
Set-ExecutionPolicy Bypass -Scope Process -Force
iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
choco install gradle
```

### 3. Изучение созданной структуры проекта

После инициализации проекта изучите созданную структуру:
```bash
ls -la
```

Обратите внимание на следующие файлы и директории:
- `build.gradle` — основной файл конфигурации сборки
- `settings.gradle` — настройки проекта
- `gradle/wrapper/` — файлы Gradle Wrapper
- `gradlew` и `gradlew.bat` — скрипты запуска Gradle Wrapper
- `src/` — директория с исходным кодом

### 4. Запуск сборки проекта
```bash
./gradlew build
```

### 5. Запуск приложения
```bash
./gradlew run
```

## Вопросы для обсуждения

1. Какие файлы были созданы при инициализации проекта?
2. Зачем нужны файлы в директории `gradle/wrapper/`?
3. Почему рекомендуется использовать Gradle Wrapper вместо глобально установленного Gradle?
4. Какие задачи (tasks) доступны в созданном проекте? (Подсказка: выполните `./gradlew tasks`)
5. Что произойдет при выполнении команды `./gradlew clean`?

## Связь с уроком

Это упражнение демонстрирует:
- Процесс создания базового Gradle-проекта
- Структуру Gradle-проекта
- Использование Gradle Wrapper
- Базовые команды Gradle

## Дополнительные задания

1. Измените сообщение, выводимое приложением, и запустите его снова
2. Изучите содержимое файла `gradle-wrapper.properties` и объясните его назначение
3. Выполните команду `./gradlew help` и изучите доступную справку

## Следующий шаг

После выполнения этого упражнения переходите к [Упражнению 2: Изучение структуры build.gradle](../exercise2/README.md)
