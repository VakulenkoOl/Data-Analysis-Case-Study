# Data-Analysis-Case-Study
## Аналіз FitBit Fitness Tracker Data отримуючи Google Data Analytics Professional Certificate
### 1. Умови
Під час отрмання Google Data Analytics Professional Certificate програма дає можливість створити власне дослідження на 2 теми на вибір. Я зосередився саме на FitBit Fitness Tracker Data, оскільки вона здалась мені цікавою за рахунок великої кількості метрик, які можна проаналізувати, знайти кореляцію та причинно-наслідковий зв'язок між ними та отримати інсайди.

Власне, вихідні умови такі: "Ви - молодший аналітик даних у команді маркетингової аналітики компанії Bellabeat, високотехнологічного виробника товарів для здоров’я, орієнтованих на жінок. Bellabeat — успішна невелика компанія, яка має потенціал стати значним гравцем на світовому ринку розумних пристроїв. Уршка Сршен, співзасновниця та директорка з креативних питань Bellabeat, вважає, що аналіз даних про фізичну активність, отриманих із розумних пристроїв, може допомогти компанії відкрити нові можливості для зростання. Вам доручено зосередитися на одному з продуктів Bellabeat і проаналізувати дані з розумних пристроїв, щоб зрозуміти, як саме споживачі ними користуються. Отримані висновки допоможуть сформувати маркетингову стратегію компанії. Ви представите результати аналізу керівництву Bellabeat разом із загальними рекомендаціями щодо маркетингової стратегії компанії."

Bellabeat має декілька продуктів, але тут я зосередився саме на Bellabeat app, оскільки застосунок Bellabeat надає користувачам інформацію про стан здоров’я, що стосується їхньої активності, сну, рівня стресу та менструального циклу. Ці дані допомагають користувачам краще зрозуміти свої звички й приймати рішення, корисні для здоров’я.

У цьому досліджені я використав 6 етапів аналізу даних:
* Ask
* Prepare
* Process
* Analyze
* Share
* Act

### 2. Ask
Завдання полягає у тому, щоб зосередитися на одному з продуктів Bellabeat і проаналізувати дані про використання розумних пристроїв, щоб зрозуміти, як саме люди вже користуються ними. На основі отриманої інформації потрібно зробити узагальнені рекомендації щодо того, як ці тенденції можуть вплинути на маркетингову стратегію Bellabeat.

До стейкхолдерів належать:
* Уршка Сршен: співзасновниця та директорка з креативних питань компанії Bellabeat
* Сандо Мур: математик і співзасновник Bellabeat; ключовий член управлінської команди Bellabeat.
* Команда маркетингової аналітики Bellabeat

