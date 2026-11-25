# FNIRSI 2D15P — UA mod 1.2 / 1.3 / 1.4 / 1.5 / 1.6

Unofficial modification of the **FNIRSI 2D15P** firmware: **Ukrainian interface language**, **corrected English translation** and (in 1.3–1.6) **fixes for some stock issues and small new features**.
Неофіційна модифікація прошивки осцилографа **FNIRSI 2D15P**: **українська мова інтерфейсу**, **виправлений англійський переклад** і (у версіях 1.3–1.6) **виправлення частини заводських вад і невеликі нові функції**.

---

## English

> ⚠️ **For firmware V2.7.0.7 only** (`2D15P_V2.7.0.7_260826.bin`, CRC32 `B43E8C2D`).
> The patch checks the checksum and **will refuse** any other version. Do not try to bypass this: the changes target exact addresses of this version, and on other firmware the device may fail to boot.

### Which version
| | **1.2** | **1.3** | **1.4** | **1.5** | **1.6** |
|---|---|---|---|---|---|
| Ukrainian language and corrected English | ✓ | ✓ | ✓ | ✓ | ✓ |
| Generator: non-sine waveforms up to **5 MHz** (stock limit 2 MHz) | — | ✓ | ✓ | ✓ | ✓ |
| Beep in diode mode | — | ✓ | ✓ | ✓ | ✓ |
| "OL" instead of ".OL" | — | ✓ | ✓ | ✓ | ✓ |
| **Menu** key works in the generator and multimeter | — | — | ✓ | ✓ | ✓ |
| Hidden-filter marker (frequency below 4.19 MHz) | — | — | ✓ | ✓ | ✓ |
| Relative measurement (REL) in the multimeter | — | — | — | ✓ | ✓ |
| **Single** key restores the previous trigger mode | — | — | — | ✓ | ✓ |
| Multimeter: "Max" above "Min" | — | — | — | ✓ | ✓ |
| Battery: no sudden shutdowns from voltage dips | — | — | — | ✓ | ✓ |
| Generator controlled with the **knobs** | — | — | — | — | ✓ |
| Battery: **percentage** instead of the icon, lightning while charging | — | — | — | — | ✓ |
| USB drive page: the **ON** button is framed | — | — | — | — | ✓ |
| Long press of **Menu** switches oscilloscope / multimeter / generator | — | — | — | — | ✓ |
| Patch file | `…-1.2.bps` | `…-1.3.bps` | `…-1.4.bps` | `…-1.5.bps` | `…-1.6.bps` |
| Result CRC32 | `3DD5A6F0` | `CA67F6A9` | `BA028F8D` | `5CF4B48D` | `76208FBF` |

Full patch names: `2D15P_V2.7.0.7_UA-mod-<version>.bps`.

- **1.2** — translation only, device logic is stock. This version is frozen: it will change only for a critical translation bug.
- **1.3** — translation plus fixes that change device behavior (generator, multimeter).
- **1.4** — everything in 1.3, plus easier navigation (Menu) and an honest marker when the scope smooths the signal.
- **1.5** — everything in 1.4, plus relative measurement in the multimeter, the Single key fix, a more stable battery reading and translation fixes.
- **1.6** — everything in 1.5, plus generator control with the knobs, switching instruments with a long press of Menu, battery percentage measured on a real discharge curve, and a framed ON button on the USB drive page.
- Older versions stay available: new releases come out alongside them, not instead of them. Pick the one you need.
- **All patches apply to the stock V2.7.0.7**, not on top of each other. Do not apply a newer version over an already patched older one.

### Project status
The project is alive, but new releases will come out more slowly. The quick changes are already done; what is left takes much longer.
- Some ideas need test equipment. It has to be found, bought with my own money and then waited for until it is delivered.
- Some depend on information I am still waiting for.
- Many need long tests: a discharge curve alone means hours of continuous measurement and then building tables from it.
- Not every idea works out. Sometimes the tests only show that it is not acceptable, and weeks of work end without a release.

So a long pause between versions does not mean the project is abandoned — I keep working on it as time, resources and the complexity of each task allow.

I collect ideas and requests everywhere: Issues, forums and chats. I read everything, but what to implement and when is my decision, based on usefulness and complexity.

I do not accept money donations. If you want to help the project with test equipment, contact me. A specific feature can also be moved up: for a fee I will put other tasks aside and do it sooner. You pay for my time, not for exclusivity — the feature will still be published in this repository for everyone under GPL-3.0.

**Contact:** questions, requests and bug reports — via the Issues tab. Equipment for testing or a paid feature — by e-mail: [axonixdev.contact@gmail.com](mailto:axonixdev.contact@gmail.com).

### What's done (all versions)
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
- About page shows the mod version, e.g. "Version (UA mod 1.6)".

