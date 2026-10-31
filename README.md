<div align="center">

# <img src="https://img.shields.io/badge/-mini--packages-6366f1?style=flat-square&labelColor=1e293b" height="28" alt="mini-packages" /> &nbsp; A curated collection of packages for the Mini language

**Colors. Noise. Terminals. Meshes. Crypto. SQLite. Graphs.**

*Pure-Mini source. Zero hidden dependencies. Every package tested offline, documented in full, and installable with a single command.*

<br/>

[![Language](https://img.shields.io/badge/language-Mini-ec4899?style=flat-square&labelColor=1e293b)](#)
[![License](https://img.shields.io/badge/license-MIT-22c55e?style=flat-square&labelColor=1e293b)](LICENSE)
[![Packages](https://img.shields.io/badge/packages-30+-f59e0b?style=flat-square&labelColor=1e293b)](#packages)
[![Tests](https://img.shields.io/badge/tests-offline%20%C2%B7%20deterministic-3b82f6?style=flat-square&labelColor=1e293b)](#testing)

<br/>

[**Packages**](#-packages) &nbsp;·&nbsp; [**Install**](#-installation) &nbsp;·&nbsp; [**Design**](#-design-principles) &nbsp;·&nbsp; [**Authoring**](#-authoring-a-package) &nbsp;·&nbsp; [**Contributing**](#-contributing)

</div>

---

## <span style="color:#6366f1">◆</span> What this is

Mini ships with a small core: a lexer, a parser, a tree-walking interpreter, a garbage collector, and native modules for I/O, networking, threads, and the operating system. Everything above that core is a **package** — a self-contained directory of Mini source that adds a domain of functionality.

This is the canonical collection of those packages.

Every package here is:

<table>
<tr>
<td width="33%" valign="top">

### 🌿 Pure Mini first

If a feature can be written in the language, it is. Natives are used only where the language genuinely cannot reach — a file writer, a socket, a terminal ioctl — and even then, only through probed natives with graceful fallbacks.

</td>
<td width="33%" valign="top">

### 📦 Self-contained

A package imports only its own source files. It never imports from `lib/`, because `lib/` is not available at the installed path. When a helper is needed, it is inlined into the package's own `common.mini`.

</td>
<td width="33%" valign="top">

### 🎯 Deterministic

Every function is a pure function of its arguments and its seed. Same input, same output — across runs, machines, and Mini versions. No global state that drifts. No timing dependence.

</td>
</tr>
<tr>
<td valign="top">

### 🧪 Tested

Every package ships an offline test suite that runs in under a second. Tests do not touch the network, the filesystem, or the terminal. Failure messages sanitize escape bytes so a failing test never corrupts your terminal.

</td>
<td valign="top">

### 📖 Documented

Each package ships a quick-start `README.md`, a full-API `docs/reference.md`, and a `docs/coverage.md` that records the source of truth, every constant, and every known limitation.

</td>
<td valign="top">

### 🔍 Honest

No stubs. No placeholders. No `TODO`. Every function has a complete body. Every limitation is documented with a workaround. A user who reads `coverage.md` is never surprised by runtime behavior.

</td>
</tr>
</table>

---

## <span style="color:#6366f1">◆</span> Packages

### 🎨 Graphics & color

<table>
<tr><td width="180"><code><b>mini-color</b></code></td><td>

Eleven color spaces — RGB, HSL, HSV, HWB, CMYK, YUV, XYZ, LAB, LCH, OKLab, OKLCh. CSS parsing and formatting, W3C blending, manipulation, WCAG and APCA contrast, five ΔE metrics, color-vision simulation, harmony generators, multi-space gradients, CSS-147 named colors, Tailwind and Material palettes, ANSI 16/256/truecolor output.

</td></tr>
<tr><td><code><b>mini-noise</b></code></td><td>

Twenty-one modules covering every base noise — value, Perlin, simplex, OpenSimplex, Worley, Gabor, white — plus fBm and its variants, domain warping, analytic gradients, curl noise, response curves, tileable variants, blend modes, pattern primitives, terrain generation, hydraulic erosion, colormaps, PPM/PGM image I/O, and OBJ mesh export.

</td></tr>
</table>

### 🖥️ Terminal & interaction

<table>
<tr><td width="180"><code><b>mini-termios</b></code></td><td>

Raw mode, key input, escape-sequence parsing, cursor positioning, alternate screen, mouse, bracketed paste, focus tracking, event loop, box drawing, text composition, tables, layout, double-buffered screens, progress bars, extended prompt with history and tab completion, sprites, effects, animation, scene composition.

</td></tr>
<tr><td><code><b>mini-progress</b></code></td><td>

Progress bars, spinners, multi-bar coordination, in-place terminal rendering. Twelve bar styles, fourteen spinner presets, gradient support via `mini-color`.

</td></tr>
</table>

### 🧬 Data & structures

<table>
<tr><td width="180"><code><b>mini-graph</b></code></td><td>Directed and undirected graphs. Adjacency lists, BFS, DFS, Dijkstra, Bellman–Ford, topological sort, connected components, cycle detection.</td></tr>
<tr><td><code><b>mini-trie</b></code></td><td>Prefix trees. Insert, search, prefix search, longest-match, autocompletion.</td></tr>
<tr><td><code><b>mini-disjoint-set</b></code></td><td>Union–find with path compression and union by rank.</td></tr>
<tr><td><code><b>mini-lru-cache</b></code></td><td>Bounded LRU cache with O(1) lookup, insert, and eviction.</td></tr>
<tr><td><code><b>mini-fenwick-tree</b></code></td><td>Binary indexed tree. Prefix sums, range queries, point updates.</td></tr>
<tr><td><code><b>mini-segment-tree</b></code></td><td>Range queries with lazy propagation. Min, max, sum, custom combine functions.</td></tr>
<tr><td><code><b>mini-avl-tree</b></code></td><td>Self-balancing binary search tree. Insert, delete, range queries.</td></tr>
<tr><td><code><b>mini-bloom-filter</b></code></td><td>Probabilistic set membership with configurable false-positive rate.</td></tr>
<tr><td><code><b>mini-bitset</b></code></td><td>Fixed-size bit vector. Bitwise ops, popcount, iteration.</td></tr>
<tr><td><code><b>mini-ring-buffer</b></code></td><td>Fixed-size circular queue. Enqueue, dequeue, peek, overflow handling.</td></tr>
<tr><td><code><b>mini-sparse-table</b></code></td><td>O(1) range queries after O(n log n) preprocessing.</td></tr>
</table>

### ⚙️ Algorithms & computation

<table>
<tr><td width="180"><code><b>mini-math3d</b></code></td><td>Vectors (2/3/4), quaternions, matrices (3×3, 4×4), affine transforms, rays, planes, AABBs, spheres.</td></tr>
<tr><td><code><b>mini-mesh</b></code></td><td>Mutable triangle meshes. Topology, primitive builders, OBJ/PLY/STL I/O. <em>Depends on</em> <code>mini-math3d</code>.</td></tr>
<tr><td><code><b>mini-compression</b></code></td><td>Lossless compression primitives. RLE, LZ-style dictionary coding, Huffman, arithmetic coding.</td></tr>
<tr><td><code><b>mini-protocols</b></code></td><td>Wire-format encoders and decoders. Protocol Buffers, MessagePack, CBOR.</td></tr>
</table>

### 🔐 Security & encoding

<table>
<tr><td width="180"><code><b>mini-crypto</b></code></td><td>Cryptographic primitives. SHA-256, SHA-512, HMAC, PBKDF2, AES-CBC, AES-GCM, ChaCha20-Poly1305.</td></tr>
<tr><td><code><b>mini-scapy</b></code></td><td>Packet construction, parsing, raw-socket helpers. Ethernet, IPv4, IPv6, TCP, UDP, ICMP.</td></tr>
</table>

### 💾 Storage & persistence

<table>
<tr><td width="180"><code><b>mini-sqlite</b></code></td><td>Idiomatic Mini wrapper for the <code>native_sqlite</code> runtime. Connections, prepared statements, transactions, result sets.</td></tr>
<tr><td><code><b>mini-json-tools</b></code></td><td>Advanced JSON beyond <code>lib/json.mini</code>: streaming parser, JMESPath-style queries, schema validation, JSON Patch and Merge Patch.</td></tr>
</table>

### 🎮 Applications

<table>
<tr><td width="180"><code><b>mini-game-engine</b></code></td><td>Minimal 2D/3D game engine. Scene graph, sprites, tilemaps, collision, input binding, camera.</td></tr>
</table>

---

## <span style="color:#6366f1">◆</span> Installation

### From this repository

Clone the repository, then from **your project directory**:

```powershell
mini pkg install mini-color  path\to\mini-packages\packages\mini-color
mini pkg install mini-noise  path\to\mini-packages\packages\mini-noise
```

The package is copied into `.mini_packages\<name>` in your project. Any Mini script in that project can import it by name:

```mini
import "mini-color" as color;
import "mini-noise" as noise;
```

### From a fork or a local modification

```powershell
mini pkg install mini-color  .\forked-packages\mini-color
```

### List, remove, inspect

```powershell
mini pkg list
mini pkg remove mini-color
```

### Dependency graph

Some packages build on others. Install dependencies explicitly — `mini pkg install` does not currently resolve transitive dependencies.

```
mini-mesh     ──▶  mini-math3d
mini-progress ──▶  mini-color
mini-crypto   ──▶  (optional mini-hash)
mini-scapy    ──▶  (native_scapy runtime module)
mini-sqlite   ──▶  (native_sqlite runtime module)
mini-color    ──▶  (none)
mini-noise    ──▶  (none)
mini-termios  ──▶  (none)
```

---

## <span style="color:#6366f1">◆</span> Design principles

Every package in this repository follows the same six rules. They are not stylistic preferences — they are the difference between a package that works when installed and one that silently fails at import time.

<table>
<tr>
<td width="60" align="center" valign="top">
<b>01</b>
</td>
<td>

**Pure Mini first.** Every feature that can be written in the language is written in the language. Natives are reserved for I/O, sockets, threads, terminal control, OS integration, and the two database/raw-socket modules — nothing else.

</td>
</tr>
<tr>
<td align="center" valign="top"><b>02</b></td>
<td>

**Self-contained.** A package file never imports from `lib/`. When a package is installed to `.mini_packages/<name>/`, `import "lib/net.mini"` resolves to `.mini_packages/<name>/lib/net.mini`, which does not exist — and the import silently returns an empty module. Every symbol becomes `nil`, every call raises a confusing traceback. If a package needs a helper, the helper is inlined into `common.mini`.

</td>
</tr>
<tr>
<td align="center" valign="top"><b>03</b></td>
<td>

**Deterministic.** Every function is a pure function of its arguments and its seed. Same input → same output across runs, machines, and Mini versions. No global RNG state that drifts. No timing dependence. This makes packages usable for procedurally generated content, reproducible test fixtures, distributed rendering, and replay testing.

</td>
</tr>
<tr>
<td align="center" valign="top"><b>04</b></td>
<td>

**Tested.** Every package ships an offline test suite. Tests do not touch the network, the filesystem, or the terminal. Failure messages sanitize `chr(27)` to `<ESC>` so a failing test never corrupts your terminal.

</td>
</tr>
<tr>
<td align="center" valign="top"><b>05</b></td>
<td>

**Complete files.** No stubs. No placeholders. No `TODO`. Every function has a complete body. Every file shown in the documentation is a complete file.

</td>
</tr>
<tr>
<td align="center" valign="top"><b>06</b></td>
<td>

**Honest.** Every package ships `docs/coverage.md` documenting the reference source for each module, every constant used, every known limitation with a workaround, and every function whose behavior differs from the naive expectation. A user who reads the coverage document is never surprised by runtime behavior.

</td>
</tr>
</table>

---

## <span style="color:#6366f1">◆</span> Package structure

Every package in this repository follows the same layout.

```
packages/<name>/
├── README.md              Quick start, API overview, install
├── main.mini              Public entry point (imports every module)
├── api.mini               Facade class with every public function
├── common.mini            Self-contained helpers (imports nothing)
├── <topic>.mini           One module per concern
│   ...
├── docs/
│   ├── reference.md       Full API with examples
│   └── coverage.md        Source of truth, per-module limitations
├── examples/
│   └── <name>_demo.mini   End-to-end demonstration
└── tests/
    └── <name>_test.mini   Offline test suite (exit code = pass/fail)
```

### Three ways to import a package

```mini
// Full package — top-level functions plus namespaces
import "mini-color" as color;
let red = color.parse("#ff0000");

// Single module — when only one feature is needed
import "mini-color/hsl.mini" as hsl;
let c = hsl.hsl_map(120, 100, 50, 1.0);

// Selective — brings specific functions into scope
import {parse, to_hex} from "mini-color";
let hex = to_hex(parse("#ff0000")["color"]);
```

---

## <span style="color:#6366f1">◆</span> Testing

From the repository root:

```powershell
mini pkg install mini-color packages\mini-color
mini tests\mini-color_test.mini
```

From inside a package:

```powershell
mini packages\mini-color\tests\mini-color_test.mini
```

Every test suite exits `0` on all-pass, `1` on any failure, and prints `passed: N, failed: M` on the way out.

To run every package's test suite at once:

```powershell
# PowerShell
Get-ChildItem packages -Directory | ForEach-Object {
    $name = $_.Name
    $test = "packages\$name\tests\${name}_test.mini"
    if (Test-Path $test) {
        Write-Host ""
        Write-Host "▶ $name" -ForegroundColor Cyan
        mini pkg install $name packages\$name | Out-Null
        mini $test
    }
}
```

```bash
# POSIX
for dir in packages/*/; do
    name=$(basename "$dir")
    test="$dir/tests/${name}_test.mini"
    if [ -f "$test" ]; then
        echo ""
        echo "▶ $name"
        mini pkg install "$name" "$dir" > /dev/null
        mini "$test"
    fi
done
```

---

## <span style="color:#6366f1">◆</span> Authoring a package

### Required files

```
packages/<name>/
├── README.md              Install, one code example, list of modules
├── main.mini              Public entry point
├── api.mini               Facade class (recommended)
├── docs/
│   ├── reference.md       Every public function with an example
│   └── coverage.md        Source of truth and known limitations
├── examples/
│   └── <name>_demo.mini   Runs to completion on a fresh install
└── tests/
    └── <name>_test.mini   Exits 0 on all-pass, 1 on any failure
```

### The seven rules for authoring

| # | Rule |
|---|---|
| **1** | **No `lib/` imports.** Inline helpers into `common.mini`. See [Design principles, rule 02](#-design-principles). |
| **2** | **Every function has a complete body.** No stubs. No placeholders. No `TODO`. If you cannot finish a function, do not ship the module. |
| **3** | **Documented return shape.** Fallible functions return `{ok, value, error, meta}`. Infallible functions return the value directly and throw on programmer error. |
| **4** | **Actionable failure messages.** `"mini-xyz.write_file: cannot write 'path'"` — lowercase verb, module prefix, failing argument. |
| **5** | **No reserved-word identifiers.** `print`, `if`, `let`, `while`, `for`, `fun`, `return`, `class`, `import`, `from`, `as`, `try`, `catch`, `throw`, `finally`, `this`, `super`, `true`, `false`, `nil`, `and`, `or`, `not`, `in`, `break`, `continue`, `else`, `elif`, `do`, `enum`, `switch`, `case`, `default`, `struct`, `namespace`, `extends` — none may be identifiers, including namespace fields. |
| **6** | **Strict syntax.** Every `let` declares one variable. Every `import` ends with `;`. Every `if`/`while`/`for` condition is parenthesized. No `X and Y or Z` idioms. No `!` unary. No `**` operator. |
| **7** | **Test everything.** Every public function has at least one assertion. Edge cases have assertions. Failure messages are sanitized so `chr(27)` never corrupts the terminal. |

### Naming conventions

| Kind | Convention | Example |
|---|---|---|
| Functions, variables | `snake_case` | `read_file`, `max_retries` |
| Classes, types | `PascalCase` | `HttpClient`, `UserProfile` |
| Constants | `UPPER_SNAKE_CASE` | `MAX_SIZE`, `DEFAULT_TIMEOUT` |
| Module files | `snake_case.mini` | `http_client.mini` |
| Private helpers | `_` prefix | `_internal_work` |

### Submission

1. Fork the repository.
2. Add your package under `packages/<your-name>/` following the layout above.
3. `mini tests/<your-name>_test.mini` exits `0` from a fresh install.
4. The demo runs to completion on a system without network or special natives.
5. Open a pull request. Include:
   - A brief description of what the package does.
   - Native modules it depends on (if any).
   - Any known limitations not already in `docs/coverage.md`.

---

## <span style="color:#6366f1">◆</span> Contributing

### Reporting a bug

- **Minimal reproduction script.** The smallest `.mini` file that triggers the bug.
- **Exact error message.** Copy from the terminal, including line numbers.
- **Mini version.** `mini --version`.
- **Platform.** Windows, Linux, macOS, and whether WSL is in play.

### Suggesting a feature

- **The use case.** What problem does this solve? A concrete example beats a general statement.
- **Why the existing packages do not cover it.** If another package is close, say what is missing.
- **Expected API shape.** Even a one-line sketch of the function signature helps.

### Before opening a pull request

```powershell
mini pkg remove <name>
mini pkg install <name> packages\<name>
mini tests\<name>_test.mini
mini examples\<name>_demo.mini
make test
```

All five must pass. If any fails, fix the package before submitting.

---

## <span style="color:#6366f1">◆</span> Versioning

This repository does not use semantic versioning. Each package is versioned by its `docs/coverage.md` and the commit history of its directory.

A breaking change to a package is documented in that package's `README.md` under a **Changelog** section, and its `docs/coverage.md` records what changed and why.

Consumers who need stability are advised to pin to a specific commit and vendor the package into their project's `.mini_packages/` directory.

---

## <span style="color:#6366f1">◆</span> License

MIT. See [LICENSE](LICENSE) at the repository root.

Each package's `README.md` may add its own license terms if it includes code derived from a differently-licensed reference. The Mini interpreter itself is not part of this repository and is licensed separately.

---

## <span style="color:#6366f1">◆</span> Acknowledgments

The base noise algorithms in **mini-noise** derive from the published work of Ken Perlin (Perlin noise, *Improving Noise*), Steven Worley (cellular noise), Stefan Gustavson (simplex noise), Kurt Spencer (OpenSimplex), Björn Ottosson (OKLab), and Hans Theobald Beyer (hydraulic erosion).

The color space mathematics in **mini-color** derive from the CIE 1976 CIELAB standard, IEC 61966-2-1 (sRGB), and the CSS Color Module Level 4.

Each package's `docs/coverage.md` cites the specific references used.

---

<div align="center">

**Built with Mini, for Mini.**

[Back to top ↑](#-a-curated-collection-of-packages-for-the-mini-language)

</div>