### 3. Prepare
Для цього дослідження нам надали [📊 Fitbit Fitness Tracker Data на Kaggle](https://www.kaggle.com/datasets/arashnic/fitbit)

Цей датасет було сформовано на основі відповідей учасників опитування, проведеного через платформу Amazon Mechanical Turk у період із 3 по 5 грудня 2016 року. Тридцять користувачів Fitbit дали згоду на надання персональних даних із трекера, зокрема показників фізичної активності, частоти серцевих скорочень і моніторингу сну з деталізацією по хвилинах. Проте, в ході аналізу було виявлено, що користувачів 33 у більшості файлів.

Сам датасет є публічним, тож я можу копіювати, змінювати, поширювати та публічно демонструвати його, зокрема й із комерційною метою, без отримання додаткового дозволу.

Власне сам датасет я завантажував zip-файлом, у якому було 18 csv-файлів. Оскільки файли відносно невеликі, я зміг відкрити та проаналізувати ці файли в Google Sheets. Для подальшого послідження я використав 6 файлів, бо саме з них можна було дістати необхідні інсайди, окрім того, більшість файлів - звіт по окремому показнику, котрі і так були представлені у merged файлах. Список використаних файлів:

* dailyActivity_merged.csv
* hourlyCalories_merged.csv
* hourlySteps_merged.csv
* sleepDay_merged.csv
* hourlyIntensities_merged.csv
* weightLogInfo_merged.csv

Щодо актуальності та достовірності даних, то можна констатувати, що жоден з цих показників не дотриманий. Дані були зібрані у грудні 2016 року, тому є неактуальними. У датасеті немає жодних даних про вік, стать та місцезнаходження користувачів, а також сама вибірка є дуже малою (33 людини), що робить її нерепрезентативною для широкого загалу користувачів. Самі продукти Bellabeat орієнтовані на жінок, тож можна припускати, що абсолютна більшість користувачів це саме жінки, проте ми не можемо знати напевно.

### 4. Process
Під час цього етапу я очистив дані та привів їх до уніфікованого формату:
* Відсортував та відфільтрував дані (видалив порожні значення);
* Прибрав дублікати та пробіли;
* Змінив формат дат з mm.dd.yyyy на dd.mm.yyyy, створив окремі колонки які позначали дні тижня;
* Змінив годинний формат з tt на hh:mm;
* За необхідності розділив колонки mm.dd.yyyy tt на окремо dd.mm.yyyy та hh:mm;

### 5. Analyze
Вже очищені файли я аналізував у BigQuery та Jupyter Notebook. Тут я викладу аналіз саме за допомогою SQL, а ідентичні кроки, але вже за допомогою Python викладені тут [AnalysisPython](AnalysisPython.ipynb)

Також всі візуалізації я робив за допомогою Tableu. 
**Посилання на дашборди: Інтерактивний дашборд у Tableau[![FitBit Dashboard Preview](images/tableau_dashboard_preview.png)](https://public.tableau.com/views/Book1_17918991296460/Dashboard1)**

З файлу dailyActivity_merged дізнався середні значення різних змінних:
```sql
SELECT 
  round(AVG(Calories),1) AS AverageCalories,
  round(AVG(TotalSteps),1) AS AverageSteps,
  round(AVG(TotalDistance),1) AS AverageDistance,
  round(AVG(VeryActiveDistance),1) AS AverageVeryActiveDistance,
  round(AVG(ModeratelyActiveDistance),1) AS AverageModeratelyActiveDistance,
  round(AVG(LightActiveDistance),1) AS AverageLightActiveDistance,
  round(AVG(VeryActiveMinutes),1) AS AverageVeryActiveMinutes,
  round(AVG(FairlyActiveMinutes),1) AS AverageFairlyActiveMinutes,
  round(AVG(LightlyActiveMinutes),1) AS AverageLightlyActiveMinutes,
  round(AVG(SedentaryMinutes),1) AS AverageSedentaryMinutes,
FROM core-almanac-504208-f8.fit_bit.dailyActivity_merged
```
Результат 
![середні значення dailyActivity_merged](images/image_2026-10-05_11-17-30.png)

Дізнався середні значення різних змінних відповідно до дня тижня
```sql
SELECT 
  DayOfTheWeek,
  round(AVG(Calories),1) AS AverageCalories,
  round(AVG(TotalSteps),1) AS AverageSteps,
  round(AVG(TotalDistance),1) AS AverageDistance,
  round(AVG(VeryActiveDistance),1) AS AverageVeryActiveDistance,
  round(AVG(ModeratelyActiveDistance),1) AS AverageModeratelyActiveDistance,
  round(AVG(LightActiveDistance),1) AS AverageLightActiveDistance,
  round(AVG(VeryActiveMinutes),1) AS AverageVeryActiveMinutes,
  round(AVG(FairlyActiveMinutes),1) AS AverageFairlyActiveMinutes,
  round(AVG(LightlyActiveMinutes),1) AS AverageLightlyActiveMinutes,
  round(AVG(SedentaryMinutes),1) AS AverageSedentaryMinutes,
FROM core-almanac-504208-f8.fit_bit.dailyActivity_merged
WHERE DayOfTheWeek IS NOT NULL
GROUP BY DayOfTheWeek
ORDER BY 
  CASE 
    WHEN DayOfTheWeek LIKE 'пон%' THEN 1
    WHEN DayOfTheWeek LIKE 'вів%' THEN 2
    WHEN DayOfTheWeek LIKE 'сер%' THEN 3
    WHEN DayOfTheWeek LIKE 'чет%' THEN 4
    WHEN DayOfTheWeek LIKE 'п%'   THEN 5
    WHEN DayOfTheWeek LIKE 'суб%' THEN 6
    WHEN DayOfTheWeek LIKE 'нед%' THEN 7
  END
```
Результат 
![середні значення різних змінних відповідно до дня тижня](images/image_2026-10-05_11-33-00.png)
<img width="1189" height="794" alt="image" src="https://github.com/user-attachments/assets/45e34a05-c153-4b0c-84ae-5a10fceff6e9" />


Найменш активними днями тижня за кількістю кроків, калорій та відстанню є понеділок, п'ятниця та неділя, натомість найактивнішими для цих показників є середа, четвер та субота. Для хвилин високої інтенсивності наймеш активними є вівторок, п'ятниця та неділя, найбільш - понеділок, середа, субота. Для хвилин помірної інтенсивності найменш активними є понеділок, четвер, п'ятниця та неділя, а решта - найактивніші. Для хвилин легкої інтенсивності спостерігається поступове зростання від початку тижня, що спадає у неділю.

Потім я підрахував кількість окремих користувачів
```sql
SELECT 
  count(distinct(id))
FROM core-almanac-504208-f8.fit_bit.dailyActivity_merged
```
Їх виявилося 33.

Підрахував середні значення різних показників за день кожного користувача
```sql
SELECT 
  id,
  round(AVG(Calories),1) AS AverageCalories,
  round(AVG(TotalSteps),1) AS AverageSteps,
  round(AVG(TotalDistance),1) AS AverageDistance,
  round(AVG(VeryActiveDistance),1) AS AverageVeryActiveDistance,
  round(AVG(ModeratelyActiveDistance),1) AS AverageModeratelyActiveDistance,
  round(AVG(LightActiveDistance),1) AS AverageLightActiveDistance,
  round(AVG(VeryActiveMinutes),1) AS AverageVeryActiveMinutes,
  round(AVG(FairlyActiveMinutes),1) AS AverageFairlyActiveMinutes,
  round(AVG(LightlyActiveMinutes),1) AS AverageLightlyActiveMinutes,
  round(AVG(SedentaryMinutes),1) AS AverageSedentaryMinutes
FROM core-almanac-504208-f8.fit_bit.dailyActivity_merged
group by id
order by id
```
Результат 
![середні значення різних змінних відповідно до дня тижня](images/image_2026-10-05_12-09-38.png)
<img width="1164" height="781" alt="image" src="https://github.com/user-attachments/assets/caeb351c-5397-4516-948e-d04c7f0aa5b7" />

Я розділив людей на категорії за їхнім рівнем активності (за кроками >10к - висока, >5к - середня, решта - низька) з використанням тимчасової таблиці та порахував к-сть людей у кожній категорії та їхнє співвідношення.
```sql
WITH UserGroups AS (
  SELECT 
    id,
    AVG(TotalSteps) AS AverageSteps,
    CASE 
      WHEN AVG(TotalSteps) >= 10000 THEN 'High Activity'
      WHEN AVG(TotalSteps) >= 5000  THEN 'Moderate Activity'
      ELSE 'Low Activity'
    END AS ActivityGroup
  FROM core-almanac-504208-f8.fit_bit.dailyActivity_merged
  GROUP BY id
)

SELECT 
  ActivityGroup,
  COUNT(id) AS UserCount,
  ROUND(COUNT(id) * 100.0 / SUM(COUNT(id)) OVER(), 1) AS Percentage
FROM UserGroups
GROUP BY ActivityGroup
ORDER BY UserCount DESC;
```
Результат


![середні значення різних змінних відповідно до дня тижня](images/image_2026-10-05_13-10-28.png)
<img width="1190" height="798" alt="image" src="https://github.com/user-attachments/assets/535b0e0d-720f-4500-858a-a8c86ff464a0" />
