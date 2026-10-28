# FNIRSI 2D15P — UA mod 1.2 / 1.3 / 1.4 / 1.5

Неофіційна модифікація прошивки осцилографа **FNIRSI 2D15P**: **українська мова інтерфейсу**, **виправлений англійський переклад** і (у версіях 1.3–1.5) **виправлення частини заводських вад**.
Unofficial modification of the **FNIRSI 2D15P** firmware: **Ukrainian interface language**, **corrected English translation** and (in 1.3–1.5) **fixes for some stock issues**. *English version below.*

> ⚠️ **Лише для прошивки V2.7.0.7** (файл `2D15P_V2.7.0.7_260826.bin`, CRC32 `B43E8C2D`).
> Патч перевіряє контрольну суму і **не застосується** до іншої версії. Не намагайтеся обійти цю перевірку: зміни прив'язані до точних адрес саме цієї версії, і на іншій прошивці прилад може не запуститися.

---

## Українською

### Яку версію обрати
| | **1.2** | **1.3** | **1.4** | **1.5** |
|---|---|---|---|---|
| Українська мова й виправлена англійська | ✓ | ✓ | ✓ | ✓ |
| Генератор: несинусоїдні форми до **5 МГц** (заводська межа 2 МГц) | — | ✓ | ✓ | ✓ |
| Звук у режимі діода | — | ✓ | ✓ | ✓ |
| «OL» замість «.OL» | — | ✓ | ✓ | ✓ |
| Кнопка **Menu** працює в генераторі й мультиметрі | — | — | ✓ | ✓ |
| Позначка прихованого фільтра (частота нижче 4,19 МГц) | — | — | ✓ | ✓ |
| Відносний вимір (REL) у мультиметрі | — | — | — | ✓ |
| Кнопка **Single** повертає попередній режим запуску | — | — | — | ✓ |
| Мультиметр: «Макс.» над «Мін.» | — | — | — | ✓ |
| Батарея: без раптових вимкнень від просідання напруги | — | — | — | ✓ |
| Файл патча | `2D15P_V2.7.0.7_UA-mod-1.2.bps` | `2D15P_V2.7.0.7_UA-mod-1.3.bps` | `2D15P_V2.7.0.7_UA-mod-1.4.bps` | `2D15P_V2.7.0.7_UA-mod-1.5.bps` |
| CRC32 результату | `3DD5A6F0` | `CA67F6A9` | `BA028F8D` | `5CF4B48D` |

- **1.2** — лише переклад, логіка приладу заводська. Ця версія заморожена: змінюватиметься тільки при критичній помилці в перекладі.
- **1.3** — переклад плюс виправлення, які змінюють поведінку приладу (генератор, мультиметр).
- **1.4** — усе з 1.3 плюс зручніше керування (Menu) і чесна позначка, коли прилад згладжує сигнал.
- **1.5** — усе з 1.4 плюс відносний вимір у мультиметрі, кнопка Single, стабільніша батарея і правки перекладу.
- Старі версії лишаються доступними: нові випуски виходять поруч, а не замість них. Оберіть ту, яка вам потрібна.
- **Усі патчі накладаються на заводську V2.7.0.7**, а не один на інший. Не накладайте новішу версію поверх уже пропатченої старшої.

### Що зроблено (обидві версії)
| | |
|---|---|
| Перекладено написів інтерфейсу | **115** + 9 поза таблицями мов |
| Виправлено англійських написів | **29** |
| Додано літер у шрифти | **74** символи × **6** шрифтів = **444** гліфи |
| Змін у розмітці меню | меню в **3** ряди + **13** карт дотиків |
| Вміст патча | лише власні зміни, без коду FNIRSI |

- **Українська мова** на місці китайської. У виборі мови: «Українська» / «English». Після скидання налаштувань прилад запускається українською.
- **Кирилиця в усіх шести шрифтах** приладу, підібрана за висотою й товщиною під заводську латиницю (гарнітура Fixel).
- **Виправлена англійська**, наприклад: «Level» → «Horizontal», «Ramp» → «Triangle», «Skew» → «Offset», «Regarding» → «About», «Auto Shut» → «Auto Off», «2.bmpSaving...» → «2.bmp saving...».
- **Верхнє меню в три ряди**: повні назви вміщаються і більше не перекривають підменю, зони дотику кнопок розширено.
- Рядок стану: короткі назви режимів синхронізації, які не переносяться.
- У «Про прилад» видно версію моду, наприклад «Версія (UA-мод 1.5)».