### New in 1.3 (also in 1.4–1.6)
- **Generator up to 5 MHz** for all waveforms except sine (sine stays at 10 MHz). The stock firmware silently limits non-sine waveforms to 2 MHz.
  - **Orange frequency with "!"** (e.g. "4.4!") means: the frequency is above 2 MHz and the waveform shape is **distorted**. The reason is hardware: the generator DAC (about 50 MSa/s) cannot reproduce the shape exactly. The frequency itself is accurate.
  - Usable limits from my measurements: square up to about 5 MHz, triangle 3–5 MHz, half wave ~3 MHz, staircase and full wave recognizable up to 5 MHz. Above 5 MHz non-sine waveforms turn into a sine or garbage, so the limit is not raised further.
- **Beep in diode mode** when the reading is below 0.05 V (shorted probes), with the same sound as continuity. Like continuity, it beeps even at zero volume, because it is a measurement signal, not a key click.
- **"OL"** without the dot on overload.

### New in 1.4 (also in 1.5, 1.6)
- **Menu key in the generator and multimeter.** In the stock firmware it only works in the scope. Now, from the generator or multimeter, it opens the same general menu as in the scope. Before, you had to press Back first.
- **Hidden-filter marker.** When the measured frequency is below 4.19 MHz (2²² Hz), the scope smooths the signal (see "Known stock issues"). In that case the frequency is now highlighted with an **amber plate and black digits** in two places: the "Freq" row of the measurement list and the top F field.
  - The frequency value itself is correct. The plate warns about something else: **the waveform on screen is smoothed**, so edges, ringing and overshoot cannot be trusted.
  - Above the threshold the plate disappears by itself. When there is no value ("***") or it is zero, there is no plate either.
  - Only what the filter is proven to affect is marked. The rising/falling edge counters were checked: they count correctly under the filter, so they are not marked.
  - The colour is deliberate: red is reserved for a future "invalid data / device limit" marker, and amber with black digits reads best on this screen.
- The top **F field shows the frequency of the trigger source channel** (Trigger menu → CH1/CH2), not of the currently selected channel. This is stock behavior; the filter itself decides per channel, from that channel's own frequency.

### New in 1.5 (also in 1.6)
- **Relative measurement (REL) in the multimeter.** **Long press Run** stores the current reading as zero, and the display then shows the difference from it. Another long press turns it off. Works for **DC voltage, resistance, diode and capacitance**.
  - Main use: subtract the probe resistance (short the probes → long Run), or the stray capacitance of probes and leads.
  - The reference survives auto-ranging. Changing the function turns REL off.
  - Only the large reading becomes relative. The graph and "Max"/"Min" keep showing normal, absolute values.
  - **Indicator: the LED next to Run** is red while REL is on. On the multimeter page this LED now shows REL. **HOLD works as before** and is shown on screen (HOLD plate), but it no longer turns the LED red.
- **Single key.** In the stock firmware, leaving Single mode always switches the trigger to Auto. Now the mode that was active before Single (Normal or Auto) is restored.
- **"Max" above "Min"** in the multimeter panel.
- **Battery:** the charge reading is averaged, so a short voltage dip under load should no longer cause a sudden shutdown. The shutdown threshold is unchanged.
- **Ukrainian Display menu:** clearer labels; line breaks now fall between words.

