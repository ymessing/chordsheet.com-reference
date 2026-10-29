# ChordSheet.com — Complete Syntax & Practical Reference

A comprehensive reference for converting lead sheets and handwritten chord charts into [chordsheet.com](https://www.chordsheet.com/) text format. Combines the official **Cheat Sheet (v04)**, rules from the [Online Manual](https://www.chordsheet.com/manual/) and [A–Z Glossary](https://www.chordsheet.com/glossary), and practical patterns learned from transcribing real charts.

---

## 1. Core Principles & Layout

- **Whitespace separates bars**: Each space-separated token (or `_`-glued group) is **one bar**.
- **No barline delimiters needed**: Do **not** type `|` between normal bars; regular barlines are drawn automatically.
- **4 bars per line**: Standard layout is 4 bars per line.
- **No lyrics in the chord grid**: Lyrics are not supported inline with chords (use `"annotation"` only for short musical cues, never lyrics).
- **Comments**: Start a line with `#` for comments (ignored by the renderer; useful for song title/artist metadata at the top of a `.txt` file).

---

## 2. Section Titles, Labels & Dividers

| Syntax | Meaning | Visual Result |
| :--- | :--- | :--- |
| `- Verse` | Plain text line | Unboxed text annotation above the next row |
| `-` | Blank text line | Adds extra vertical spacing between rows (prevents symbol collisions) |
| `; Ve   rs  e` | Literal text line | Preserves multiple spaces |
| `: Verse` | Boxed section title | Text inside a border box |
| `= Verse` | **Section delimiter** + box | Text inside a border box **and** automatically closes the previous bar with `\|\|` and opens the next bar with `\|\|` |
| `<: A` or `<= A` | **Left floating label** | Places a boxed `A` in the far-left margin of the row (saves vertical space) |
| `<- 5` | **Left floating bar number** | Places italicized bar number `5` in the far-left margin |
| `>- guitar joins` | **Right floating note** | Places text in the right margin (add `X` at the end of the row or reduce bars per row to leave room) |
| `+` or `+ Chorus` | Page break | Starts a new page (optionally starting a `= Chorus` section) |
| `RULER` / `DOTTED4` / `DASHED3` | Horizontal divider | Draws a solid, dotted, or dashed horizontal line (`1`–`9` sets thickness) |
| `TAB` or `TAB1`..`TAB7` | TAB staff row | Adds a row of TAB lines (`TAB` defaults to 6 lines; `TAB1` acts as a separator) |

### Three Columns of Text
Use **two spaces** to push text to the next column (left, center, right):
- `-left text` -> left column
- `-  center text` -> center column (2 spaces after `-`)
- `-    right text` -> right column (4 spaces after `-`)
- `-left  center  right` -> all three columns

---

## 3. Chord Nomenclature & Handwritten Chart Translations

When reading handwritten or jazz lead sheets, convert symbols as follows:

| Chart Symbol | Meaning | ChordSheet.com Syntax | Notes / Edge Cases |
| :--- | :--- | :--- | :--- |
| `C`, `F#`, `Bb` | Major | `C`, `F#`, `Bb` | Uppercase root |
| `Cm`, `Dm` | Minor | `Cm`, `Cmi`, `Cmin`, `C-`, `c` | All render identically based on user settings |
| `CMaj7`, `Δ7` | Major 7th | `Cmaj7`, `Cj7`, `CM7` | Also `Cmaj9`, `Cj9`, `Cj13`, `CM13`, `C6`, `C69` |
| `C7` | Dominant 7th | `C7` | |
| `Eb79`, `Eb9` | Dominant 9th | `Eb9` | Handwritten charts often write `79`; write `Eb9` (or `C11`, `C13`) |
| `Dm7` | Minor 7th | `Dm7` | Also `Dm6`, `Dm9`, `Dm11`, `DmM7`, `DmMaj9`, `Cm6add9` |
| `Eø`, `Eø7`, `Em7b5` | **Half-diminished** | `Em7b5` | Always write `m7b5` (renders as `ø7` or `m7b5` per settings) |
| `C#o`, `C#o7` | **Diminished / Dim 7** | `C#dim`, `C#dim7` | Always write `dim` or `dim7` (renders as `°` / `°7` per settings) |
| `B+`, `Baug` | Augmented | `B+`, `Baug`, `Ab7+`, `Bbaug7` | |
| `Dsus`, `Dsus4`, `Dsus2` | Suspended | `Dsus`, `Dsus4`, `Dsus2`, `D4`, `D2` | Also `A7sus4`, `A9sus4`, `A13sus4` |
| `A7b9`, `A7b13` | **Altered Dominant (single)** | `A7b9`, `A7#9`, `A7b5`, `A7#5`, `A7#11`, `A7b13` | No parentheses needed when `7`, `9`, `11`, or `13` is present (`A13b9`) |
| `Eb7(b9b13)` | **Altered Dominant (multiple)** | `Eb7(b9b13)`, `F7(#9b13)`, `Ebalt`, `A7alt` | Use parentheses for multiple alterations, or `alt` |
| `B(b5)` vs `Ab7b5` | Major flat 5 | `B(b5)`, `Ab7b5`, `Bbj7b5` | **Parentheses required** if no `7`/`j7` so `B(b5)` isn't read as `Bb5` |
| `G(#11)` vs `G7#11` | Lydian (`#11`) | `G(#11)`, `Gadd#11`, `G7#11` | **Parentheses required** if no `7`/`add` so `G(#11)` isn't read as `G#11` |
| `Amb6` vs `a(b6)` | Minor flat 6 | `Amb6`, `B-b6`, `a(b6)` | Parentheses required only if using lowercase minor notation (`a(b6)`) |
| `Cadd9`, `A5` | Added tone / Power | `Cadd2`, `Cadd4`, `Cadd9`, `Cadd11`, `Cadd13`, `A5` | |
| `N.C.` | No Chord | `NC` or `N.C.` | Prints `N.C.` |
| `*` | **Blank / Invisible Chord** | `*` | Prints nothing; used for empty bars, beat spacing, ties, and moving basslines |

---

## 4. Slash Chords & Moving Basslines

- **Standard slash chord**: `D/F#`, `Gm/Bb`, `Bb/C` (uppercase bass note).
- **Moving bassline under the same chord (`Dm   /C`)**:
  When a chart writes a chord on beat 1 and only the new bass note `/C` on beat 3, use the blank chord `*` before the slash:
  ```text
  Dm_*/C
  ```
  This renders as `| Dm   /C |` without repeating `Dm`. (Or write `Dm_Dm/C` if the chart explicitly repeats the root chord name).

---

## 5. Split Bars & Beat Placement (`_` and `*`)

Use the underscore `_` ("glue") to put multiple chords in a single bar. Combine with `*` (blank chord) to place chords on specific beats in a 4/4 bar:

| Beat Positions in 4/4 | Syntax | Visual Result in Bar |
| :--- | :--- | :--- |
| Beats 1 & 3 (half-bar split) | `Dm_G7` | `\| Dm    G7 \|` |
| Three chords in one bar | `A_C_D` | `\| A  C  D \|` |
| Four chords (one per beat) | `A_B_C_D` | `\| A B C D \|` |
| Chord on **Beat 2** only | `*_B_*_*` | `\|   B     \|` |
| Chord on **Beat 3** only | `*_*_C_*` | `\|     C   \|` |
| Chord on **Beat 4** only | `*_*_*_D` | `\|       D \|` |
| Chords on **Beats 1 & 4** | `A_*_*_D` | `\| A     D \|` |
| Chords on **Beats 1 & 2** | `A_B_*_*` | `\| A B     \|` |
| Chords on **Beats 3 & 4** | `*_*_C_D` | `\|     C D \|` |

---

## 6. Rhythmic Notation, Pushes & Ties

While `chordsheet.com` does not draw full 5-line musical staves, it provides dedicated symbols for syncopations, anticipations (pushes), ties across barlines, holds, and rhythmic slashes:

| Feature | Syntax | Symbol Rendered | Placement Rules |
| :--- | :--- | :--- | :--- |
| **Eighth-note push** | `<C` or `Am_<D7` | `♪‿` above chord | Prefix `<` **immediately before** the chord (`<Dm/F`) |
| **Sixteenth-note push** | `<<C` or `Am_<<D7` | `♬‿` above chord | Prefix `<<` **immediately before** the chord |
| **Tie across barline** | `C ^ C` or `Dm ^ *` | `⁀` over barline | Place `^` **after** the tied chord at the end of a bar |
| **Whole-note / Diamond** | `G <>` or `G diamond` | `◇` above chord | Place `<>` or `diamond` **after** the chord |
| **Fermata** | `G fermata` | `𝄐` above chord | Place `fermata` **after** the chord |
| **Stroke / Slash marks** | `A,,,` or `A,B,` or `A,,B` | `/` beat slashes | Add one `,` per slash after the chord (or `A_B,,`) |
| **Rests** | `r1`, `r2`, `r4`, `r8`, `r16` | Standard rest symbols | Can be dotted (`r2.`, `r4.`, `r8.`) and glued (`r2_r4._r8`) |
| **Time Signature** | `4:4 A` or `2:4 B` or `6:8 C` | Time signature at bar start | Place `N:M` before the first chord of the bar |
| **Chord Annotation** | `G "stop"` | Small text above chord | Put text in double quotes after the chord |

### Practical Pattern: Syncopated Intro with Pushes & Ties Across Barlines
When a chart has a rhythmic figure under the chords—for example, in *Hayiti Omeret*, where:
- **Bar 1**: `Gm` on beat 1 (dotted quarter), `Dm/F` pushed on beat 2& (held through beat 3), `Em7b5` pushed on beat 4& and **tied across the barline** into Bar 2
- **Bar 2**: `(Em7b5)` held on beat 1, `A7` pushed on beat 2& (held through beat 3), `Dm` pushed on beat 4& and **tied across the barline** into Bar 3
- **Bar 3**: `(Dm)` held for the entire bar
- **Bar 4**: `A7b13` held as a whole note

Write it using 4 beat slots per split bar so the pushed beat-4& chord sits right against the barline where `^` draws the tie arch, and use `*` for held beats/bars so chord names aren't redundantly reprinted:
```text
= Intro
4:4 Gm_<Dm/F_*_<Em7b5 ^ *_<A7_*_<Dm ^ * A7b13 <>
```

---

## 7. Repeats, Endings, Indentation & Simile Marks

- **Repeat section (`|: ... :|`)**: Wrap bars in parentheses: `(A B C D)`
- **Repeat N times**: `(A B C D)x3` or `(A B C D)3x`
- **1st and 2nd Endings (Volta Brackets)**:
  ```text
  (Dm G7 1. Cm7 F7
  X X 2. Cmaj7 % )
  ```
  - Use `1.`, `2.` (or complex endings like `1.-3.+5.`) before the first bar of each ending.
  - Use `X` (one `X` per indented bar) on the second line so the 2nd ending aligns vertically under the 1st ending.
- **Explicit Double Barline (`||`)**:
  - Start of row: `|| A B C D`
  - End of row: `A B C D ||`
  - Mid-row: `A B || C D`
  *(Note: `= Section` adds closing/opening `||` automatically, so explicit `||` is only needed when not starting a new `=` section).*
- **Simile Marks (print `%` or `%%` symbol)**:
  - `%` — single-bar simile mark
  - `%%` — two-bar simile mark
- **Reprint Shortcuts (copies actual chord names from previous bars)**:
  - `%1` — reprints the previous 1 bar's chords
  - `%2` — reprints the previous 2 bars' chords (also `%4`, etc.)
- **Optional / Grouped Chords**:
  - `A?` or `B_C?` — puts parentheses `(A)` or `(B C)` around optional/turnaround chords.
  - `[Dm7_G7]` — encloses multiple chords in square brackets `[Dm7 G7]` (often used for turnaround bars at the end of a section before a Coda jump).

---

## 8. Navigational Markers (Coda, Segno, D.C., D.S., Fine)

| Token | Meaning | Placement Rule |
| :--- | :--- | :--- |
| `o` (lowercase) | **Coda-from** (`⊕` jump marker) | Placed **after** the bar where you jump to the Coda; renders `⊕` at the **end of that bar** (e.g., `Em7b5_A7b13 o`) |
| `O` (uppercase) | **Coda-to** (`⊕` target section) | Placed at the **start of the Coda line**; always renders `⊕` at the far left of the line (e.g., `O (Dm_Dm/C ...)`) |
| `$` or `§` | **Segno** (`𝄋`) | Placed before the target bar/repeat (e.g., `§ (G Bm C D)`) |
| `fine` | **Fine** | Placed after the ending bar (e.g., `C fine`) |
| `D.C.` / `D.S.` | Da Capo / Dal Segno | Placed at the end of the bar: `D.C.`, `D.C. al fine`, `D.C. al coda`, `D.C. al coda con rep.`, `D.C. al coda senza rep.`, `D.S.`, `D.S. al fine`, `D.S. al coda con rep.` |

### Coda Example
```text
# Jump marker at the end of Bar 2 in the last line of A:
Gm_Dm/F Em7b5_A7b13 o Dm A7b13

= Coda
O (Dm_Dm/C Dm/Bb_Dm/A Gm_Dm/F Em7b5_A7b13)
```

---

## 9. Chord Diagrams (Guitar Voicings)

- **Show diagram for a single chord**: Add a period `.` after the chord (`A B7. C D .`).
- **Show diagrams for an entire line**: Start the line with a period (`. A B C D`).
- **Define a custom chord diagram**:
  - Frets only: `// C7 x32310`
  - Frets + fingering (12 chars): `// C7 x32310032410`