### Що додано в 1.3 (є і в 1.4, 1.5)
- **Генератор до 5 МГц** для всіх форм, крім синуса (синус, як і раніше, до 10 МГц). Заводська прошивка мовчки обрізає несинусоїдні форми до 2 МГц.
  - **Помаранчева частота зі знаком «!»** (наприклад «4.4!») означає: частота вища за 2 МГц, і форма сигналу вже **спотворюється**. Причина апаратна: ЦАП генератора (приблизно 50 млн точок/с) не встигає точно відтворити форму. Частота при цьому точна.
  - Реальні межі за моїми вимірами: прямокутник придатний приблизно до 5 МГц, трикутник 3–5 МГц, півхвиля ~3 МГц, сходинки й повна хвиля впізнавані до 5 МГц. Вище 5 МГц несинусоїдні форми перетворюються на синус або сміття, тому далі межу не піднято.
- **Звук у режимі діода**: писк, коли показ нижче 0,05 В (замкнені щупи), тим самим звуком, що й у прозвонці. Як і прозвонка, пищить навіть при нульовій гучності, бо це сигнал виміру, а не звук кнопок.
- **«OL»** без крапки при перевантаженні.

### Що додано в 1.4 (є і в 1.5)
- **Кнопка Menu в генераторі й мультиметрі.** У заводській прошивці вона працює лише в осцилографі. Тепер з генератора чи мультиметра вона відкриває те саме загальне меню, що й в осцилографі. Раніше для цього треба було спершу вийти «Назад».
- **Позначка прихованого фільтра.** Коли виміряна частота нижча за 4,19 МГц (2²² Гц), прилад згладжує сигнал (див. «Відомі заводські вади»). Тепер у цьому разі частота виділяється **бурштиновою плашкою з чорними цифрами** у двох місцях: у рядку «Част.» нижнього списку вимірювань і у верхньому полі F.
  - Саме число частоти правильне. Плашка попереджає інше: **форма сигналу на екрані згладжена**, тому фронтам, дзвону й викидам довіряти не можна.
  - Вище порога плашка зникає сама. Коли значення немає («***») або воно нульове, плашки теж немає.
  - Позначено лише те, на що фільтр доведено впливає. Лічильники «Фронти»/«Спади» перевірено: під фільтром вони рахують правильно, тому їх не позначено.
  - Колір обрано не випадково: червоний залишено для майбутньої позначки «дані некоректні / межа приладу», а бурштиновий фон з чорними цифрами читається на екрані найкраще.
- Верхнє поле **F показує частоту каналу-джерела синхронізації** (меню «Синхронізація» → CH1/CH2), а не того каналу, що зараз вибраний. Так у заводській прошивці; фільтр при цьому вирішує для кожного каналу окремо, за його власною частотою.

### Що додано в 1.5
- **Відносний вимір (REL) у мультиметрі.** **Довге натискання Run** запам'ятовує поточне показання як нуль, і далі прилад показує різницю відносно нього. Повторне довге натискання вимикає режим. Працює для **постійної напруги, опору, діода й ємності**.
  - Головне застосування: відняти опір щупів (замкніть щупи → довге Run) або власну ємність щупів і проводів.
  - Опорне значення переживає автоперемикання діапазону. Зміна функції вимикає режим.
  - Відносним стає лише велике число. Графік і «Макс.»/«Мін.» показують звичайні, абсолютні значення.
  - **Індикатор — світлодіод біля Run:** червоний, коли режим увімкнено. На сторінці мультиметра цей світлодіод тепер показує саме REL. **HOLD працює як раніше**, його видно на екрані (плашка HOLD), але світлодіод від нього вже не червоніє.
