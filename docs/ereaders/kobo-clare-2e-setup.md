---
title: Kobo Clare 2E Setup
icon: simple/rakutenkobo
status: done
---

This guide provides a comprehensive walkthrough for setting up and optimizing your **Kobo Clara 2E**, specifically focusing on bypassing regional restrictions, enabling developer features, and installing essential third-party software.

## 1. Initial Setup & Account Bypass

Because the Kobo Store cannot process purchases in certain countries (e.g., China), you can use a SQL injection to bypass the mandatory login.

### Bypass Steps:

1.  **Factory Reset**: Go to `More > Settings > Device Information > Advanced > Factory Reset`.

2.  **Skip Wi-Fi**: On the welcome screen, select **"Don't have a Wi-Fi network?"**.

3.  **Database Modification**:

    -   Connect the Kobo to your PC via USB.

    -   Open the `.kobo/KoboReader.sqlite` file using an **SQLite** editor.
        ```shell
        $ sqlite3 .kobo/KoboReader.sqlite
        ```

    -   Execute the following command:

        ```SQL
        sqlite> INSERT INTO user(UserID, UserKey) VALUES ('1', '');
        sqlite> .exit
        ```

4.  **Restart**: Eject and reboot. The "Discover" button will appear, and the account will show as logged in (with an empty username).

## 2. Power User Tweaks

### Developer Mode

-   **Enable**: Tap the **Search** icon and type `devmodeon`.
-   **Effect**: New games and experimental features will appear under `More > Beta Features`.

### Configuration File (`Kobo eReader.conf`)

Located at: `KOBOeReader/.kobo/Kobo/Kobo eReader.conf`. Add these lines to enable specific features:

```ini
[FeatureSettings]
# Prevent the device from scanning hidden system folders for books
ExcludeSyncFolders=(\\.(?!kobo|adobe).+|([^.][^/]*/)+\\..+)
# Enable the hidden "Export Highlights" menu option
ExportHighlights=true
```

## 3. Essential Software & Plugins

### File Management & Conversion

-   **[kepubify](https://pgaskin.net/kepubify/)**: Converts standard EPUBs to Kobo-optimized EPUBs (Kepub) for faster performance.
-   **[Send to Kobo](https://send.djazz.se/)**: Wireless file transfer. *Note: Filenames must not contain Chinese characters.*

### Third-Party Apps

- [NickelMenu](https://pgaskin.net/NickelMenu/) - Adds custom shortcuts to the main menu.
- [NickelClock](https://github.com/shermp/NickelClock) - Displays a clock in the header/footer while reading.
- [KOReader](https://koreader.rocks/) - A powerful alternative document viewer (highly recommended for PDFs).
- [KoboCloud](https://github.com/fsantini/KoboCloud) - Syncs books from Dropbox, Google Drive, or pCloud.
- [Plato](https://github.com/baskerville/plato)

## 4. Custom NickelMenu Configuration

To customize your menu, edit `.adds/nm/config`. Below is a recommended setup for quick access to system toggles and games:

| **Category** | **Command Examples**                                         |
| ------------ | ------------------------------------------------------------ |
| **System**   | Reboot, Dark Mode Toggle, Screenshot Toggle                  |
| **Tools**    | Web Browser, Reading Life Statistics                         |
| **Games**    | Sketch Pad, Sudoku, Unblock It (Hua Rong Dao)                |
| **Custom**   | `menu_item :main :Send to Kobo :nickel_browser :modal :https://send.djazz.se` |

```
# ==============================================================================
# NICKELMENU CONFIGURATION
# Location: KOBOeReader/.adds/nm/config
# ==============================================================================

# --- [ MAIN MENU: SYSTEM & POWER ] ---
# Quickly reboot the device
menu_item :main :Reboot 重启 :power :reboot

# --- [ MAIN MENU: CONNECTIVITY & TOOLS ] ---
# Wireless file transfer service (Note: avoid Chinese characters in filenames)
menu_item :main :Send to Kobo :nickel_browser :modal :https://send.djazz.se

# Open the built-in web browser
menu_item :main :Browser 浏览器 :nickel_browser :modal

# View reading statistics and awards
menu_item :main :Reading Life 阅读统计 :nickel_open :reading_life:reading_life

# --- [ MAIN MENU: SETTINGS TOGGLES ] ---
# Toggle high-contrast dark mode
menu_item :main :Dark Mode 夜间模式 :nickel_setting :toggle :dark_mode

# Toggle the ability to take screenshots by pressing the power button
menu_item :main :Screenshots 截图 :nickel_setting :toggle :screenshots

# --- [ MAIN MENU: ANNOTATION SYNC ] ---
# Connects to WiFi and runs a script to export all highlights and notes
menu_item :main    :Sync Annotations 导出全部注释    :nickel_wifi     :autoconnect
  chain_success                         :cmd_spawn       :quiet:/mnt/onboard/.adds/notes/notes.sh
  chain_success                         :dbg_toast       :Syncing Notes 导出成功
  chain_failure                         :dbg_toast       :Syncing Notes 导出失败

# --- [ MAIN MENU: EXTRAS & GAMES ] ---
# Access hidden beta features and games
menu_item :main :Sketch Pad 涂鸦板 :nickel_extras :sketch_pad
menu_item :main :Sudoku 数独 :nickel_extras :sudoku
menu_item :main :Unblock It 华容道 :nickel_extras :unblock_it

# --- [ READER MENU: IN-BOOK CONTROLS ] ---
# These items appear in the menu while you are actively reading a book
menu_item :reader :Screenshots 截图 :nickel_setting :toggle :screenshots
menu_item :reader :Dark Mode 夜间模式 :nickel_setting :toggle :dark_mode
```

## 5. Dictionaries

Kobo supports custom dictionaries in the `.dicthtml` format.

-   **Path**: Place files in `KOBOeReader/.kobo/custom-dict`.
-   **Resources**: [MobileRead Custom Dict Index](https://www.mobileread.com/forums/showthread.php?t=232883) is the primary source for English-Chinese and other bilingual variants.

## References

### 1. 综合配置与新手教程

-   **[Kobo 上手配置教程 (Gist)](https://gist.github.com/Bubbu0129/92db9ad73ff32408cc41edaef1bbe130)**：涵盖基础设置的 Walkthrough 手册。
-   **[我的 Kobo 电子书阅读器设置](https://www.owenyoung.com/blog/kobo-setup/) (2023-12-03)**：Owen Young 的个人配置心得。
-   **[Kobo Libra H2O 使用体验和设置指南](https://sspai.com/post/78528) (2023-02-28)**：少数派作者“双耳鱼禾”撰写，包含详细的体验与针对性设置。
-   **[A Guide to Customize Kobo for New Simplified Chinese Readers](https://www.mobileread.com/forums/showthread.php?t=339630)**：MobileRead 社区针对简体中文用户的定制化指南，解决中文字体、排版等痛点。

### 2. 插件、扩展与开发者进阶

用于提升 Kobo 功能上限的工具与开发资源：

-   **[Kobo 電子書小外掛](https://hsuan9522.medium.com/kobo-reader-plugin-300eda218441) (2022-06-13)**：介绍了实用的 Kobo 第三方小插件。
-   **[Create your own native development environment on your Kobo!](https://www.mobileread.com/forums/showthread.php?t=336175)**：开发者向，指导如何在 Kobo 上构建原生开发环境。
-   **[Kobo_Tips (GitHub Repo)](https://github.com/Megumi-B/Kobo_Tips)**：GitHub 上的技巧汇总仓库。

