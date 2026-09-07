`rime` is a modular, extensible input method engine in cross-platform C++ code, built on top of open-source technologies.

## Core

|Package|Feature|
|-------|-------|
|`librime`|Rime core engine library|
|`fcitx5-rime`|Fcitx5 rime backend plugin|

## Data

|Location|Purpose|
|--------|-------|
|`/usr/share/rime-data`|System-wide data (managed by package manager, read-only)|
|`~/.local/share/fcitx5/rime`|User-specific data (customisation, overrides system data)|

System-wide data includes the following schema packages:

|Package|Feature|
|-------|-------|
|`rime-prelude`|Essential configuration|
|`rime-essay`|Shared vocabulary|
|`rime-stroke`|Stroke input schema|
|`rime-cangjie`|Cangjie input schema|
|`rime-luna-pinyin`|Luna Pinyin input schema|
|`rime-terra-pinyin`|Terra Pinyin input schema|
|`rime-bopomofo`|Bopomofo input schema|
|`rime-quick`|Quick input schema|
|`rime-emoji`|Emoji input support|

## Related Links

- [Rime Official Documentation](https://rime.im/docs)