- **Кнопка Single.** У заводській прошивці вихід з одиночного режиму завжди перемикає запуск на «Авто». Тепер повертається режим, який був до натискання Single («Нормальний» чи «Авто»).
- **«Макс.» над «Мін.»** у панелі мультиметра.
- **Батарея:** вимір заряду тепер усереднюється, тож коротке просідання напруги під навантаженням більше не має спричиняти раптового вимкнення. Поріг вимкнення не змінено. Наразі поведінка лише стабілізована. Повне рішення потребує часу, тестів і додаткової інформації, і від неї залежатиме, чи буде другий етап.
- **Переклад меню «Дисплей»:** «Вигляд сигналу», «Яскрав. сигналу», «Згасання» (було «Післясвічення»), «Стерти». Підписи переносяться між словами, а не посеред слова.

### Що НЕ змінено
- **Вимірювання й калібрування** працюють за заводською логікою.
- Вади в ПЛІС (див. нижче) з боку мікроконтролера не виправити.

### Встановлення
**Що потрібно:** прилад, заряджений хоча б наполовину, USB-кабель, комп'ютер або телефон.

1. Завантажте з сайту FNIRSI **офіційну** прошивку V2.7.0.7 і розпакуйте архів. Потрібен файл `2D15P_V2.7.0.7_260826.bin`.
2. Відкрийте **Rom Patcher JS**: https://www.marcrobledo.com/RomPatcher.js/ (працює в браузері, і на телефоні теж, нічого встановлювати не треба).
3. У полі «ROM file» оберіть файл прошивки, у полі «Patch file» — патч потрібної версії (`...-1.2.bps`, `...-1.3.bps`, `...-1.4.bps` або `...-1.5.bps`), натисніть «Apply patch» і збережіть результат.
   *Альтернатива для комп'ютера: програма Floating IPS (Flips).*
4. Переконайтеся, що збережений файл називається **точно** `2D15P_V2.7.0.7_260826.bin`. Якщо браузер додав до назви щось своє, перейменуйте. Для перевірки: CRC32 результату — у таблиці вище.
5. На приладі (заводська англійська версія): кнопка **Menu** → **USB Sharing** → **ON**. Прилад з'явиться на комп'ютері як USB-диск.
6. Скопіюйте файл у папку **`Upgrade file`** на цьому диску.
7. Вимкніть і увімкніть прилад. Оновлення встановиться саме, файл після цього зникне з диска.
8. **Settings → Language → «Українська»**.

### Як повернути заводську прошивку
Встановлення **повністю оборотне**.
- **Звичайний спосіб:** прошийте офіційний файл V2.7.0.7 так само, як описано вище (кроки 5–7).
- **Якщо прилад не запускається:** вимкніть його, **затисніть великий регулятор і коротко натисніть кнопку живлення**. Запуститься завантажувач, який незалежно від основної прошивки відкриється на комп'ютері як USB-диск. Скопіюйте офіційний файл у папку `Upgrade file` і перезапустіть прилад.

### ⚠️ Старі прошивки й ревізії
FNIRSI підтвердили: 2D15P випускається в **різних апаратних версіях**, і прошивки для них **несумісні**. Неправильна прошивка робить прилад непрацездатним, і повернути його можна лише аварійним способом (див. вище). На моєму приладі (куплено у вересні 2026, з коробки V2.6.0.7) офіційна V1.2.0.6 саме так і зламала роботу. Без потреби не ставте старіші прошивки.

