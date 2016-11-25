GPRS Shield
===========

Библиотека для Arduino, позволяющая управлять [GPRS Shield’ом](http://amperka.ru/product/arduino-gprs-shield)
от [Амперки](http://amperka.ru/).

Установка
=========

Скачайте последний релиз библиотеки:

<a class="btn btn-sm btn-primary" href="https://github.com/amperka/gprs-shield/releases/download/v1.1/GPRSShield-1.1.zip">Скачать GPRS Shield v1.1</a>

В Arduino IDE выберите пункт меню «Скетч» → «Импортировать библиотеку» →
«Добавить библиотеку…». В появившемся окне выберите скачаный архив с
библиотекой. Установка завершена.

Пример использования
====================

```cpp
// библиотека для работы с GPRS устройством
#include <GPRS_Shield_Arduino.h>
 
// библиотека для эмуляции Serial порта
// она нужна для работы библиотеки GPRS_Shield_Arduino
#include <SoftwareSerial.h>
 
// создаём объект класса GPRS и передаём в него объект Serial1 
GPRS gprs(Serial1);
// можно указать дополнительные параметры — пины PK и ST
// по умолчанию: PK = 2, ST = 3
// GPRS gprs(Serial1, 2, 3);
 
void setup()
{
  // включаем GPRS шилд
  gprs.powerUpDown();
  // открываем последовательный порт для мониторинга действий в программе
  Serial.begin(9600); 
  while (!Serial) {
    // ждём, пока не откроется монитор последовательного порта
    // для того, чтобы отследить все события в программе
  }
  // проверяем есть ли связь с GPRS устройством
  while (!gprs.init()) {
    // если связи нет, ждём 1 секунду
    // и выводим сообщение об ошибке
    // процесс повторяется в цикле
    // пока не появится ответ от GPRS устройства
    delay(1000);
    Serial.print("Init error\r\n");
  }
  // отправляем сообщение по указанному номеру с заданным текстом
  gprs.sendSMS("+79263995140", "Hello SMS from Amperka!");
}
 
void loop()
{
}
```

Больше примеров — [в статье на Амперка / Вики](http://wiki.amperka.ru/%D0%BF%D1%80%D0%BE%D0%B4%D1%83%D0%BA%D1%82%D1%8B:gprs-shield).
