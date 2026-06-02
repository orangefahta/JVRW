# JVRW Toolchain — Installation Guide

## Requirements

- Java 17 or higher
- Gradle 8.x
- Fabric Loom (any version compatible with your target branch)

---

## Step 1 — Download the plugin

Download the latest `jvrw-toolchain.jar` from the
[JVRW GitHub Releases](https://github.com/orangefahta/JVRW/releases).

---

## Step 2 — Add the plugin to your project

Place the downloaded JAR into your project directory:

```
your-mod/
  gradle/
    plugins/
      jvrw-toolchain.jar   ← here
  src/
  build.gradle
  settings.gradle
  jvrw.json                ← here (see Step 3)
```

---

## Step 3 — Create jvrw.json

Create a file named `jvrw.json` in the **root of your project**
(next to `build.gradle`):

```json
{
  "target": "1.21",
  "strict": false
}
```

### Fields

| Field    | Required | Description                                                                 |
|----------|----------|-----------------------------------------------------------------------------|
| `target` | ✅ Yes   | The Minecraft branch you are targeting (e.g. `"1.21"`, `"1.20"`, `"1.19"`) |
| `strict` | ❌ No    | If `true`, JVRW will throw an error when a method is not found in the diff table. Defaults to `false`. |

### Supported branches and their anchor versions

| Branch  | Anchor version |
|---------|----------------|
| `1.14`  | 1.14.4         |
| `1.15`  | 1.15.2         |
| `1.16`  | 1.16.5         |
| `1.17`  | 1.17.1         |
| `1.18`  | 1.18.2         |
| `1.19`  | 1.19.2         |
| `1.20`  | 1.20.1         |
| `1.21`  | 1.21.1         |

You only need to specify the branch. JVRW automatically uses
the correct anchor version for compilation.

---

## Step 4 — Register the plugin in settings.gradle

Add the following to your `settings.gradle`:

```groovy
buildscript {
    dependencies {
        classpath files('gradle/plugins/jvrw-toolchain.jar')
    }
}
```

---

## Step 5 — Apply the plugin in build.gradle

Add the following line to your `build.gradle`:

```groovy
apply plugin: 'dev.jvrw.toolchain'
```

---

## Step 6 — Build with JVRW

Run the following command to build your mod with JVRW support:

```bash
./gradlew build --JVRW
```

That's it. JVRW will automatically:
- Lock the project to the anchor version mappings
- Inject a JVRW marker into the output JAR
- Prepare your mod for cross-version compatibility

---

## Notes

- Do **not** change your `minecraft` version in `build.gradle` manually.
  JVRW handles version targeting automatically based on `jvrw.json`.
- The output JAR will work on **all minor versions** within your target branch
  as long as JVRW Runtime is installed by the end user.
- JVRW does **not** support cross-branch compatibility (e.g. `1.21` → `1.20`).
  Each branch requires a separate build.

---

## Need help?

Open an issue at [github.com/orangefahta/JVRW](https://github.com/orangefahta/JVRW)