### Відомі заводські вади
**У ПЛІС (модом не виправити):**
- **Прихований фільтр нижче 4,19 МГц** (2²² Гц = 4 194 304 Гц). Коли виміряна частота сигналу нижча за поріг, прилад згладжує фронти, дзвін і викиди — так, ніби завжди ввімкнено обмеження смуги 20M. Ручне 20M накладає його вдруге. Частота, шпаруватість і рівні при цьому правильні (амплітуда на ~3 % нижча). FNIRSI підтвердили, що фільтр навмисний і в налаштуваннях не вимикається. Рішення ухвалюється окремо для кожного каналу за його частотою. **На практиці:** для пошуку викидів на ключах чи дзвону на повільних сигналах цьому приладу не довіряйте.
- **Частотомір помиляється** на похилих фронтах і малій амплітуді: наприклад, сходинки 3 МГц він показує як 181 кГц, повну хвилю 2 МГц — як 57,6 Гц. На чистому прямокутнику він точний. Перевіряйте частоту курсорами. Через це фільтр може вмикатися й на сигналах, справжня частота яких вища за поріг.
- **Нормальний запуск не тримає осцилограму.** Від звичайного цифрового осцилографа очікують, що в режимі «Нормальний» остання осцилограма лишається на екрані до наступного запуску. Тут вона згасає за налаштуванням «Згасання» (до 1.5 — «Післясвічення»): з найкоротшим зникає майже одразу, з довшим — поступово тьмяніє, а з «∞» взагалі не стирається, а накопичується. Вимкнути «Згасання» не можна (мінімум — Min), тож жодне значення не дає утримання останнього кадру. Вимірювання в стані очікування показують «***». Інструкція (с. 43) каже інакше: «Normal: Refresh waveform only when a trigger event occurs». Виправити це з боку мікроконтролера не можна: осцилограму на екран накладає й гасить ПЛІС, а в режимі «Нормальний» вона не зберігає останній запуск.

**Осцилограф:**
- **Глибина пам'яті (10K / 100K / 1M) не дає видимої різниці.** Це помітили й інші власники на форумі EEVblog. Прошивка мікроконтролера передає вибрану глибину в ПЛІС; що ПЛІС з нею робить — невідомо. Напис частоти дискретизації («…Sa/s») від глибини не залежить взагалі, тож за ним судити про глибину не можна. Тест 22.10.2026 на офіційній V2.7.0.7 (імпульс близько 1 мкс, 9,7 кГц, 10 мс/под): живий екран і зупинений розтягнутий кадр однакові для 10K і 1M, на 100 мкс/под в обох випадках губиться більшість імпульсів. Дані осцилограми прилад не зберігає (лише знімки екрана), тож скористатися глибиною користувач ніде не може.

**Генератор:**
- Заявлено 0–10 МГц для всіх форм, але заводська прошивка мовчки обмежує всі форми, крім синуса, до 2 МГц (у 1.3 — до 5 МГц з позначкою).
- Шум не має частоти, лише амплітуду; він однополярний (0…~1,1 В) з гострими піками вгору.
- Повна хвиля при амплітуді «1 В» має розмах лише ~0,44 В, з дном на ~0,46 В, а не на нулі.

**Мультиметр (у 1.2):** немає звуку в режимі діода; перевантаження показується як «.OL».

**Керування (у 1.2 і 1.3):** кнопка Menu працює лише в осцилографі. **(у 1.2–1.4):** вихід з режиму Single завжди вмикає «Авто».

**Батарея (у 1.2–1.4):** одне коротке просідання напруги нижче 3,68 В під навантаженням прилад запам'ятовує як 5% і вимикається, навіть якщо значок щойно показував дві поділки.

**Інше:**
- «Trig'd», «Stop», «Roll» та інші стани в рядку стану англійською в обох мовах (свідомо не перекладено: це загальноприйняті терміни).

### Безпека й підказки (чого немає в інструкції)
- В інструкції вказано **CAT I 300 В** і ступінь забруднення 1 на весь прилад. Тобто мережу офіційно міряти не можна, хоча мультиметр має діапазони 750 В змінної і 1000 В постійної.
- **«Земля» CH1 і CH2 спільна.** «Крокодили» обох щупів — лише в одну точку, інакше буде замикання через прилад.
- **Металева провушина зліва внизу** на передній панелі — вивід калібрування щупа, прямокутник 1 кГц.
- Обидва щупи в моїй коробці були **перекомпенсовані**. Перед вимірами фронтів налаштуйте їх на виводі калібрування.

### Відмова від відповідальності
Мод перевірено на одному приладі. Використовуєте на власний ризик. Автор не пов'язаний з FNIRSI. Відгуки й повідомлення про помилки — через розділ Issues цього репозиторію.

---

## English

> ⚠️ **For firmware V2.7.0.7 only** (`2D15P_V2.7.0.7_260826.bin`, CRC32 `B43E8C2D`).
> The patch checks the checksum and **will refuse** any other version. Do not try to bypass this: the changes target exact addresses of this version, and on other firmware the device may fail to boot.