### New in 1.6
- **Generator controlled with the knobs** (requested in GitHub issue #3). On the generator page:
  - **large knob, press** — select the row: frequency → amplitude → duty cycle (only the rows the waveform has). The selected row has a blue frame;
  - **small top knob, turn** — change the value of the selected row;
  - **small top knob, press** — frequency step, in a loop: 1 Hz … 1 MHz. The current step is shown under the rows ("Step: 1 kHz").
  - Limits are the same as with the on-screen keypad (5 MHz for non-sine waveforms, 10 MHz for sine). Amplitude and duty cycle change exactly like with the on-screen arrows.
- **Long press of Menu switches the instrument** in a loop: oscilloscope → multimeter → generator → oscilloscope. A short press works as before. Handy when you work in gloves and cannot use the touchscreen (requested by a user in the WhatsApp group). It works on the three instrument pages, including the oscilloscope with its menu open; on other pages (settings, picture view) a long press does nothing.
- **Battery percentage instead of the icon** (scope, multimeter and generator pages).
  - **White number** — charge in %, **red** below 20 %, **yellow lightning** while charging.
  - The percentage comes from a **discharge curve measured on the device** (24.11.2026), not from the stock 10 % steps. The stock steps lag: "100" stays until about 93 %, "90" until about 84 %.
  - For the first minute after power-on or unplugging the charger the number follows the real value (the battery "settles" after charging). After that, **on battery it never goes up** and falls by at most 1 % per 15 s (1 % per 3 s if the real value is 5 % or more below). A short load (touching the screen, switching the generator on) moves it by 1 % at most, instead of jumping by 7–10 %.
  - 0 % is the stock shutdown threshold (3.68 V, unchanged). The device switches itself off there.
  - **Runtime depends heavily on the load.** The curve was measured with one channel on and **the generator running at 1 V**: about **85 minutes** from full charge to shutdown. The generator takes its output power from the battery, so it is the biggest consumer; at **3 V** the battery drains much faster. With the scope or multimeter only (no generator) the device runs considerably longer, and the percentage in the middle of the range may read a few percent high.
- **USB drive page: the ON button is framed** with a blue outline. In the stock firmware it is a grey label that does not look like a button.

### What's NOT changed
Measurement and calibration logic are stock. FPGA issues (below) cannot be fixed from the MCU side.

### Installation
1. Download the **official** V2.7.0.7 firmware from FNIRSI and unzip it (`2D15P_V2.7.0.7_260826.bin`).
2. Open **Rom Patcher JS**: https://www.marcrobledo.com/RomPatcher.js/ (runs in the browser, phones included). Alternative: Floating IPS (Flips).
3. Select the firmware as "ROM file" and the patch of your chosen version (`...-1.2.bps` … `...-1.6.bps`) as "Patch file", click "Apply patch", save the result.
4. Make sure the result is named **exactly** `2D15P_V2.7.0.7_260826.bin` (CRC32 in the table above).
5. On the device: **Menu** button → **USB Sharing** → **ON**, copy the file into the **`Upgrade file`** folder, power cycle.
6. **Settings → Language → «Українська»** (or keep English). The language setting is kept between updates.

### Reverting
Fully reversible. Flash the official V2.7.0.7 file the same way. If the device does not boot: power off, **hold the large knob and briefly press the power button** — the bootloader appears as a USB drive regardless of the main firmware.

### ⚠️ Old firmware and hardware versions
FNIRSI confirmed that the 2D15P exists in **different hardware versions** and their firmware is **not compatible**. According to FNIRSI, the version is identified by the **first digit of the firmware the device was shipped with**: "1…" means the first generation, "2…" the second. Flash only firmware of your own generation. This mod is for V2.7.0.7, i.e. for second-generation devices. If something goes wrong, use the emergency method above.

If you have a **first-generation** device and want the mod's features on it, please say so in Issues. I have not come across one myself, but they are said to exist, and the mod has not been made or tested for them.

### Known stock issues
**In the FPGA (cannot be fixed by this mod):**
- **Hidden filter below 4.19 MHz** (2²² Hz = 4,194,304 Hz). When the measured frequency is below the threshold, the scope smooths edges, ringing and overshoot, as if the 20M bandwidth limit were always on. Turning 20M on by hand applies it a second time. Frequency, duty cycle and levels are correct (amplitude about 3 % lower). FNIRSI confirmed the filter is intentional and cannot be turned off in the settings. The decision is made per channel from its own frequency. **In practice:** do not trust this scope for switching spikes or ringing on slow signals.
- **The frequency counter fails** on slow edges and small amplitudes: e.g. a 3 MHz staircase is shown as 181 kHz, a 2 MHz full wave as 57.6 Hz. On a clean square wave it is accurate. Check frequency with the cursors. Probably because of this, the filter may also turn on for signals whose real frequency is above the threshold (not confirmed).
- **Normal trigger does not hold the trace.** On a typical digital scope, in Normal mode the last trace stays on screen until the next trigger. Here it fades according to the "Afterglow" setting: with the shortest setting it vanishes almost at once, with longer ones it dims gradually, and with "∞" it is never cleared but accumulates. Afterglow cannot be switched off (the minimum is Min), so no setting holds the last frame. Measurements show "***" while waiting. The manual (p. 43) says otherwise: "Normal: Refresh waveform only when a trigger event occurs". This cannot be fixed from the MCU side: the trace is drawn over the screen and faded by the FPGA, so most likely it is the FPGA that does not keep the last capture in Normal mode.

**Scope:**
- **Memory depth (10K / 100K / 1M) makes no visible difference.** Other owners on the EEVblog forum noticed this too. The MCU firmware does send the selected depth to the FPGA; what the FPGA does with it is unknown. The sample-rate label ("…Sa/s") does not depend on the depth at all, so it cannot be used to judge the depth. Test on 22.10.2026, official V2.7.0.7 (pulse about 1 µs, 9.7 kHz, 10 ms/div): the live screen and the stopped, stretched frame are the same for 10K and 1M; at 100 µs/div most pulses are lost in both cases. The device does not save waveform data (screenshots only), so the user cannot benefit from the depth anywhere.

**Generator:**
- Advertised as 0–10 MHz for all waveforms, but the stock firmware silently limits every waveform except sine to 2 MHz (5 MHz with a marker in 1.3 and later).
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
- **Switch the generator off when you do not need it** — it drains the battery fastest.

### Disclaimer
Tested on one unit. Use at your own risk. Not affiliated with FNIRSI. Please report issues via the Issues tab.

---

## Українською

> ⚠️ **Лише для прошивки V2.7.0.7** (файл `2D15P_V2.7.0.7_260826.bin`, CRC32 `B43E8C2D`).
> Патч перевіряє контрольну суму і **не застосується** до іншої версії. Не намагайтеся обійти цю перевірку: зміни прив'язані до точних адрес саме цієї версії, і на іншій прошивці прилад може не запуститися.

### Яку версію обрати
| | **1.2** | **1.3** | **1.4** | **1.5** | **1.6** |
|---|---|---|---|---|---|
| Українська мова й виправлена англійська | ✓ | ✓ | ✓ | ✓ | ✓ |
| Генератор: несинусоїдні форми до **5 МГц** (заводська межа 2 МГц) | — | ✓ | ✓ | ✓ | ✓ |
| Звук у режимі діода | — | ✓ | ✓ | ✓ | ✓ |
| «OL» замість «.OL» | — | ✓ | ✓ | ✓ | ✓ |
| Кнопка **Menu** працює в генераторі й мультиметрі | — | — | ✓ | ✓ | ✓ |
| Позначка прихованого фільтра (частота нижче 4,19 МГц) | — | — | ✓ | ✓ | ✓ |
| Відносний вимір (REL) у мультиметрі | — | — | — | ✓ | ✓ |
| Кнопка **Single** повертає попередній режим запуску | — | — | — | ✓ | ✓ |
| Мультиметр: «Макс.» над «Мін.» | — | — | — | ✓ | ✓ |
| Батарея: без раптових вимкнень від просідання напруги | — | — | — | ✓ | ✓ |
| Керування генератором **ручками** | — | — | — | — | ✓ |
| Батарея: **відсотки** замість значка, блискавка під час заряджання | — | — | — | — | ✓ |
| Сторінка USB-диска: кнопка **«Увімк.»** у рамці | — | — | — | — | ✓ |
| Довге натискання **Menu** перемикає осцилограф / мультиметр / генератор | — | — | — | — | ✓ |
| Файл патча | `…-1.2.bps` | `…-1.3.bps` | `…-1.4.bps` | `…-1.5.bps` | `…-1.6.bps` |
| CRC32 результату | `3DD5A6F0` | `CA67F6A9` | `BA028F8D` | `5CF4B48D` | `76208FBF` |

Повні назви патчів: `2D15P_V2.7.0.7_UA-mod-<версія>.bps`.

- **1.2** — лише переклад, логіка приладу заводська. Ця версія заморожена: змінюватиметься тільки при критичній помилці в перекладі.
- **1.3** — переклад плюс виправлення, які змінюють поведінку приладу (генератор, мультиметр).
- **1.4** — усе з 1.3 плюс зручніше керування (Menu) і чесна позначка, коли прилад згладжує сигнал.
- **1.5** — усе з 1.4 плюс відносний вимір у мультиметрі, кнопка Single, стабільніша батарея і правки перекладу.
- **1.6** — усе з 1.5 плюс керування генератором ручками, перемикання приладів довгим натисканням Menu, відсотки заряду за виміряною кривою розряду і рамка навколо кнопки «Увімк.» на сторінці USB-диска.
- Старі версії лишаються доступними: нові випуски виходять поруч, а не замість них. Оберіть ту, яка вам потрібна.
- **Усі патчі накладаються на заводську V2.7.0.7**, а не один на інший. Не накладайте новішу версію поверх уже пропатченої старшої.

### Стан проєкту
Проєкт живий, але нові версії виходитимуть повільніше. Швидкі зміни вже зроблено, а те, що лишилося, потребує значно більше часу.
- Частина задумів потребує обладнання для тестів. Його треба знайти, купити за власні кошти і дочекатися доставки.
- Частина залежить від інформації, на яку я ще чекаю.
- Багато що потребує довгих тестів: одна лише крива розряду — це години безперервних вимірів, а потім складання таблиць.
- Не кожна ідея спрацьовує. Буває, що тести лише показують, що так робити не можна, і тижні роботи закінчуються без випуску.

Тож довга пауза між версіями не означає, що проєкт закинуто: я працюю над ним у міру часу, можливостей і складності кожної задачі.

Ідеї та побажання я збираю звідусіль: з Issues, форумів і чатів. Читаю все, але що і коли впроваджувати, вирішую сам, оцінивши користь і складність.

Грошових пожертв я не приймаю. Якщо хочете допомогти проєкту обладнанням для тестів, напишіть мені. Окрему функцію можна й прискорити: за оплату я відкладу інші задачі й зроблю її раніше. Це оплата за мій час, а не за ексклюзивність: функція все одно з'явиться в репозиторії для всіх на умовах GPL-3.0.

**Зв'язок:** питання, побажання й повідомлення про помилки — через розділ Issues. Щодо обладнання для тестів або оплачуваної функції — на пошту [axonixdev.contact@gmail.com](mailto:axonixdev.contact@gmail.com).

### Що зроблено (усі версії)
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
- У «Про прилад» видно версію моду, наприклад «Версія (UA-мод 1.6)».

### Що додано в 1.3 (є і в 1.4–1.6)
- **Генератор до 5 МГц** для всіх форм, крім синуса (синус, як і раніше, до 10 МГц). Заводська прошивка мовчки обрізає несинусоїдні форми до 2 МГц.
  - **Помаранчева частота зі знаком «!»** (наприклад «4.4!») означає: частота вища за 2 МГц, і форма сигналу вже **спотворюється**. Причина апаратна: ЦАП генератора (приблизно 50 млн точок/с) не встигає точно відтворити форму. Частота при цьому точна.
  - Реальні межі за моїми вимірами: прямокутник придатний приблизно до 5 МГц, трикутник 3–5 МГц, півхвиля ~3 МГц, сходинки й повна хвиля впізнавані до 5 МГц. Вище 5 МГц несинусоїдні форми перетворюються на синус або сміття, тому далі межу не піднято.
- **Звук у режимі діода**: писк, коли показ нижче 0,05 В (замкнені щупи), тим самим звуком, що й у прозвонці. Як і прозвонка, пищить навіть при нульовій гучності, бо це сигнал виміру, а не звук кнопок.
- **«OL»** без крапки при перевантаженні.

### Що додано в 1.4 (є і в 1.5, 1.6)
- **Кнопка Menu в генераторі й мультиметрі.** У заводській прошивці вона працює лише в осцилографі. Тепер з генератора чи мультиметра вона відкриває те саме загальне меню, що й в осцилографі. Раніше для цього треба було спершу вийти «Назад».
- **Позначка прихованого фільтра.** Коли виміряна частота нижча за 4,19 МГц (2²² Гц), прилад згладжує сигнал (див. «Відомі заводські вади»). Тепер у цьому разі частота виділяється **бурштиновою плашкою з чорними цифрами** у двох місцях: у рядку «Част.» нижнього списку вимірювань і у верхньому полі F.
  - Саме число частоти правильне. Плашка попереджає інше: **форма сигналу на екрані згладжена**, тому фронтам, дзвону й викидам довіряти не можна.
  - Вище порога плашка зникає сама. Коли значення немає («***») або воно нульове, плашки теж немає.
  - Позначено лише те, на що фільтр доведено впливає. Лічильники «Фронти»/«Спади» перевірено: під фільтром вони рахують правильно, тому їх не позначено.
  - Колір обрано не випадково: червоний залишено для майбутньої позначки «дані некоректні / межа приладу», а бурштиновий фон з чорними цифрами читається на екрані найкраще.
- Верхнє поле **F показує частоту каналу-джерела синхронізації** (меню «Синхронізація» → CH1/CH2), а не того каналу, що зараз вибраний. Так у заводській прошивці; фільтр при цьому вирішує для кожного каналу окремо, за його власною частотою.

### Що додано в 1.5 (є і в 1.6)
- **Відносний вимір (REL) у мультиметрі.** **Довге натискання Run** запам'ятовує поточне показання як нуль, і далі прилад показує різницю відносно нього. Повторне довге натискання вимикає режим. Працює для **постійної напруги, опору, діода й ємності**.
  - Головне застосування: відняти опір щупів (замкніть щупи → довге Run) або власну ємність щупів і проводів.
  - Опорне значення переживає автоперемикання діапазону. Зміна функції вимикає режим.
  - Відносним стає лише велике число. Графік і «Макс.»/«Мін.» показують звичайні, абсолютні значення.
  - **Індикатор — світлодіод біля Run:** червоний, коли режим увімкнено. На сторінці мультиметра цей світлодіод тепер показує саме REL. **HOLD працює як раніше**, його видно на екрані (плашка HOLD), але світлодіод від нього вже не червоніє.
- **Кнопка Single.** У заводській прошивці вихід з одиночного режиму завжди перемикає запуск на «Авто». Тепер повертається режим, який був до натискання Single («Нормальний» чи «Авто»).
- **«Макс.» над «Мін.»** у панелі мультиметра.
- **Батарея:** вимір заряду усереднюється, тож коротке просідання напруги під навантаженням більше не має спричиняти раптового вимкнення. Поріг вимкнення не змінено.
- **Переклад меню «Дисплей»:** «Вигляд сигналу», «Яскрав. сигналу», «Згасання» (було «Післясвічення»), «Стерти». Підписи переносяться між словами, а не посеред слова.

### Що додано в 1.6
- **Керування генератором ручками** (запит у GitHub №3). На сторінці генератора:
  - **велика ручка, натискання** — вибір рядка: частота → амплітуда → заповнення (лише ті рядки, що є в цієї форми). Вибраний рядок обведено синьою рамкою;
  - **мала верхня ручка, обертання** — зміна значення вибраного рядка;
  - **мала верхня ручка, натискання** — крок частоти по колу: 1 Гц … 1 МГц. Поточний крок видно під рядками («Крок: 1 kHz»).
  - Межі ті самі, що й з екранної клавіатури (5 МГц для несинусоїдних форм, 10 МГц для синуса). Амплітуда й заповнення змінюються так само, як заводськими стрілками на екрані.
- **Довге натискання Menu перемикає прилад** по колу: осцилограф → мультиметр → генератор → осцилограф. Коротке натискання працює як раніше. Зручно, коли працюєте в рукавицях і не можете користуватися сенсорним екраном (запит користувача з групи WhatsApp). Працює на трьох сторінках приладів, зокрема в осцилографі з відкритим меню; на інших сторінках (налаштування, перегляд знімків) довге натискання нічого не робить.
- **Відсотки заряду замість значка батареї** (на сторінках осцилографа, мультиметра й генератора).
  - **Біле число** — заряд у %, **червоне** нижче 20 %, **жовта блискавка** під час заряджання.
  - Відсоток рахується за **кривою розряду, виміряною на приладі** (24.11.2026), а не заводськими сходинками по 10 %. Заводські сходинки запізнюються: «100» тримається приблизно до 93 %, «90» — приблизно до 84 %.
  - Першу хвилину після ввімкнення або відключення зарядки число йде за реальним значенням (батарея «відпочиває» після зарядки). Далі **без зарядки воно не росте** і спадає не швидше 1 % за 15 с (1 % за 3 с, якщо реальне значення нижче на 5 % і більше). Коротке навантаження (дотики до екрана, увімкнення генератора) зсуває число щонайбільше на 1 %, а не на 7–10 %.
  - 0 % — це заводський поріг вимкнення (3,68 В, не змінено). На ньому прилад вимикається сам.
  - **Час роботи сильно залежить від навантаження.** Криву виміряно з одним увімкненим каналом і **генератором на 1 В**: приблизно **85 хвилин** від повного заряду до вимкнення. Генератор віддає енергію з батареї, тому він найбільший споживач; на **3 В** батарея сідає значно швидше. Лише з осцилографом чи мультиметром (без генератора) прилад працює помітно довше, а відсоток у середині діапазону може бути завищений на кілька відсотків.
- **Сторінка USB-диска: кнопку «Увімк.» обведено синьою рамкою.** У заводській прошивці це сірий напис, не схожий на кнопку.

### Що НЕ змінено
- **Вимірювання й калібрування** працюють за заводською логікою.
- Вади в ПЛІС (див. нижче) з боку мікроконтролера не виправити.

### Встановлення
**Що потрібно:** прилад, заряджений хоча б наполовину, USB-кабель, комп'ютер або телефон.

1. Завантажте з сайту FNIRSI **офіційну** прошивку V2.7.0.7 і розпакуйте архів. Потрібен файл `2D15P_V2.7.0.7_260826.bin`.
2. Відкрийте **Rom Patcher JS**: https://www.marcrobledo.com/RomPatcher.js/ (працює в браузері, і на телефоні теж, нічого встановлювати не треба).
3. У полі «ROM file» оберіть файл прошивки, у полі «Patch file» — патч потрібної версії (`...-1.2.bps` … `...-1.6.bps`), натисніть «Apply patch» і збережіть результат.
   *Альтернатива для комп'ютера: програма Floating IPS (Flips).*
4. Переконайтеся, що збережений файл називається **точно** `2D15P_V2.7.0.7_260826.bin`. Якщо браузер додав до назви щось своє, перейменуйте. Для перевірки: CRC32 результату — у таблиці вище.
5. На приладі (заводська англійська версія): кнопка **Menu** → **USB Sharing** → **ON**. Прилад з'явиться на комп'ютері як USB-диск.
6. Скопіюйте файл у папку **`Upgrade file`** на цьому диску.
7. Вимкніть і увімкніть прилад. Оновлення встановиться саме, файл після цього зникне з диска.
8. **Settings → Language → «Українська»**. Вибрана мова зберігається між оновленнями.

### Як повернути заводську прошивку
Встановлення **повністю оборотне**.
- **Звичайний спосіб:** прошийте офіційний файл V2.7.0.7 так само, як описано вище (кроки 5–7).
- **Якщо прилад не запускається:** вимкніть його, **затисніть великий регулятор і коротко натисніть кнопку живлення**. Запуститься завантажувач, який незалежно від основної прошивки відкриється на комп'ютері як USB-диск. Скопіюйте офіційний файл у папку `Upgrade file` і перезапустіть прилад.

### ⚠️ Старі прошивки й ревізії
FNIRSI підтвердили: 2D15P випускається в **різних апаратних версіях**, і прошивки для них **несумісні**. За словами FNIRSI, версію визначає **перша цифра прошивки, з якою прилад постачався**: «1…» — перше покоління, «2…» — друге. Ставте лише прошивки свого покоління. Цей мод — для V2.7.0.7, тобто для приладів другого покоління. Якщо щось пішло не так, скористайтеся аварійним способом (див. вище).

Якщо у вас прилад **першого покоління** і ви хочете мати можливості мода, напишіть про це в Issues. Сам я таких не зустрічав, але, кажуть, вони є, а під них мод не робився й не перевірявся.

### Відомі заводські вади
**У ПЛІС (модом не виправити):**
- **Прихований фільтр нижче 4,19 МГц** (2²² Гц = 4 194 304 Гц). Коли виміряна частота сигналу нижча за поріг, прилад згладжує фронти, дзвін і викиди — так, ніби завжди ввімкнено обмеження смуги 20M. Ручне 20M накладає його вдруге. Частота, шпаруватість і рівні при цьому правильні (амплітуда на ~3 % нижча). FNIRSI підтвердили, що фільтр навмисний і в налаштуваннях не вимикається. Рішення ухвалюється окремо для кожного каналу за його частотою. **На практиці:** для пошуку викидів на ключах чи дзвону на повільних сигналах цьому приладу не довіряйте.
- **Частотомір помиляється** на похилих фронтах і малій амплітуді: наприклад, сходинки 3 МГц він показує як 181 кГц, повну хвилю 2 МГц — як 57,6 Гц. На чистому прямокутнику він точний. Перевіряйте частоту курсорами. Імовірно, через це фільтр може вмикатися й на сигналах, справжня частота яких вища за поріг (не підтверджено).
- **Нормальний запуск не тримає осцилограму.** Від звичайного цифрового осцилографа очікують, що в режимі «Нормальний» остання осцилограма лишається на екрані до наступного запуску. Тут вона згасає за налаштуванням «Згасання» (до 1.5 — «Післясвічення»): з найкоротшим зникає майже одразу, з довшим — поступово тьмяніє, а з «∞» взагалі не стирається, а накопичується. Вимкнути «Згасання» не можна (мінімум — Min), тож жодне значення не дає утримання останнього кадру. Вимірювання в стані очікування показують «***». Інструкція (с. 43) каже інакше: «Normal: Refresh waveform only when a trigger event occurs». Виправити це з боку мікроконтролера не можна: осцилограму на екран накладає й гасить ПЛІС, тож, найімовірніше, саме вона не зберігає останній запуск у режимі «Нормальний».

**Осцилограф:**
- **Глибина пам'яті (10K / 100K / 1M) не дає видимої різниці.** Це помітили й інші власники на форумі EEVblog. Прошивка мікроконтролера передає вибрану глибину в ПЛІС; що ПЛІС з нею робить — невідомо. Напис частоти дискретизації («…Sa/s») від глибини не залежить взагалі, тож за ним судити про глибину не можна. Тест 22.10.2026 на офіційній V2.7.0.7 (імпульс близько 1 мкс, 9,7 кГц, 10 мс/под): живий екран і зупинений розтягнутий кадр однакові для 10K і 1M, на 100 мкс/под в обох випадках губиться більшість імпульсів. Дані осцилограми прилад не зберігає (лише знімки екрана), тож скористатися глибиною користувач ніде не може.

**Генератор:**
- Заявлено 0–10 МГц для всіх форм, але заводська прошивка мовчки обмежує всі форми, крім синуса, до 2 МГц (у 1.3 і новіших — до 5 МГц з позначкою).
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
- **Вимикайте генератор, коли він не потрібен** — він найшвидше садить батарею.

### Відмова від відповідальності
Мод перевірено на одному приладі. Використовуєте на власний ризик. Автор не пов'язаний з FNIRSI. Відгуки й повідомлення про помилки — через розділ Issues цього репозиторію.

---

## Changelog / Історія версій
- **1.6** — Generator controlled with the knobs (large knob press: row; top knob turn: value; top knob press: frequency step 1 Hz…1 MHz); long press of Menu cycles oscilloscope → multimeter → generator; battery percentage instead of the icon, measured on a real discharge curve, red below 20 %, yellow lightning while charging, never rises on battery and falls at a limited rate; ON button on the USB drive page framed. / керування генератором ручками (натискання великої — рядок; обертання верхньої — значення; натискання верхньої — крок частоти 1 Гц…1 МГц); довге натискання Menu по колу перемикає осцилограф → мультиметр → генератор; відсотки заряду замість значка за виміряною кривою розряду, червоні нижче 20 %, жовта блискавка під час заряджання, без зарядки не ростуть і спадають з обмеженою швидкістю; рамка навколо кнопки «Увімк.» на сторінці USB-диска.
- **1.5** — Relative measurement (REL) in the multimeter: long press Run, the LED next to Run is the indicator; Single restores the previous trigger mode; "Max" above "Min"; averaged battery reading against sudden shutdowns; Ukrainian Display menu labels. / відносний вимір (REL) у мультиметрі: довге натискання Run, індикатор — світлодіод біля Run; Single повертає попередній режим запуску; «Макс.» над «Мін.»; усереднення виміру батареї проти раптових вимкнень; переклад меню «Дисплей» («Згасання» замість «Післясвічення»).
- **1.4** — Menu key in the generator and multimeter; amber plate on the frequency while the hidden filter is active (below 4.19 MHz), in the measurement list and the F field; Normal trigger ("Afterglow") and memory depth added to known issues. / кнопка Menu в генераторі й мультиметрі; бурштинова плашка на частоті, коли діє прихований фільтр (нижче 4,19 МГц), у списку вимірювань і в полі F; до відомих вад додано нормальний запуск («Післясвічення») і глибину пам'яті.
- **1.3** — Generator up to 5 MHz for non-sine waveforms with a marker above 2 MHz (orange and "!"); beep in diode mode; "OL" instead of ".OL"; stock issues section updated. / генератор до 5 МГц для несинусоїдних форм з позначкою понад 2 МГц (помаранчевий колір і «!»); звук у режимі діода; «OL» замість «.OL»; оновлено опис заводських вад.
- **1.2** — Fixed the generator keypad in Square mode: the long Ukrainian «Duty» label pushed it past the left screen edge, so any tap closed it. The label is shortened. / виправлено екранну клавіатуру генератора в режимі «Прямокутник»: довгий підпис «Заповнення» зсував її за лівий край екрана, і вона закривалася від будь-якого натискання. Підпис скорочено до «Запов.».
- **1.1** — Restored icons embedded in the fonts (trash can on the delete button in picture view and two warning icons) that 1.0 removed by mistake together with the CJK glyphs. / повернуто значки, вбудовані в шрифти (кошик на кнопці видалення в перегляді знімка та два значки попереджень), які версія 1.0 помилково прибрала разом з ієрогліфами.
- **1.0** — First release. / перший випуск.

---

## License / Ліцензія
- My own changes in this repository (patches, tools, translations and corrections) are licensed under **GPL-3.0**, see `LICENSE`.
  Мої власні зміни в цьому репозиторії (патчі, інструменти, переклади й виправлення) поширюються за ліцензією **GPL-3.0**, див. `LICENSE`.
- **Additional terms:** everything in this repository is available on the same GPL-3.0 terms for everyone. Any exceptions or additional permissions (including different licensing terms) are possible only under a written agreement with the author, separately or together with other terms of such an agreement.
  **Додаткові умови:** усе в цьому репозиторії поширюється на однакових умовах GPL-3.0 для всіх. Будь-які винятки чи додаткові дозволи (зокрема інші умови ліцензування) можливі лише за письмовою угодою з автором, окремо або разом з іншими умовами такої угоди.
- Cyrillic glyphs rendered from **Fixel Text** © 2023 MacPaw Way Ltd., **SIL Open Font License 1.1** (`OFL-Fixel.txt`), converted to the device's bitmap format.
  Кириличні гліфи — з гарнітури **Fixel Text** © 2023 MacPaw Way Ltd., ліцензія **SIL Open Font License 1.1** (`OFL-Fixel.txt`), перетворено в растровий формат приладу.
- The original firmware is © FNIRSI and must be obtained from FNIRSI. The patch contains only the changes.
  Прошивка FNIRSI не входить до репозиторію, її треба завантажити з сайту FNIRSI. Патч містить лише зміни.

## See also / Дивіться також
- [2D15P thread on the EEVblog forum](https://www.eevblog.com/forum/testgear/new-handheld-dsodmm-fnirsi-2d15p-100mhz500msps-(september-2025)/) — discussion of the device, test details and photos. / [Тема 2D15P на форумі EEVblog](https://www.eevblog.com/forum/testgear/new-handheld-dsodmm-fnirsi-2d15p-100mhz500msps-(september-2025)/) — обговорення приладу, подробиці тестів і фото.
- Another 2D15P mod: boots into the multimeter, Turkish / German / Dutch UI. The ideas of the Menu key outside the scope (1.4) and of relative measurement (REL), with part of the key and multimeter field map (1.5), also come from there; both implemented with my own code. / [giray/fnirsi-2d15p-mod](https://github.com/giray/fnirsi-2d15p-mod) — інший мод 2D15P: запуск одразу в мультиметр, турецька / німецька / нідерландська мови. Звідти ж ідея кнопки Menu поза осцилографом (у 1.4) і відносного виміру REL разом з частиною карти кнопок і полів мультиметра (у 1.5); обидва реалізовано власним кодом.
  ⚠️ **This mod (UA mod) and giray's mod are not compatible**, because they are built on completely different principles and implementation methods. Do not try to combine them or flash one on top of the other: the device will stop working and will have to be recovered with the emergency method. Use one mod or the other, always starting from the official V2.7.0.7. / ⚠️ **Цей мод (UA-мод) і мод giray несумісні**, бо вони побудовані на зовсім різних принципах і методах реалізації. Не намагайтеся поєднати їх чи накласти один поверх іншого: прилад перестане працювати, і його доведеться відновлювати аварійним способом. Використовуйте або один мод, або інший, завжди починаючи з офіційної V2.7.0.7.
