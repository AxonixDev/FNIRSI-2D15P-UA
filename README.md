# FNIRSI 2D15P — UA mod 1.2 / 1.3

Неофіційна модифікація прошивки осцилографа **FNIRSI 2D15P**: **українська мова інтерфейсу**, **виправлений англійський переклад** і (у версії 1.3) **виправлення частини заводських вад**.
Unofficial modification of the **FNIRSI 2D15P** firmware: **Ukrainian interface language**, **corrected English translation** and (in 1.3) **fixes for some stock issues**. *English version below.*

> ⚠️ **Лише для прошивки V2.7.0.7** (файл `2D15P_V2.7.0.7_260826.bin`, CRC32 `B43E8C2D`).
> Патч перевіряє контрольну суму і **не застосується** до іншої версії. Не намагайтеся обійти цю перевірку: зміни прив'язані до точних адрес саме цієї версії, і на іншій прошивці прилад може не запуститися.

---

## Українською

### Яку версію обрати
| | **1.2** | **1.3** |
|---|---|---|
| Українська мова й виправлена англійська | ✓ | ✓ |
| Генератор: несинусоїдні форми до **5 МГц** (заводська межа 2 МГц) | — | ✓ |
| Звук у режимі діода | — | ✓ |
| «OL» замість «.OL» | — | ✓ |
| Файл патча | `2D15P_V2.7.0.7_UA-mod-1.2.bps` | `2D15P_V2.7.0.7_UA-mod-1.3.bps` |
| CRC32 результату | `3DD5A6F0` | `CA67F6A9` |

- **1.2** — лише переклад, логіка приладу заводська. Ця версія заморожена: змінюватиметься тільки при критичній помилці в перекладі.
- **1.3** — переклад плюс виправлення, які змінюють поведінку приладу (генератор, мультиметр).
- **Обидва патчі накладаються на заводську V2.7.0.7**, а не один на інший. Не накладайте 1.3 поверх уже пропатченої 1.2.

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
- У «Про прилад» видно версію моду, наприклад «Версія (UA-мод 1.3)».

### Що додано в 1.3
- **Генератор до 5 МГц** для всіх форм, крім синуса (синус, як і раніше, до 10 МГц). Заводська прошивка мовчки обрізає несинусоїдні форми до 2 МГц.
  - **Помаранчева частота зі знаком «!»** (наприклад «4.4!») означає: частота вища за 2 МГц, і форма сигналу вже **спотворюється**. Причина апаратна: ЦАП генератора (приблизно 50 млн точок/с) не встигає точно відтворити форму. Частота при цьому точна.
  - Реальні межі за моїми вимірами: прямокутник придатний приблизно до 5 МГц, трикутник 3–5 МГц, півхвиля ~3 МГц, сходинки й повна хвиля впізнавані до 5 МГц. Вище 5 МГц несинусоїдні форми перетворюються на синус або сміття, тому далі межу не піднято.
- **Звук у режимі діода**: писк, коли показ нижче 0,05 В (замкнені щупи), тим самим звуком, що й у прозвонці. Як і прозвонка, пищить навіть при нульовій гучності, бо це сигнал виміру, а не звук кнопок.
- **«OL»** без крапки при перевантаженні.

### Що НЕ змінено
- **Вимірювання й калібрування** працюють за заводською логікою.
- Вади в ПЛІС (див. нижче) з боку мікроконтролера не виправити.

### Встановлення
**Що потрібно:** прилад, заряджений хоча б наполовину, USB-кабель, комп'ютер або телефон.

1. Завантажте з сайту FNIRSI **офіційну** прошивку V2.7.0.7 і розпакуйте архів. Потрібен файл `2D15P_V2.7.0.7_260826.bin`.
2. Відкрийте **Rom Patcher JS**: https://www.marcrobledo.com/RomPatcher.js/ (працює в браузері, і на телефоні теж, нічого встановлювати не треба).
3. У полі «ROM file» оберіть файл прошивки, у полі «Patch file» — патч потрібної версії (`...-1.2.bps` або `...-1.3.bps`), натисніть «Apply patch» і збережіть результат.
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
- **Частотомір помиляється** на похилих фронтах і малій амплітуді: наприклад, сходинки 3 МГц він показує як 181 кГц, повну хвилю 2 МГц — як 57,6 Гц. На чистому прямокутнику він точний. Перевіряйте частоту курсорами.