### Which version
| | **1.2** | **1.3** | **1.4** | **1.5** |
|---|---|---|---|---|
| Ukrainian language and corrected English | ✓ | ✓ | ✓ | ✓ |
| Generator: non-sine waveforms up to **5 MHz** (stock limit 2 MHz) | — | ✓ | ✓ | ✓ |
| Beep in diode mode | — | ✓ | ✓ | ✓ |
| "OL" instead of ".OL" | — | ✓ | ✓ | ✓ |
| **Menu** key works in the generator and multimeter | — | — | ✓ | ✓ |
| Hidden-filter marker (frequency below 4.19 MHz) | — | — | ✓ | ✓ |
| Relative measurement (REL) in the multimeter | — | — | — | ✓ |
| **Single** key restores the previous trigger mode | — | — | — | ✓ |
| Multimeter: "Max" above "Min" | — | — | — | ✓ |
| Battery: no sudden shutdowns from voltage dips | — | — | — | ✓ |
| Patch file | `2D15P_V2.7.0.7_UA-mod-1.2.bps` | `2D15P_V2.7.0.7_UA-mod-1.3.bps` | `2D15P_V2.7.0.7_UA-mod-1.4.bps` | `2D15P_V2.7.0.7_UA-mod-1.5.bps` |
| Result CRC32 | `3DD5A6F0` | `CA67F6A9` | `BA028F8D` | `5CF4B48D` |

- **1.2** — translation only, device logic is stock. This version is frozen: it will change only for a critical translation bug.
- **1.3** — translation plus fixes that change device behavior (generator, multimeter).
- **1.4** — everything in 1.3, plus easier navigation (Menu) and an honest marker when the scope smooths the signal.
- **1.5** — everything in 1.4, plus relative measurement in the multimeter, the Single key fix, a more stable battery reading and translation fixes.
- Older versions stay available: new releases come out alongside them, not instead of them. Pick the one you need.
- **All patches apply to the stock V2.7.0.7**, not on top of each other. Do not apply a newer version over an already patched older one.

### What's done (both versions)
| | |
|---|---|
| UI strings translated | **115** + 9 outside the language tables |
| English strings corrected | **29** |
| Glyphs added to fonts | **74** characters × **6** fonts = **444** glyphs |
| Menu layout changes | **3**-row menu + **13** touch maps |
| Patch content | own changes only, no FNIRSI code |

- **Ukrainian language** replaces Chinese (language menu: «Українська» / «English»). After a factory reset the device starts in Ukrainian.
- **Cyrillic in all six device fonts**, matched to the stock Latin height and weight (Fixel typeface).
- **Corrected English**, e.g. "Level" → "Horizontal", "Ramp" → "Triangle", "Skew" → "Offset", "Regarding" → "About", "Auto Shut" → "Auto Off", "2.bmpSaving..." → "2.bmp saving...".
- **Three-row top menu**: full labels fit and no longer cover the submenu; touch zones enlarged.
- About page shows the mod version, e.g. "Version (UA mod 1.5)".

### New in 1.3 (also in 1.4, 1.5)
- **Generator up to 5 MHz** for all waveforms except sine (sine stays at 10 MHz). The stock firmware silently limits non-sine waveforms to 2 MHz.
  - **Orange frequency with "!"** (e.g. "4.4!") means: the frequency is above 2 MHz and the waveform shape is **distorted**. The reason is hardware: the generator DAC (about 50 MSa/s) cannot reproduce the shape exactly. The frequency itself is accurate.
  - Usable limits from my measurements: square up to about 5 MHz, triangle 3–5 MHz, half wave ~3 MHz, staircase and full wave recognizable up to 5 MHz. Above 5 MHz non-sine waveforms turn into a sine or garbage, so the limit is not raised further.
- **Beep in diode mode** when the reading is below 0.05 V (shorted probes), with the same sound as continuity. Like continuity, it beeps even at zero volume, because it is a measurement signal, not a key click.
- **"OL"** without the dot on overload.

