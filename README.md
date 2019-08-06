# Сгенерить ЕЦП ключ для налоговой через Privat24.
 - логинимся в  https://www.privat24.ua/ в Персональный кабинет (не для бизнесса)
 - Идем в Все услуги - бизнесс - Загрузить сертификать.
 - Ставим екстешен для хрома https://chrome.google.com/webstore/detail/bankid-cryptoplugin/pgfbdgicjmhenccemcijooffohcdanic
 - Если у вас линукс качаем шелл скрипт для хромовского екстеншена. 
   - Если у вас Хромиум (а не хром), то меняем в скрипте путь `sed -i 's/google-chrome/chromium/g' ./cryptoplugin-1.2.2.run `
   - Устанавливаем скрипт `sh ./cryptoplugin-1.2.2.run`
   - Если что-то сломалось, открываем скрипт через редактор, видим, что логи пишутся в `log_file="$HOME/.cryptoplugin/installer.log"
` и проверяем этот файл
- Создаем ЕЦП ключ
- Логинимся в https://cabinet.sfs.gov.ua выбрав акредитированный центр Приват

# Сдаем отчетность
 - Логинимся в https://www.privat24.ua/ для бизнеса
 - Жмакаем "Вернуться в старый интрефейс"
 - Документы - Електронная отчетность 
 - Создать отчет - Подактова декларация платника единого податку ФОП 3 группа
 - Редактировать:
   - Подактовый звитный период - ставим в зависимости от квартала 
   - Подактовый звитный период, язык уточнюется - оставляем без изменений)
   - Факточна чисельнисть найманых працивникив - 0
   - Код Згидно КВЕД - 62.01 ( http://www.proagro.com.ua/reference/promua/skp/7403.html)
   - Ряд 06 (Обсяг доходу за звитный период що оподатковуется за ставкою 5%) - сколько в сумме от начало года до этого квадрата, учитывая этот квартал. Можно посмотреть в налоговом кабинете по предидущей декларации на https://cabinet.sfs.gov.ua)
   - ряд 08 (Загальна сумма доходу за звитный подактовий перид, сума значчень радкив 01 -07) - указываем столько же сколько и в 06 (суммируем рядки 01-07, поскольку у нас ток 06 указан, то он просто продублируетсяю)
   - ряд 11 (сума податку за ставкою 5%) - умножаем ряд 06 на 0.05 
   - Ряд 12 (суммируем 09 10 11, т.е.) - дублируем рядок 11
   - Ряд 13 (Нараховано за попредений звитный период). То, что получили во всех предидущих кварталах умножаем на 0.05 (т.е. 08 ряд отнимаем то, что получили в текущем, и умножаем на 0.05)
   - Ряд 14 (Сумма единого податку, яка пидлягае) - То, что получили в этом квартале умножаем на 0.05 (т.е. ряд 13 + ряд 14 = ряд 12)
 - Пример (например отчет на полугодие, за первый квартал 75$, за второй 100$):
   - Подактовый звитный период - полугодие
   - Факточна чисельнисть найманых працивникив - 0
   - Код Згидно КВЕД - 62.01
   - Ряд 06 - 175
   - ряд 08 - 175
   - ряд 11 - 8.75
   - Ряд 12 - 8.75
   - Ряд 13 - 3.75
   - Ряд 14 - 5
 - Подписуем ключем ЕЦП, с первого пункта (как директор) и отправляем
 - Дальше можно трекать статус в Привате и в налоговом кабинете
 
# Платил ЕСВ/ЕН
   - идем на https://taxer.ua/ (советую зарегаться, платить 450 грн в год необязатальено)
     - жмакаемм на календарь, выбираем Уплата ЕСВ (или ЕН)
     - Сформировать отчет 
     - Выбираем свою область и город -> запоминаем данные
     - ДЛЯ ЕСВ (фикс около 2700) `*;101;1234567890;Сплата ЄСВ за II квартал 2019 року;;;` где 1234567890 ваш идентификационый, посмотреть его можно залогинившись в taxer и нажать на Уплату ЕН -> сформировать отчет ФЛП Фаилимя Имя - сгенерировать отчет
     - ДЛЯ ЕН (5%)`*;101;3350113472;Сплата ЄП за I квартал 2019 року;;;`
   - Логинимся в приват для бизнесса (платить можно также через платеж через украину в приват для физического лица, провернно лично мной)
     - Посмотреть ЕН за  текущий квартар -> 
        - новый интрефейфес
        - Счета и Выписки
        - Выбираем карту
        - Выписка за предыдущий квартал
        - Листаем до самого низа и нажимаем прогрузить, пока кнопка не исчезнет ( если у вас много транзакций)
        - devconsole -> в Elements выбираем iframe со списоком, в консоли выполняем `document.querySelectorAll('.panel tr:not(.repeat-dissabled)').forEach(a => a.style.display = 'none')`
        - Считаем сумму на всех картах
      - Создаем платеж:
        - Гривневые платежи - создать платеж - гривневый
        - Все что запомнили в пункте выше вводим в платеж (можно также создать шаблон)
        - Наименование должно само подтянуться
        - Сохраняем,
        - Подписать можно СМС зашел в журнал платежей
