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