### New in 1.4 (also in 1.5)
- **Menu key in the generator and multimeter.** In the stock firmware it only works in the scope. Now, from the generator or multimeter, it opens the same general menu as in the scope. Before, you had to press Back first.
- **Hidden-filter marker.** When the measured frequency is below 4.19 MHz (2²² Hz), the scope smooths the signal (see "Known stock issues"). In that case the frequency is now highlighted with an **amber plate and black digits** in two places: the "Freq" row of the measurement list and the top F field.
  - The frequency value itself is correct. The plate warns about something else: **the waveform on screen is smoothed**, so edges, ringing and overshoot cannot be trusted.
  - Above the threshold the plate disappears by itself. When there is no value ("***") or it is zero, there is no plate either.
  - Only what the filter is proven to affect is marked. The rising/falling edge counters were checked: they count correctly under the filter, so they are not marked.
  - The colour is deliberate: red is reserved for a future "invalid data / device limit" marker, and amber with black digits reads best on this screen.
- The top **F field shows the frequency of the trigger source channel** (Trigger menu → CH1/CH2), not of the currently selected channel. This is stock behavior; the filter itself decides per channel, from that channel's own frequency.

### New in 1.5
- **Relative measurement (REL) in the multimeter.** **Long press Run** stores the current reading as zero, and the display then shows the difference from it. Another long press turns it off. Works for **DC voltage, resistance, diode and capacitance**.
  - Main use: subtract the probe resistance (short the probes → long Run), or the stray capacitance of probes and leads.
  - The reference survives auto-ranging. Changing the function turns REL off.
  - Only the large reading becomes relative. The graph and "Max"/"Min" keep showing normal, absolute values.
  - **Indicator: the LED next to Run** is red while REL is on. On the multimeter page this LED now shows REL. **HOLD works as before** and is shown on screen (HOLD plate), but it no longer turns the LED red.
- **Single key.** In the stock firmware, leaving Single mode always switches the trigger to Auto. Now the mode that was active before Single (Normal or Auto) is restored.
- **"Max" above "Min"** in the multimeter panel.
- **Battery:** the charge reading is now averaged, so a short voltage dip under load should no longer cause a sudden shutdown. The shutdown threshold is unchanged. For now the behaviour is only stabilised. A complete solution needs time, tests and more information, and whether a second stage follows depends on it.
- **Ukrainian Display menu:** clearer labels; line breaks now fall between words.

### What's NOT changed
Measurement and calibration logic are stock. FPGA issues (below) cannot be fixed from the MCU side.

### Installation
1. Download the **official** V2.7.0.7 firmware from FNIRSI and unzip it (`2D15P_V2.7.0.7_260826.bin`).
2. Open **Rom Patcher JS**: https://www.marcrobledo.com/RomPatcher.js/ (runs in the browser, phones included). Alternative: Floating IPS (Flips).
3. Select the firmware as "ROM file" and the patch of your chosen version (`...-1.2.bps`, `...-1.3.bps`, `...-1.4.bps` or `...-1.5.bps`) as "Patch file", click "Apply patch", save the result.
4. Make sure the result is named **exactly** `2D15P_V2.7.0.7_260826.bin` (CRC32 in the table above).
5. On the device: **Menu** button → **USB Sharing** → **ON**, copy the file into the **`Upgrade file`** folder, power cycle.
6. **Settings → Language → «Українська»** (or keep English).

### Reverting
Fully reversible. Flash the official V2.7.0.7 file the same way. If the device does not boot: power off, **hold the large knob and briefly press the power button** — the bootloader appears as a USB drive regardless of the main firmware.

### ⚠️ Old firmware and hardware versions
FNIRSI confirmed that the 2D15P exists in **different hardware versions** and their firmware is **not compatible**. The wrong firmware makes the device unresponsive, and only the emergency method above brings it back. On my unit (bought September 2026, shipped with V2.6.0.7) the official V1.2.0.6 did exactly that. Do not flash older firmware without a reason.

