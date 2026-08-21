# Changelog

---

## [v77]

> **Before you update:** two changes in this release can alter how existing presets
> sound. See [Preset compatibility](#preset-compatibility) below.

### Added

#### Step Modulator

A new modulator that works either as an **arpeggiator** or as a **step sequencer**
triggered by one of the internal trigger sources. It occupies two pages in **page group 7**.

**`sSEQ` — sequence editing**

| Parameter | Range | Description |
|---|---|---|
| `VALU` | −36 : 36 | Value of the sequence step under the cursor |
| `CURS` | — | Moves the sequence cursor. Press and hold the encoder to set sequence length, 1–16 steps |
| `ROTA` | — | Rotates the sequence |
| `RAND` | 0 : 32 | Amount of randomness used by the generation algorithm. `0` fills the whole sequence with zeros; `32` continuously generates new random values for every step |

To generate a new sequence manually: hold `TSEL` to select the track, then press the
`RAND` encoder.

**`sMX` — modulation matrix**

| Parameter | Description |
|---|---|
| `PARM` | Parameter to be modulated |
| `DEST` | Track containing the selected `PARM` |
| `TSRC` | Trigger source that advances the sequencer to the next step |
| `ALIAS` | Base value of the modulated parameter |

`TSRC` values:

| Value | Advances the sequencer on |
|---|---|
| `OFF` | Triggering disabled |
| `vENV` | Amplitude envelope in loop mode |
| `mENV` | Modulation envelope in loop mode |
| `vmEN` | Both envelopes in loop mode |
| `TSEL` | Each press of the track touch sensor |

#### Modulation and synthesis (PAGE 1, 2, 3)

- **`GLIDE` added as a modulation destination.**
- **`RELEASE` added as a modulation destination.**
- **`Sample & Hold` type added to the `QUANT*` parameter.**
- **`Envelope Follower` type added to the `QUANT*` parameter.**
- **Just Intonation tuning added to the `SCALE` parameter.**
- **Sharp Attack mode added to the `SHAP` parameter** on the `*ENV` pages.

#### Interface 

- **`1HOT TSEL` mode added** in `tSEL`. Lets you edit the last selected track without holding the
  Track Select button. All tracks must be set to `1HOT` mode for this to work correctly.
- **Active modulation destination parameter names are now highlighted** while the `ALIAS`
  encoder is rotated on `*MX` pages.

### Changed

- **`FOLD` renamed to `MULT`.** Both hard sync and wavefolding effectively behave as
  forms of frequency multiplication, and the name now reflects that.
- **`MIDL` now compensates for aliasing automatically.** As oscillator `FREQ` rises,
  `MIDL` gradually moves toward `0.5`, reducing harmonic richness and minimizing aliasing.
- **`DRIV` now displays gain values.** The parameter's lookup table has been rebuilt.
- **Improved filter resonance response.** Resonance now behaves more like a classic Moog
  ladder filter — smoother in character, with the characteristic drop in output level at
  higher resonance settings.
- **MIDI CC17 (Filter Cutoff) now controls the currently selected filter type.** Use the
  KALEIDOSCOPE interface to select which filter type is active.
- **New generative sequencer behavior.** When an EOC trigger from Voice A is sent to
  Voice *B*, and *B* is not currently holding its envelope while its Modulator MIDI
  Channel is also set to *B*, **both** the *B* amplitude envelope and the *B*
  modulation envelope are triggered.
- Minor interface improvements.

### Fixed

- Fixed the default preset.
- Minor bug fixes.

### Preset compatibility

| Change | Effect on existing presets |
|---|---|
| `DRIV` lookup table rebuilt | Presets may sound slightly different. Adjust `DRIV` manually where needed. |
| `MIDL` aliasing compensation | Bright, high-`FREQ` patches will read as less harmonically rich than before — this is the anti-aliasing behavior working as intended. |

# Firmware Update

How to install a new firmware version on KALEIDOSCOPE.

> 🇷🇺 **Русская версия** — в конце страницы, [Обновление прошивки](#обновление-прошивки).

---

## Before you start

You will need a computer and a **USB Type-C** cable. Nothing else — the device carries
its own bootloader and mounts as a plain flash drive.

> ⚠️ **Back up your presets first.** A firmware update does not intentionally clear
> memory slots, but an interrupted update can leave the device in an unknown state.
> Export anything you care about — see [PRESETS.md](PRESETS%20&%20ENSEMBLES.md).

> ℹ️ Some releases change how existing presets sound. Read
> [CHANGELOG.md](CHANGELOG.md) before updating.

---

## Update procedure

1. Connect the device to your computer with a **USB Type-C** cable.
2. Rename the firmware file you want to install to **`blink.bin`**.
3. Press and hold **Encoder 1**. While holding it, briefly tap the **RESET** button to
   restart the device.
4. The display shows a message confirming **USB mode** — you can release Encoder 1 now.
   The device appears on your computer as a USB flash drive.
5. Copy **`blink.bin`** to the **root** of that drive.
6. When the copy finishes, **safely eject** the drive through your operating system.
7. Restart KALEIDOSCOPE with a brief press of **RESET**.
8. On startup the display confirms that the firmware was installed successfully.

The device copies the firmware into its internal memory, deletes `blink.bin`, and boots
into the application. The file disappearing from the drive is normal — it means the
update went through.

---

## Quick reference

| | |
|---|---|
| **Firmware filename** | `blink.bin` — exactly this name, in the drive root |
| **Enter USB mode** | Hold Encoder 1 + tap RESET |
| **Exit USB mode** | Safely eject, then tap RESET |
| **Simplified font** | Hold Encoder 2 while the device starts up |

---

## Troubleshooting

| Symptom | Likely cause |
|---|---|
| Device does not appear as a flash drive | Encoder 1 was released too early, or the cable is charge-only — use a cable that carries data |
| Nothing happens after RESET | The file is not named exactly `blink.bin`, or it is in a subfolder instead of the drive root |
| `blink.bin` is still on the drive after restart | The update did not run. Check the filename, re-copy, and eject safely before pressing RESET |
| Update seems to hang | Do not disconnect power. Wait for the on-screen message, then RESET |
| Display looks garbled after the update | Boot once with Encoder 2 held to use the simplified font |

> ⚠️ **Never unplug the device mid-update.** Wait for the confirmation message on screen.

---
---

# Обновление прошивки

Как установить новую версию прошивки на KALEIDOSCOPE.

## Перед началом

Понадобится компьютер и кабель **USB Type-C**. Больше ничего — загрузчик уже внутри
устройства, оно монтируется как обычная флешка.

> ⚠️ **Сначала сделайте бэкап пресетов.** Обновление прошивки не стирает слоты памяти
> намеренно, но прерванная прошивка может оставить устройство в непредсказуемом
> состоянии. Экспортируйте всё, что дорого — см. [PRESETS.md](PRESETS%20&%20ENSEMBLES.md).

> ℹ️ Некоторые релизы меняют звучание существующих пресетов. Перед обновлением загляните
> в [CHANGELOG.md](CHANGELOG.md).

---

## Порядок обновления

1. Подключите устройство к компьютеру кабелем **USB Type-C**.
2. Переименуйте файл прошивки, который хотите установить, в **`blink.bin`**.
3. Нажмите и удерживайте **Encoder 1**. Удерживая его, кратковременно нажмите кнопку
   **RESET**, чтобы перезапустить устройство.
4. На экране появится сообщение о переходе в **режим USB** — теперь Encoder 1 можно
   отпустить. Устройство определится на компьютере как USB-флэш-накопитель.
5. Скопируйте **`blink.bin`** в **корневую папку** накопителя.
6. После завершения копирования **безопасно извлеките** накопитель средствами
   операционной системы.
7. Перезапустите KALEIDOSCOPE кратковременным нажатием **RESET**.
8. После запуска на экране появится сообщение об успешной загрузке новой прошивки.

Устройство копирует прошивку во внутреннюю память, удаляет `blink.bin` и переходит к
работе приложения. То, что файл пропал с накопителя, — нормально: значит, обновление
прошло.

---

## Шпаргалка

| | |
|---|---|
| **Имя файла прошивки** | `blink.bin` — ровно так, в корне накопителя |
| **Вход в режим USB** | Удерживать Encoder 1 + нажать RESET |
| **Выход из режима USB** | Безопасно извлечь, затем нажать RESET |
| **Упрощённый шрифт** | Удерживать Encoder 2 во время запуска устройства |

---

## Что делать, если не сработало

| Симптом | Вероятная причина |
|---|---|
| Устройство не появляется как накопитель | Encoder 1 отпущен слишком рано, либо кабель только для зарядки — нужен кабель с передачей данных |
| После RESET ничего не происходит | Файл назван не ровно `blink.bin`, либо лежит в подпапке, а не в корне |
| `blink.bin` остался на накопителе после перезапуска | Обновление не запустилось. Проверьте имя, скопируйте заново и извлеките накопитель безопасно перед RESET |
| Кажется, что обновление зависло | Не отключайте питание. Дождитесь сообщения на экране, затем нажмите RESET |
| После обновления экран выглядит странно | Запустите устройство один раз с зажатым Encoder 2 — включится упрощённый шрифт |

> ⚠️ **Никогда не отключайте устройство во время обновления.** Дождитесь подтверждения
> на экране.
