## Отчёт о тестировании Credit Card Number Validator##

 **Краткое описание**

Проверка реализованности функциональности валидации банковских карт. Проведено функциональное тестирование приложения валидатора на основе наработок программиста и использования программы IntelliJ IDEA (См. пункт Источник тестовых данных)

**Дата начала:** 11.12.2020

**Дата окончания:** 11.12.2020

**На тестирование затрачено:** 1 час 

**Что нужно проверить:**

1. Приложение IntelliJ IDEA запускается и совместимо с Java 11

2. Приложение работает согласно руководству использования

3. Валидация проходит успешно, при валидных номерах карт

## **Описание процесса тестирования** ##

1. Скачать и протестировать установку IntelliJIDEA в соответствии с инструкцией по ссылке: https://github.com/netology-code/javaqa-homeworks/blob/master/intro/idea.md
2. Изменить содержимое файла Main.java на наработки кода программиста
3. В 4 строку кода поочередно вставлять номера невалидных карт, разных брендов, сгенерированных по ссылке: https://www.freeformatter.com/credit-card-number-generator-validator.html
5. Смотреть на результат вывода программы внизу экрана 

**В процессе тестирования использовались следующие артефакты:**
* IntelliJIDEA
* Код оставшийся от программиста:

public class Main {
  public static void main(String[] args) {
    
    String number = "5351719427810741";
        System.out.println(String.format("Result is %s", isValidCardNumber(number) ? "OK" : "FAIL"));
  }

  public static boolean isValidCardNumber(String number) {
    if (number == null) {
      return false;
    }

    if (number.length() != 16) {
      return false;
    }

    long result = 0;
    for (int i = 0; i < number.length(); i++) {
      int digit;
      try {
        digit = Integer.parseInt(number.charAt(i) + "");
      } catch (NumberFormatException e) {
        return false;
      }

      if (i % 2 == 0) {
        digit *= 2;
        if (digit > 9) {
          digit -= 9;
        }
      }
      result += digit;
    }

    return (result != 0) && (result % 10 == 0);
  }
}

**В качестве тестовых данных использовались данные сервиса, который генерирует валидные номера карт:**
https://www.freeformatter.com/credit-card-number-generator-validator.html

**Ожидаемый результат**

Для валидных номеров карт: «Result is OK»

**Фактический результат**

Программа считает валидными только 16-ти значные номера банковских карт вне зависимости от бренда карты

**В результате тестирования выявлены следующие дефекты:**

https://github.com/mariyaburtseva/Java-homework-1-2/issues/1

**Тестирование производилось в следующем окружении:**

* Ноутбук Dell 
* Windows 10, X64
* Версия Java: 11.0.9.1
* Yandex.Browser 20.11.2.78 (64-bit)