### Known stock issues
**In the FPGA (cannot be fixed by this mod):**
- **Hidden filter below 4.19 MHz** (2²² Hz = 4,194,304 Hz). When the measured frequency is below the threshold, the scope smooths edges, ringing and overshoot, as if the 20M bandwidth limit were always on. Turning 20M on by hand applies it a second time. Frequency, duty cycle and levels are correct (amplitude about 3 % lower). FNIRSI confirmed the filter is intentional and cannot be turned off in the settings. The decision is made per channel from its own frequency. **In practice:** do not trust this scope for switching spikes or ringing on slow signals.
- **The frequency counter fails** on slow edges and small amplitudes: e.g. a 3 MHz staircase is shown as 181 kHz, a 2 MHz full wave as 57.6 Hz. On a clean square wave it is accurate. Check frequency with the cursors. Because of this, the filter can also turn on for signals whose real frequency is above the threshold.
- **Normal trigger does not hold the trace.** On a typical digital scope, in Normal mode the last trace stays on screen until the next trigger. Here it fades according to the "Afterglow" setting: with the shortest setting it vanishes almost at once, with longer ones it dims gradually, and with "∞" it is never cleared but accumulates. Afterglow cannot be switched off (the minimum is Min), so no setting holds the last frame. Measurements show "***" while waiting. The manual (p. 43) says otherwise: "Normal: Refresh waveform only when a trigger event occurs". This cannot be fixed from the MCU side: the trace is drawn over the screen and faded by the FPGA, and in Normal mode the FPGA does not keep the last capture.

**Scope:**
- **Memory depth (10K / 100K / 1M) makes no visible difference.** Other owners on the EEVblog forum noticed this too. The MCU firmware does send the selected depth to the FPGA; what the FPGA does with it is unknown. The sample-rate label ("…Sa/s") does not depend on the depth at all, so it cannot be used to judge the depth. Test on 22.10.2026, official V2.7.0.7 (pulse about 1 µs, 9.7 kHz, 10 ms/div): the live screen and the stopped, stretched frame are the same for 10K and 1M; at 100 µs/div most pulses are lost in both cases. The device does not save waveform data (screenshots only), so the user cannot benefit from the depth anywhere.

**Generator:**
- Advertised as 0–10 MHz for all waveforms, but the stock firmware silently limits every waveform except sine to 2 MHz (5 MHz with a marker in 1.3).
- Noise has no frequency setting, only amplitude; it is unipolar (0 to ~1.1 V) with sharp peaks upward.
- Full wave at amplitude "1 V" has only ~0.44 V peak-to-peak, with the bottom at ~0.46 V instead of 0 V.

**Multimeter (in 1.2):** no beep in diode mode; overload shown as ".OL".

**Controls (in 1.2 and 1.3):** the Menu key only works in the scope. **(in 1.2–1.4):** leaving Single mode always switches to Auto.

**Battery (in 1.2–1.4):** a single short voltage dip below 3.68 V under load is stored as 5% and the device shuts down, even if the icon showed two bars a moment before.

**Other:** "Trig'd", "Stop", "Roll" and other status-bar states remain English in both languages (kept on purpose: these are standard terms).

### Safety and tips (not in the manual)
- The manual gives **CAT I 300 V** and pollution degree 1 for the whole device. So officially you cannot measure mains, although the meter has 750 V AC and 1000 V DC ranges.
- **CH1 and CH2 grounds are common.** Clip both ground leads to the same point only, otherwise you create a short through the scope.
- **The metal lug at the lower left** of the front panel is the probe calibration output, 1 kHz square wave.
- Both probes in my box were **overcompensated**. Adjust them on the calibration output before measuring edges.

### Disclaimer
Tested on one unit. Use at your own risk. Not affiliated with FNIRSI. Please report issues via the Issues tab.

---

