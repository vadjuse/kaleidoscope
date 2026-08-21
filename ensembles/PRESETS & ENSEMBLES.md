# README

How to save, export, and import sounds on KALEIDOSCOPE.

> 🇷🇺 **Русская версия** — в конце страницы, [Пресеты и ансамбли](#пресеты-и-ансамбли).

---

## How preset memory works

KALEIDOSCOPE has two kinds of storage:

| **Native slots** | 4 per Voice — the settings a track is actually playing from |
| ---------------- | ----------------------------------------------------------- |
| **Memory slots** | 128 shared slots, numbered `000`–`127`                      |

Settings move **between a native slot and a memory slot** in either direction. They can
**not** be copied directly from one memory slot to another.

A single preset file holds the settings of **one Voice**. A four-Voice patch — what we
call an **ensemble** — is therefore four files, one per Voice.

---

## Saving and loading on the device

Everything happens on the **CFG → PRST** page.

**To load a memory slot into a Voice:**

1. Hold the Voice selector sensor `Tx`.
2. Turn encoder `V1` to choose the slot.
3. Hold `Tx` again and hold encoder `V3` until the on-screen progress bar fills.

**To save a Voice into a memory slot:**

1. Hold the track selector sensor `Tx`.
2. Turn encoder `V1` to choose the slot.
3. Hold `Tx` again and hold encoder `V4` until the on-screen progress bar fills.

> ⚠️ **Both actions overwrite permanently.** Loading erases the track's current preset;
> saving erases whatever was in the target slot. Back up to another slot or to your
> computer first.

---

## Entering USB mode

Export and import both run from USB mode. The device mounts as a plain flash drive.

1. Connect KALEIDOSCOPE to a computer over USB.
2. Hold **encoder 1**.
3. Press the **reset** button.
4. Release encoder 1.

The computer mounts the device as a flash drive and the screen shows on-device
instructions. All files below go to the **root** of that drive.

---

## Exporting presets to your computer

1. Enter USB mode.
2. Copy an empty file named **`exp.bin`** to the root of the drive. This is the flag that
   tells the device an export was requested.
3. Copy one file per slot named **`expXXX.bin`**, where `XXX` is the slot number.
4. Safely eject the device, then press **reset**.
5. The device writes each slot's settings into its matching `expXXX.bin`, deletes
   `exp.bin`, and returns to USB mode.
6. Copy the files to your computer.

**`XXX` must always be three digits:**

| Slot | Filename |
|---|---|
| 3 | `exp003.bin` |
| 29 | `exp029.bin` |
| 127 | `exp127.bin` |

---

## Importing presets into the device

1. Rename each preset you want to import to **`impXXX.bin`**, where `XXX` is the
   **destination slot** in device memory — `imp000.bin`, `imp012.bin`, `imp123.bin`.
2. Enter USB mode.
3. Copy an empty file named **`imp.bin`** to the root of the drive. This is the flag that
   tells the device an import was requested.
4. Copy the `impXXX.bin` files to the root as well.
5. Safely eject the device, then press **reset**.
6. The device writes each file into its matching slot, deletes `imp.bin`, and boots into
   the application.

> ⚠️ **Import overwrites the destination slot permanently.** Whatever was in slot `XXX`
> is gone. Pick empty slots, or export the existing contents first.

**Note the number swap:** the number in an exported filename is the slot it *came from*.
The number in an imported filename is the slot it will *go to*. Renaming
`exp063.bin` → `imp010.bin` puts that sound into slot 10.

---

## Loading an ensemble

A shared four-track patch only works if each preset lands on the **Voice it was written
for**. Generative sequencer patching (EOC triggers, `LNK`) and sidechains address Voice
by number, so track assignment is what recreates the piece — the slot numbers you use
along the way do not matter.

**Example ensemble:**

| Voice  | File         | Suggested import name |
| ------ | ------------ | --------------------- |
| **T1** | `exp063.bin` | `imp063.bin`          |
| **T2** | `exp064.bin` | `imp064.bin`          |
| **T3** | `exp118.bin` | `imp118.bin`          |
| **T4** | `exp117.bin` | `imp117.bin`          |

**Steps:**

1. Rename the four files to `impXXX.bin`, choosing four free memory slots. Keeping the
   original numbers is the simplest option if those slots are free.
2. Import all four at once — one `imp.bin` flag file covers the whole batch.
3. On the **CFG → PRST** page, load each slot into its track: slot for T1 → `T1`, slot
   for T2 → `T2`, and so on.

Once all four tracks are loaded, the generative sequencer patch and the sidechains are
recreated and the instrument plays the ensemble as recorded.

---

## Troubleshooting

| Symptom | Likely cause |
|---|---|
| Nothing happens after reset | The `imp.bin` / `exp.bin` flag file is missing, or the files are not in the **root** of the drive |
| Some presets imported, others did not | A filename is not exactly three digits — `imp12.bin` and `imp0012.bin` are both ignored |
| Export files are unchanged | `expXXX.bin` files must already exist on the drive before reset; the device fills them, it does not create them |
| The ensemble sounds wrong | Presets landed on the wrong tracks. Cross-modulation and sidechains are addressed by track number |
| Device did not remount | Always eject safely before pressing reset |

---
---

# Пресеты и ансамбли

Как сохранять, экспортировать и импортировать звуки на KALEIDOSCOPE.

## Как устроена память пресетов

У KALEIDOSCOPE два типа хранилища:

| | |
|---|---|
| **Родные слоты** | 4 на каждый трек — настройки, с которыми трек играет прямо сейчас |
| **Слоты памяти** | 128 общих слотов, номера `000`–`127` |

Настройки перемещаются **между родным слотом и слотом памяти** в обе стороны. Напрямую
из одного слота памяти в другой скопировать **нельзя**.

Один файл пресета хранит настройки **одного трека**. Патч на четыре трека — то, что мы
называем **ансамблем** — это, соответственно, четыре файла, по одному на трек.

---

## Сохранение и загрузка на устройстве

Всё происходит на странице **CFG → PRST**.

**Загрузить слот памяти в трек:**

1. Удерживайте сенсор трека `Tx`.
2. Крутите энкодер `V1`, выбирая слот.
3. Снова удерживайте `Tx` и держите энкодер `V3`, пока полоса прогресса на экране не заполнится.

**Сохранить трек в слот памяти:**

1. Удерживайте сенсор трека `Tx`.
2. Крутите энкодер `V1`, выбирая слот.
3. Снова удерживайте `Tx` и держите энкодер `V4`, пока полоса прогресса не заполнится.

> ⚠️ **Обе операции перезаписывают данные безвозвратно.** Загрузка стирает текущий пресет
> трека, сохранение — содержимое выбранного слота. Сначала сделайте копию в другой слот
> или на компьютер.

---

## Вход в USB-режим

Экспорт и импорт работают из USB-режима. Устройство монтируется как обычная флешка.

1. Подключите KALEIDOSCOPE к компьютеру по USB.
2. Зажмите **энкодер 1**.
3. Нажмите кнопку **reset**.
4. Отпустите энкодер 1.

Компьютер увидит устройство как флеш-накопитель, на экране появится инструкция. Все
файлы ниже кладутся **в корень** этого накопителя.

---

## Экспорт пресетов на компьютер

1. Войдите в USB-режим.
2. Скопируйте в корень пустой файл **`exp.bin`** — это флаг, который сообщает устройству
   о запросе экспорта.
3. Скопируйте по одному файлу на слот с именем **`expXXX.bin`**, где `XXX` — номер слота.
4. Безопасно извлеките устройство и нажмите **reset**.
5. Устройство запишет настройки каждого слота в соответствующий `expXXX.bin`, удалит
   `exp.bin` и вернётся в USB-режим.
6. Скопируйте файлы на компьютер.

**`XXX` — всегда три цифры:**

| Слот | Имя файла |
|---|---|
| 3 | `exp003.bin` |
| 29 | `exp029.bin` |
| 127 | `exp127.bin` |

---

## Импорт пресетов в устройство

1. Переименуйте каждый пресет в **`impXXX.bin`**, где `XXX` — **слот назначения** в памяти
   устройства: `imp000.bin`, `imp012.bin`, `imp123.bin`.
2. Войдите в USB-режим.
3. Скопируйте в корень пустой файл **`imp.bin`** — флаг запроса импорта.
4. Туда же скопируйте файлы `impXXX.bin`.
5. Безопасно извлеките устройство и нажмите **reset**.
6. Устройство запишет каждый файл в соответствующий слот, удалит `imp.bin` и перейдёт
   к работе приложения.

> ⚠️ **Импорт перезаписывает слот назначения безвозвратно.** Всё, что было в слоте `XXX`,
> будет стёрто. Выбирайте пустые слоты — или сначала экспортируйте их содержимое.

**Обратите внимание на смену номера:** номер в имени экспортированного файла — это слот,
*откуда* пресет взят. Номер в имени импортируемого файла — это слот, *куда* он ляжет.
Переименовав `exp063.bin` → `imp010.bin`, вы положите звук в слот 10.

---

## Загрузка ансамбля

Общий патч на четыре трека звучит правильно только тогда, когда каждый пресет попадает
**на тот трек, для которого он написан**. Патчинг генеративного секвенсора (EOC-триггеры,
`LNK`) и сайдчейны адресуют треки по номеру, поэтому пьесу воссоздаёт именно распределение
по трекам — номера слотов по пути значения не имеют.

**Пример ансамбля:**

| Трек | Файл | Имя для импорта |
|---|---|---|
| **T1** | `exp063.bin` | `imp063.bin` |
| **T2** | `exp064.bin` | `imp064.bin` |
| **T3** | `exp118.bin` | `imp118.bin` |
| **T4** | `exp117.bin` | `imp117.bin` |

**Порядок действий:**

1. Переименуйте четыре файла в `impXXX.bin`, выбрав четыре свободных слота памяти. Проще
   всего оставить исходные номера, если эти слоты свободны.
2. Импортируйте все четыре разом — одного флага `imp.bin` хватает на всю партию.
3. На странице **CFG → PRST** загрузите каждый слот в свой трек: слот для T1 → `T1`,
   слот для T2 → `T2` и так далее.

Когда все четыре трека загружены, патч генеративного секвенсора и сайдчейны
восстанавливаются, и инструмент играет ансамбль так, как он был записан.

---

## Что делать, если не сработало

| Симптом | Вероятная причина |
|---|---|
| После reset ничего не происходит | Нет файла-флага `imp.bin` / `exp.bin`, либо файлы лежат не **в корне** накопителя |
| Часть пресетов импортировалась, часть нет | В имени не ровно три цифры — `imp12.bin` и `imp0012.bin` игнорируются |
| Файлы экспорта не изменились | Файлы `expXXX.bin` должны уже лежать на накопителе до reset: устройство их заполняет, а не создаёт |
| Ансамбль звучит не так | Пресеты попали не на те треки. Кросс-модуляция и сайдчейны адресуются по номеру трека |
| Устройство не примонтировалось заново | Всегда извлекайте накопитель безопасно перед нажатием reset |
