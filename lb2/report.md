# Лабораторна робота №2

**Проєктування тестів. Checklist, Test Cases та Decision Table**

**Виконав:** Демидьонок Роман **Група:** ПІ:6.1214-пі-с2 **Дата виконання:** 17.11.2026

## Test Object

SauceDemo — Login: https://www.saucedemo.com/

## Test Conditions

- TCND-01 - успішна авторизація валідного користувача;
- TCND-02 - авторизація з неправильним Username;
- TCND-03 - авторизація з неправильним Password;
- TCND-04 - авторизація з порожнім Username;
- TCND-05 - авторизація з порожнім Password;
- TCND-06 - авторизація заблокованого користувача.

## Checklist

- [ ] Успішна авторизація з валідними даними.
- [ ] Відмова в авторизації з неправильним Username.
- [ ] Відмова в авторизації з неправильним Password.
- [ ] Перевірка порожнього Username.
- [ ] Перевірка порожнього Password.
- [ ] Відмова в авторизації заблокованого користувача.

## Test Cases

### TC-LOGIN-01 - Успішна авторизація standard_user

**Type:** Positive

**Preconditions:**
- відкрита сторінка Login SauceDemo;
- користувач не авторизований.

**Test Data:**
- Username: standard_user
- Password: secret_sauce

**Steps:**
1. У поле Username ввести standard_user.
2. У поле Password ввести secret_sauce.
3. Натиснути кнопку Login.

**Expected Result:**
Після введення standard_user і правильного пароля та натискання Login користувач успішно авторизується і переходить на сторінку Products.

**Actual Result:**
Після введення standard_user і правильного пароля та натискання Login відкрилася сторінка Products.

**Result:**
Pass

### TC-LOGIN-02 - Відмова в авторизації standard_user з неправильним Password

**Type:** Negative

**Preconditions:**
- відкрита сторінка Login SauceDemo;
- користувач не авторизований.

**Test Data:**
- Username: standard_user
- Password: wrong_password

**Steps:**
1. У поле Username ввести standard_user.
2. У поле Password ввести wrong_password.
3. Натиснути кнопку Login.

**Expected Result:**
Після введення standard_user і неправильного пароля та натискання Login авторизація не виконується, користувач залишається на сторінці Login, відображається повідомлення "Epic sadface: Username and password do not match any user in this service".

**Actual Result:**
Після введення standard_user і неправильного пароля та натискання Login користувач залишився на сторінці Login, відобразилося повідомлення "Epic sadface: Username and password do not match any user in this service".

**Result:**
Pass

### TC-LOGIN-03 - Відмова в авторизації locked_out_user

**Type:** Negative

**Preconditions:**
- відкрита сторінка Login SauceDemo;
- користувач не авторизований.

**Test Data:**
- Username: locked_out_user
- Password: secret_sauce

**Steps:**
1. У поле Username ввести locked_out_user.
2. У поле Password ввести secret_sauce.
3. Натиснути кнопку Login.

**Expected Result:**
Після введення locked_out_user і правильного пароля та натискання Login авторизація не виконується, користувач залишається на сторінці Login, відображається повідомлення "Epic sadface: Sorry, this user has been locked out."

**Actual Result:**
Після введення locked_out_user і правильного пароля та натискання Login користувач залишився на сторінці Login, відобразилося повідомлення "Epic sadface: Sorry, this user has been locked out."

**Result:**
Pass

## Decision Table

Умови:
- C1 - Username входить до списку допустимих?
- C2 - Password правильний?
- C3 - Користувач заблокований?

Дії:
- A1 - перейти до Products
- A2 - показати повідомлення про блокування
- A3 - показати повідомлення про неправильні credentials

| | R1 | R2 | R3 | R4 | R5 |
|---|---|---|---|---|---|
| C1: Username валідний? | T | T | F | T | F |
| C2: Password правильний? | T | T | T | F | F |
| C3: Користувач заблокований? | F | T | - | - | - |
| **A1: Products** | X | | | | |
| **A2: Locked message** | | X | | | |
| **A3: Invalid credentials** | | | X | X | X |

- R1. valid Username + valid Password + not locked = Products
- R2. valid Username + valid Password + locked = Login denied (locked message)
- R3. invalid Username + valid Password = Invalid credentials
- R4. valid Username + invalid Password = Invalid credentials
- R5. invalid Username + invalid Password = Invalid credentials

Порожні Username / Password в таблицю не включено: SauceDemo перевіряє їх окремо, до перевірки credentials (див. TCND-04, TCND-05 у checklist).

### Відповідність Test Cases правилам

| Test Case | Правило |
|---|---|
| TC-LOGIN-01 | R1 |
| TC-LOGIN-02 | R4 |
| TC-LOGIN-03 | R2 |

**Правила без окремого Test Case:** R3 (invalid Username + valid Password) та R5 (invalid Username + invalid Password). Саме для цього корисна Decision Table: вона показала комбінації, які ми могли пропустити.

## Результати виконання

| Test Case | Type | Result |
|---|---|---|
| TC-LOGIN-01 | Positive | Pass |
| TC-LOGIN-02 | Negative | Pass |
| TC-LOGIN-03 | Negative | Pass |

## Висновок

У роботі було визначено 6 Test Conditions на основі Test Basis, складено checklist, описано 3 Test Cases (1 позитивний, 2 негативні) та побудовано Decision Table для перевірки облікових даних. Усі три Test Cases виконано в SauceDemo, фактичні результати збіглися з очікуваними (Pass). Decision Table показала, що правила R3 та R5 не покриті окремими Test Cases, тож їх варто додати при розширенні тестування.

## Відповіді на контрольні питання

1. **Test Basis** - документи/вимоги, на яких базується тестування. Потрібен, щоб знати Expected Result, а не вигадувати його.
2. **Test Condition** - що саме перевірити (коротко). **Test Case** - детальний опис як перевірити: дані, кроки, очікуваний результат.
3. На питання "Що потрібно перевірити?" (визначення Test Conditions).
4. На питання "Як це перевірити?" (створення Test Cases).
5. Checklist - компактний спосіб зафіксувати, що перевірити, без детального опису дій; зручний для швидких перевірок.
6. У checklist немає даних, кроків і чіткого очікуваного результату, тому інший тестувальник може зрозуміти пункт по-іншому.
7. Positive перевіряє правильну поведінку з коректними даними; negative - реакцію системи на некоректні дані чи дії.
8. Бо Pass означає, що фактична поведінка збіглася з очікуваною. Якщо система правильно відхилила невалідний вхід, як і очікувалось, тест пройдено.
9. Для систематизації комбінацій умов та їх результатів, щоб не пропустити важливу комбінацію.
10. Щоб об'єктивно визначити, чи працює система так, як вимагає Test Basis.
11. Pass - Actual Result збігається з Expected Result. Fail - не збігається.