## Історія версій / Changelog
- **1.5** — відносний вимір (REL) у мультиметрі: довге натискання Run, індикатор — світлодіод біля Run; Single повертає попередній режим запуску; «Макс.» над «Мін.»; усереднення виміру батареї проти раптових вимкнень; переклад меню «Дисплей» («Згасання» замість «Післясвічення»). / Relative measurement (REL) in the multimeter: long press Run, the LED next to Run is the indicator; Single restores the previous trigger mode; "Max" above "Min"; averaged battery reading against sudden shutdowns; Ukrainian Display menu labels.
- **1.4** — кнопка Menu в генераторі й мультиметрі; бурштинова плашка на частоті, коли діє прихований фільтр (нижче 4,19 МГц), у списку вимірювань і в полі F; до відомих вад додано нормальний запуск («Післясвічення») і глибину пам'яті. / Menu key in the generator and multimeter; amber plate on the frequency while the hidden filter is active (below 4.19 MHz), in the measurement list and the F field; Normal trigger ("Afterglow") and memory depth added to known issues.
- **1.3** — генератор до 5 МГц для несинусоїдних форм з позначкою понад 2 МГц (помаранчевий колір і «!»); звук у режимі діода; «OL» замість «.OL»; оновлено опис заводських вад. / Generator up to 5 MHz for non-sine waveforms with a marker above 2 MHz (orange and "!"); beep in diode mode; "OL" instead of ".OL"; stock issues section updated.
- **1.2** — виправлено екранну клавіатуру генератора в режимі «Прямокутник»: довгий підпис «Заповнення» зсував її за лівий край екрана, і вона закривалася від будь-якого натискання. Підпис скорочено до «Запов.». / Fixed the generator keypad in Square mode: the long Ukrainian «Duty» label pushed it past the left screen edge, so any tap closed it. The label is shortened.
- **1.1** — повернуто значки, вбудовані в шрифти (кошик на кнопці видалення в перегляді знімка та два значки попереджень), які версія 1.0 помилково прибрала разом з ієрогліфами. / Restored icons embedded in the fonts (trash can on the delete button in picture view and two warning icons) that 1.0 removed by mistake together with the CJK glyphs.
- **1.0** — перший випуск. / First release.

---

## Ліцензія / License
- Мої власні зміни в цьому репозиторії (патчі, інструменти, переклади й виправлення) поширюються за ліцензією **GPL-3.0**, див. `LICENSE`.
  My own changes in this repository (patches, tools, translations and corrections) are licensed under **GPL-3.0**, see `LICENSE`.
- **Виняток для FNIRSI:** FNIRSI можуть використовувати переклади, виправлення англійської та будь-який код з цього проєкту у своїй офіційній прошивці без обмежень.
  **Exception for FNIRSI:** FNIRSI may use the translations, English corrections and any code from this project in their official firmware without restrictions.
- Кириличні гліфи — з гарнітури **Fixel Text** © 2023 MacPaw Way Ltd., ліцензія **SIL Open Font License 1.1** (`OFL-Fixel.txt`), перетворено в растровий формат приладу.
  Cyrillic glyphs rendered from **Fixel Text** © 2023 MacPaw Way Ltd., **SIL Open Font License 1.1** (`OFL-Fixel.txt`), converted to the device's bitmap format.
- Прошивка FNIRSI не входить до репозиторію, її треба завантажити з сайту FNIRSI. Патч містить лише зміни.
  The original firmware is © FNIRSI and must be obtained from FNIRSI. The patch contains only the changes.

## Дивіться також / See also
- [Тема 2D15P на форумі EEVblog](https://www.eevblog.com/forum/testgear/new-handheld-dsodmm-fnirsi-2d15p-100mhz500msps-(september-2025)/) — обговорення приладу, подробиці тестів і фото. / [2D15P thread on the EEVblog forum](https://www.eevblog.com/forum/testgear/new-handheld-dsodmm-fnirsi-2d15p-100mhz500msps-(september-2025)/) — discussion of the device, test details and photos.
- [giray/fnirsi-2d15p-mod](https://github.com/giray/fnirsi-2d15p-mod) — інший мод 2D15P: запуск одразу в мультиметр, турецька / німецька / нідерландська мови. Звідти ж ідея кнопки Menu поза осцилографом (у 1.4) і відносного виміру REL разом з частиною карти кнопок і полів мультиметра (у 1.5); обидва реалізовано власним кодом. / Another 2D15P mod: boots into the multimeter, Turkish / German / Dutch UI. The ideas of the Menu key outside the scope (1.4) and of relative measurement (REL), with part of the key and multimeter field map (1.5), also come from there; both implemented with my own code.