**Генератор:**
- Заявлено 0–10 МГц для всіх форм, але заводська прошивка мовчки обмежує всі форми, крім синуса, до 2 МГц (у 1.3 — до 5 МГц з позначкою).
- Шум не має частоти, лише амплітуду; він однополярний (0…~1,1 В) з гострими піками вгору.
- Повна хвиля при амплітуді «1 В» має розмах лише ~0,44 В, з дном на ~0,46 В, а не на нулі.

**Мультиметр (у 1.2):** немає звуку в режимі діода; перевантаження показується як «.OL».

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
| | **1.2** | **1.3** |
|---|---|---|
| Ukrainian language and corrected English | ✓ | ✓ |
| Generator: non-sine waveforms up to **5 MHz** (stock limit 2 MHz) | — | ✓ |
| Beep in diode mode | — | ✓ |
| "OL" instead of ".OL" | — | ✓ |
| Patch file | `2D15P_V2.7.0.7_UA-mod-1.2.bps` | `2D15P_V2.7.0.7_UA-mod-1.3.bps` |
| Result CRC32 | `3DD5A6F0` | `CA67F6A9` |

- **1.2** — translation only, device logic is stock. This version is frozen: it will change only for a critical translation bug.
- **1.3** — translation plus fixes that change device behavior (generator, multimeter).
- **Both patches apply to the stock V2.7.0.7**, not on top of each other. Do not apply 1.3 over an already patched 1.2.

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
- About page shows the mod version, e.g. "Version (UA mod 1.3)".

### New in 1.3
- **Generator up to 5 MHz** for all waveforms except sine (sine stays at 10 MHz). The stock firmware silently limits non-sine waveforms to 2 MHz.
  - **Orange frequency with "!"** (e.g. "4.4!") means: the frequency is above 2 MHz and the waveform shape is **distorted**. The reason is hardware: the generator DAC (about 50 MSa/s) cannot reproduce the shape exactly. The frequency itself is accurate.
  - Usable limits from my measurements: square up to about 5 MHz, triangle 3–5 MHz, half wave ~3 MHz, staircase and full wave recognizable up to 5 MHz. Above 5 MHz non-sine waveforms turn into a sine or garbage, so the limit is not raised further.
- **Beep in diode mode** when the reading is below 0.05 V (shorted probes), with the same sound as continuity. Like continuity, it beeps even at zero volume, because it is a measurement signal, not a key click.
- **"OL"** without the dot on overload.

### What's NOT changed
Measurement and calibration logic are stock. FPGA issues (below) cannot be fixed from the MCU side.

### Installation
1. Download the **official** V2.7.0.7 firmware from FNIRSI and unzip it (`2D15P_V2.7.0.7_260826.bin`).
2. Open **Rom Patcher JS**: https://www.marcrobledo.com/RomPatcher.js/ (runs in the browser, phones included). Alternative: Floating IPS (Flips).
3. Select the firmware as "ROM file" and the patch of your chosen version (`...-1.2.bps` or `...-1.3.bps`) as "Patch file", click "Apply patch", save the result.
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
- **The frequency counter fails** on slow edges and small amplitudes: e.g. a 3 MHz staircase is shown as 181 kHz, a 2 MHz full wave as 57.6 Hz. On a clean square wave it is accurate. Check frequency with the cursors.

**Generator:**
- Advertised as 0–10 MHz for all waveforms, but the stock firmware silently limits every waveform except sine to 2 MHz (5 MHz with a marker in 1.3).
- Noise has no frequency setting, only amplitude; it is unipolar (0 to ~1.1 V) with sharp peaks upward.
- Full wave at amplitude "1 V" has only ~0.44 V peak-to-peak, with the bottom at ~0.46 V instead of 0 V.

**Multimeter (in 1.2):** no beep in diode mode; overload shown as ".OL".

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
- [giray/fnirsi-2d15p-mod](https://github.com/giray/fnirsi-2d15p-mod) — інший мод 2D15P: запуск одразу в мультиметр, турецька / німецька / нідерландська мови. / Another 2D15P mod: boots into the multimeter, Turkish / German / Dutch UI.
