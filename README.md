

# FSJ

**FSJ** is a JavaScript serializer for the [**Ceedoku Save Format (CSF)**.](https://ceedoku.github.io/CSF-Spec-1.0.pdf)

It converts a JSON string into a CSF binary save file and automatically downloads the resulting `.csf` file.

FSJ is designed to be usable by **any JavaScript project that implements the CSF specification**.

---

## Installation

Include `fsj.js` in your webpage:

```html
<script src="fsj.js"></script>
```

FSJ has no external dependencies and runs entirely in the browser.

---

## Basic Usage

Pass FSJ a JSON string:

```js
FSJ(jsonString);
```

For example:

```js
const save = JSON.stringify({
    solution: [...],
    values: [...],
    givens: [...],
    notes: [...],
    selected: 0,
    difficulty: "easy",
    pencilMode: false,
    eraseMode: false,
    mistakes: 0,
    elapsedMs: 0,
    timerPaused: false,
    undoStack: [],
    redoStack: [],
    finished: false,
    hintcount: 0,
    hintcounter: 0,
    cooldownmoves: 0,
    cooldowntime: 30,
    cooldowntypetouse: "time",
    canusehelp: true
});

FSJ(save);
```

FSJ automatically creates and downloads a `.csf` file.

---

## How It Works

```text
JSON string
     │
     ▼
    FSJ
     │
     ├── Parse JSON
     ├── Validate data
     ├── Encode CSF fields
     ├── Calculate CRC-32C
     └── Create CSF file
             │
             ▼
        Automatic download
```

The caller does **not** need to manually create a Blob, URL, or download element.

---

## Download Filename

FSJ automatically names the generated file:

```text
ceedoku-save.csf
```

The filename can be changed in the FSJ implementation if a project requires a different default.

---

## Using FSJ in Other Projects

FSJ is not limited to Ceedoku.

Any JavaScript application can use FSJ to create CSF files, provided its data follows the CSF specification.

For example:

```js
const data = {
    solution: [...],
    values: [...],
    givens: [...],
    notes: [...],
    selected: 0,
    difficulty: "easy",
    pencilMode: false,
    eraseMode: false,
    mistakes: 0,
    elapsedMs: 0,
    timerPaused: false,
    undoStack: [],
    redoStack: [],
    finished: false,
    hintcount: 0,
    hintcounter: 0,
    cooldownmoves: 0,
    cooldowntime: 30,
    cooldowntypetouse: "time",
    canusehelp: true
};

FSJ(JSON.stringify(data));
```

This allows different applications to generate compatible CSF save files.

---

## Supported CSF Properties

FSJ currently supports the properties defined by [CSF 1.0](https://ceedoku.github.io/CSF-Spec-1.0.pdf):

| Property            | Supported |
| ------------------- | --------- |
| `solution`          | Yes       |
| `values`            | Yes       |
| `givens`            | Yes       |
| `notes`             | Yes       |
| `selected`          | Yes       |
| `difficulty`        | Yes       |
| `pencilMode`        | Yes       |
| `eraseMode`         | Yes       |
| `mistakes`          | Yes       |
| `elapsedMs`         | Yes       |
| `timerPaused`       | Yes       |
| `undoStack`         | Yes       |
| `redoStack`         | Yes       |
| `finished`          | Yes       |
| `hintcount`         | Yes       |
| `hintcounter`       | Yes       |
| `cooldownmoves`     | Yes       |
| `cooldowntime`      | Yes       |
| `cooldowntypetouse` | Yes       |
| `canusehelp`        | Yes       |


---

## CSF Version

FSJ currently generates:

```text
CEEDOKU-CSF/1
```

This corresponds to **[CSF 1.0](https://ceedoku.github.io/CSF-Spec-1.0.pdf):**.

The CSF specification defines the binary structure, key shortcodes, field widths, encoding rules, and CRC-32C checksum.

---

## Error Handling

FSJ throws an error when the supplied JSON or its data does not conform to the expected CSF structure.

Example:

```js
try {
    FSJ(jsonString);
} catch (error) {
    console.error("Failed to create CSF file:", error);
}
```

---


## Design Goals

FSJ is designed to be:

* **Simple** — one function call creates a save file.
* **Portable** — CSF files are not tied to one application.
* **Compact** — fixed-width binary fields reduce unnecessary storage.
* **Reliable** — CRC-32C detects corrupted or modified save data.
* **Dependency-free** — FSJ runs without external libraries.
* **Browser-friendly** — files are downloaded automatically.
* **Compatible** — implementations can follow the shared CSF specification.

---

## License

FSJ is an implementation of the [**Ceedoku Save Format (CSF)** Specification.](https://ceedoku.github.io/CSF-Spec-1.0.pdf)

Anyone may implement CSF-compatible serializers and parsers according to the [CSF specification](https://ceedoku.github.io/CSF-Spec-1.0.pdf).
