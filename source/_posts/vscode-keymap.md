---
title: Visual Studio Code 常用快捷键(WIN)
date: 2017-05-05 09:59:54
tags: keymap
---

## 主命令框

`F1`或 `Ctrl+Shift+P`: 打开命令面板。在打开的输入框内，可以输入任何命令，例如：

- 按一下 `Backspace `会进入到` Ctrl+P` 模式


- 在` Ctrl+P `下输入 `> `可以进入` Ctrl+Shift+P `模式

在 `Ctrl+P` 窗口下还可以:

- 直接输入文件名，跳转到文件
- `? `列出当前可执行的动作
- `!` 显示 Errors或 Warnings，也可以 `Ctrl+Shift+M`
- `: `跳转到行数，也可以 `Ctrl+G `直接进入
- `@ `跳转到 `symbol`（搜索变量或者函数），也可以 `Ctrl+Shift+O `直接进入
- `@ `根据分类跳转 `symbol`，查找属性或函数，也可以 `Ctrl+Shift+O` 后输入`:`进入
- `#`根据名字查找 `symbol`，也可以 `Ctrl+T`



## 快捷键

### Basic Editing

| Key                  | Command                                  | Command id                               |
| -------------------- | ---------------------------------------- | ---------------------------------------- |
| **Ctrl+X**           | Cut line (empty selection)               | 剪切                                       |
| **Ctrl+C**           | Copy line (empty selection)              | 复制                                       |
| **Ctrl+Shift+K**     | Delete Line                              | 删除当前行                                    |
| **Ctrl+Enter**       | Insert Line Below                        | 向下插入空行                                   |
| **Ctrl+Shift+Enter** | Insert Line Above                        | 向上插入空行                                   |
| **Alt+Down**         | Move Line Down                           | 向下移动当前行                                  |
| **Alt+Up**           | Move Line Up                             | 向上移动当前行                                  |
| **Shift+Alt+Down**   | Copy Line Down                           | 向下插入当前行内容                                |
| **Shift+Alt+Up**     | Copy Line Up                             | 向上插入当前行内容                                |
| **Ctrl+D**           | Add Selection To Next Find Match         | `editor.action.addSelectionToNextFindMatch` |
| Ctrl+K Ctrl+D        | Move Last Selection To Next Find Match   | `editor.action.moveSelectionToNextFindMatch` |
| **Ctrl+U**           | Undo last cursor operation               | 回退光标操作位置                                 |
| Shift+Alt+I          | Insert cursor at end of each line selected | `editor.action.insertCursorAtEndOfEachLineSelected` |
| Ctrl+Shift+L         | Select all occurrences of current selection | `editor.action.selectHighlights`         |
| Ctrl+F2              | Select all occurrences of current word   | `editor.action.changeAll`                |
| **Ctrl+I**           | Select current line                      | 选中当前行内容                                  |
| Ctrl+Alt+Down        | Insert Cursor Below                      | `editor.action.insertCursorBelow`        |
| Ctrl+Alt+Up          | Insert Cursor Above                      | `editor.action.insertCursorAbove`        |
| Ctrl+Shift+\         | Jump to matching bracket                 | `editor.action.jumpToBracket`            |
| **Ctrl+]**           | Indent Line                              | 增加当前行缩进                                  |
| **Ctrl+[**           | Outdent Line                             | 减少当前行缩进                                  |
| **Home**             | Go to Beginning of Line                  | 光标定位到行首                                  |
| **End**              | Go to End of Line                        | 光标定位到行尾                                  |
| **Ctrl+End**         | Go to End of File                        | 光标定位到文件的尾部                               |
| **Ctrl+Home**        | Go to Beginning of File                  | 光标定位到文件的开头                               |
| **Ctrl+Down**        | Scroll Line Down                         | 滚动条向下移动                                  |
| **Ctrl+Up**          | Scroll Line Up                           | 滚动条向上移动                                  |
| **Alt+PageDown**     | Scroll Page Down                         | 滚动条向下移动一屏                                |
| **Alt+PageUp**       | Scroll Page Up                           | 滚动条向上移动一屏                                |
| Ctrl+Shift+[         | Fold (collapse) region                   | 折叠代码                                     |
| Ctrl+Shift+]         | Unfold (uncollapse) region               | 展开代码                                     |
| Ctrl+K Ctrl+[        | Fold (collapse) all subregions           | `editor.foldRecursively`                 |
| Ctrl+K Ctrl+]        | Unfold (uncollapse) all subregions       | `editor.unfoldRecursively`               |
| Ctrl+K Ctrl+0        | Fold (collapse) all regions              | `editor.foldAll`                         |
| Ctrl+K Ctrl+J        | Unfold (uncollapse) all regions          | `editor.unfoldAll`                       |
| Ctrl+K Ctrl+C        | Add Line Comment                         | `editor.action.addCommentLine`           |
| Ctrl+K Ctrl+U        | Remove Line Comment                      | `editor.action.removeCommentLine`        |
| **Ctrl+/**           | Toggle Line Comment                      | 注释(或取消注释)当前行代码,`//注释内容`                  |
| **Shift+Alt+A**      | Toggle Block Comment                     | 注释(或取消注释)选择代码,`/*注释内容*/`                 |
| **Ctrl+F**           | Find                                     | 查找                                       |
| **Ctrl+H**           | Replace                                  | 替换                                       |
| **F3**               | Command                                  | Command id                               |
| **Shift+F3**         | Cut line (empty selection)               | 剪切                                       |
| **Ctrl+C**           | Copy line (empty selection)              | 复制                                       |
| **Ctrl+Shift+K**     | Delete Line                              | 删除当前行                                    |
| **Ctrl+Enter**       | Insert Line Below                        | 向下插入空行                                   |
| **Ctrl+Shift+Enter** | Insert Line Above                        | 向上插入空行                                   |
| **Alt+Down**         | Move Line Down                           | 向下移动当前行                                  |
| **Alt+Up**           | Move Line Up                             | 向上移动当前行                                  |
| **Shift+Alt+Down**   | Copy Line Down                           | 向下插入当前行内容                                |

### Rich Languages Editing

| Key              | Command                     | Command id                               |
| ---------------- | --------------------------- | ---------------------------------------- |
| Ctrl+Space       | Trigger Suggest             | `editor.action.triggerSuggest`           |
| Ctrl+Shift+Space | Trigger Parameter Hints     | `editor.action.triggerParameterHints`    |
| **Shift+Alt+F**  | Format Document             | `editor.action.formatDocument`           |
| Ctrl+K Ctrl+F    | Format Selection            | `editor.action.formatSelection`          |
| F12              | Go to Definition            | `editor.action.goToDeclaration`          |
| Ctrl+K Ctrl+I    | Show Hover                  | `editor.action.showHover`                |
| Alt+F12          | Peek Definition             | `editor.action.previewDeclaration`       |
| Ctrl+K F12       | Open Definition to the Side | `editor.action.openDeclarationToTheSide` |
| Ctrl+.           | Quick Fix                   | `editor.action.quickFix`                 |
| Shift+F12        | Show References             | `editor.action.referenceSearch.trigger`  |
| F2               | Rename Symbol               | `editor.action.rename`                   |
| Ctrl+Shift+.     | Replace with Next Value     | `editor.action.inPlaceReplace.down`      |
| Ctrl+Shift+,     | Replace with Previous Value | `editor.action.inPlaceReplace.up`        |
| Shift+Alt+Right  | Expand AST Select           | `editor.action.smartSelect.grow`         |
| Shift+Alt+Left   | Shrink AST Select           | `editor.action.smartSelect.shrink`       |
| Ctrl+K Ctrl+X    | Trim Trailing Whitespace    | `editor.action.trimTrailingWhitespace`   |
| Ctrl+K M         | Change Language Mode        | `workbench.action.editor.changeLanguageMode` |

### Navigation

| Key            | Command                         | Command id                               |
| -------------- | ------------------------------- | ---------------------------------------- |
| Ctrl+T         | Show All Symbols                | `workbench.action.showAllSymbols`        |
| Ctrl+G         | Go to Line...                   | `workbench.action.gotoLine`              |
| Ctrl+P         | Go to File..., Quick Open       | `workbench.action.quickOpen`             |
| Ctrl+Shift+O   | Go to Symbol...                 | `workbench.action.gotoSymbol`            |
| Ctrl+Shift+M   | Show Problems                   | `workbench.actions.view.problems`        |
| F8             | Go to Next Error or Warning     | `editor.action.marker.next`              |
| Shift+F8       | Go to Previous Error or Warning | `editor.action.marker.prev`              |
| Ctrl+Shift+P   | Show All Commands               | `workbench.action.showCommands`          |
| Ctrl+Shift+Tab | Navigate Editor Group History   | `workbench.action.openPreviousRecentlyUsedEditorInGroup` |
| Alt+Left       | Go Back                         | `workbench.action.navigateBack`          |
| Alt+Right      | Go Forward                      | `workbench.action.navigateForward`       |

### Editor/Window Management

| Key                 | Command                              | Command id                               |
| ------------------- | ------------------------------------ | ---------------------------------------- |
| Ctrl+Shift+N        | New Window                           | `workbench.action.newWindow`             |
| Ctrl+W              | Close Window                         | `workbench.action.closeWindow`           |
| Ctrl+F4             | Close Editor                         | `workbench.action.closeActiveEditor`     |
| Ctrl+K F            | Close Folder                         | `workbench.action.closeFolder`           |
| unassigned          | Cycle Between Editor Groups          | `workbench.action.navigateEditorGroups`  |
| Ctrl+\              | Split Editor                         | `workbench.action.splitEditor`           |
| Ctrl+1              | Focus into First Editor Group        | `workbench.action.focusFirstEditorGroup` |
| Ctrl+2              | Focus into Second Editor Group       | `workbench.action.focusSecondEditorGroup` |
| Ctrl+3              | Focus into Third Editor Group        | `workbench.action.focusThirdEditorGroup` |
| Ctrl+K Ctrl+Left    | Focus into Editor Group on the Left  | `workbench.action.focusPreviousGroup`    |
| Ctrl+K Ctrl+Right   | Focus into Editor Group on the Right | `workbench.action.focusNextGroup`        |
| Ctrl+Shift+PageUp   | Move Editor Left                     | `workbench.action.moveEditorLeftInGroup` |
| Ctrl+Shift+PageDown | Move Editor Right                    | `workbench.action.moveEditorRightInGroup` |
| Ctrl+K Left         | Move Active Editor Group Left        | `workbench.action.moveActiveEditorGroupLeft` |
| Ctrl+K Right        | Move Active Editor Group Right       | `workbench.action.moveActiveEditorGroupRight` |

### File Management

| Key            | Command                        | Command id                               |
| -------------- | ------------------------------ | ---------------------------------------- |
| Ctrl+N         | New File                       | `workbench.action.files.newUntitledFile` |
| Ctrl+O         | Open File...                   | `workbench.action.files.openFile`        |
| Ctrl+S         | Save                           | `workbench.action.files.save`            |
| Ctrl+K S       | Save All                       | `workbench.action.files.saveAll`         |
| Ctrl+Shift+S   | Save As...                     | `workbench.action.files.saveAs`          |
| Ctrl+F4        | Close                          | `workbench.action.closeActiveEditor`     |
| unassigned     | Close Others                   | `workbench.action.closeOtherEditors`     |
| Ctrl+K W       | Close Group                    | `workbench.action.closeEditorsInGroup`   |
| unassigned     | Close Other Groups             | `workbench.action.closeEditorsInOtherGroups` |
| unassigned     | Close Group to Left            | `workbench.action.closeEditorsToTheLeft` |
| unassigned     | Close Group to Right           | `workbench.action.closeEditorsToTheRight` |
| Ctrl+K Ctrl+W  | Close All                      | `workbench.action.closeAllEditors`       |
| Ctrl+Shift+T   | Reopen Closed Editor           | `workbench.action.reopenClosedEditor`    |
| Ctrl+K Enter   | Keep Open                      | `workbench.action.keepEditor`            |
| Ctrl+Tab       | Open Next                      | `workbench.action.openNextRecentlyUsedEditorInGroup` |
| Ctrl+Shift+Tab | Open Previous                  | `workbench.action.openPreviousRecentlyUsedEditorInGroup` |
| Ctrl+K P       | Copy Path of Active File       | `workbench.action.files.copyPathOfActiveFile` |
| Ctrl+K R       | Reveal Active File in Windows  | `workbench.action.files.revealActiveFileInWindows` |
| Ctrl+K O       | Show Opened File in New Window | `workbench.action.files.showOpenedFileInNewWindow` |
| unassigned     | Compare Opened File With       | `workbench.files.action.compareFileWith` |

### Display

| Key           | Command                      | Command id                               |
| ------------- | ---------------------------- | ---------------------------------------- |
| F11           | Toggle Full Screen           | `workbench.action.toggleFullScreen`      |
| Ctrl+K Z      | Toggle Zen Mode              | `workbench.action.toggleZenMode`         |
| Escape Escape | Leave Zen Mode               | `workbench.action.exitZenMode`           |
| Ctrl+=        | Zoom in                      | `workbench.action.zoomIn`                |
| Ctrl+-        | Zoom out                     | `workbench.action.zoomOut`               |
| Ctrl+Numpad0  | Reset Zoom                   | `workbench.action.zoomReset`             |
| Ctrl+B        | Toggle Sidebar Visibility    | `workbench.action.toggleSidebarVisibility` |
| Ctrl+Shift+E  | Show Explorer / Toggle Focus | `workbench.view.explorer`                |
| Ctrl+Shift+D  | Show Debug                   | `workbench.view.debug`                   |
| Ctrl+Shift+G  | Show Source Control          | `workbench.view.scm`                     |
| Ctrl+Shift+X  | Show Extensions              | `workbench.view.extensions`              |
| Ctrl+Shift+U  | Show Output                  | `workbench.action.output.toggleOutput`   |
| Ctrl+Q        | Quick Open View              | `workbench.action.quickOpenView`         |
| Ctrl+Shift+F  | Show Search                  | `workbench.view.search`                  |
| Ctrl+Shift+H  | Replace in Files             | `workbench.action.replaceInFiles`        |
| Ctrl+Shift+J  | Toggle Search Details        | `workbench.action.search.toggleQueryDetails` |
| Ctrl+Shift+C  | Open New Command Prompt      | `workbench.action.terminal.openNativeConsole` |
| Ctrl+Shift+V  | Toggle Markdown Preview      | `markdown.showPreview`                   |
| Ctrl+K V      | Open Preview to the Side     | `markdown.showPreviewToSide`             |
| **Ctrl+`**    | Toggle Integrated Terminal   | workbench.action.terminal.toggleTerminal |

### Preferences

| Key           | Command                    | Command id                               |
| ------------- | -------------------------- | ---------------------------------------- |
| Ctrl+,        | Open User Settings         | `workbench.action.openGlobalSettings`    |
| unassigned    | Open Workspace Settings    | `workbench.action.openWorkspaceSettings` |
| Ctrl+K Ctrl+S | Open Keyboard Shortcuts    | `workbench.action.openGlobalKeybindings` |
| unassigned    | Open User Snippets         | `workbench.action.openSnippets`          |
| Ctrl+K Ctrl+T | Select Color Theme         | `workbench.action.selectTheme`           |
| unassigned    | Configure Display Language | `workbench.action.configureLocale`       |

### Debug

| Key           | Command                   | Command id                             |
| ------------- | ------------------------- | -------------------------------------- |
| F9            | Toggle Breakpoint         | `editor.debug.action.toggleBreakpoint` |
| F5            | Start                     | `workbench.action.debug.start`         |
| F5            | Continue                  | `workbench.action.debug.continue`      |
| Ctrl+F5       | Start (without debugging) | `workbench.action.debug.run`           |
| F6            | Pause                     | `workbench.action.debug.pause`         |
| F11           | Step Into                 | `workbench.action.debug.stepInto`      |
| Shift+F11     | Step Out                  | `workbench.action.debug.stepOut`       |
| F10           | Step Over                 | `workbench.action.debug.stepOver`      |
| Shift+F5      | Stop                      | `workbench.action.debug.stop`          |
| Ctrl+K Ctrl+I | Show Hover                | `editor.debug.action.showDebugHover`   |

### Tasks

| Key          | Command        | Command id                     |
| ------------ | -------------- | ------------------------------ |
| Ctrl+Shift+B | Run Build Task | `workbench.action.tasks.build` |
| unassigned   | Run Test Task  | `workbench.action.tasks.test`  |

### Extensions

| Key        | Command                     | Command id                               |
| ---------- | --------------------------- | ---------------------------------------- |
| unassigned | Install Extension           | `workbench.extensions.action.installExtension` |
| unassigned | Show Installed Extensions   | `workbench.extensions.action.showInstalledExtensions` |
| unassigned | Show Outdated Extensions    | `workbench.extensions.action.listOutdatedExtensions` |
| unassigned | Show Recommended Extensions | `workbench.extensions.action.showRecommendedExtensions` |
| unassigned | Show Popular Extensions     | `workbench.extensions.action.showPopularExtensions` |
| unassigned | Update All Extensions       | `workbench.extensions.action.updateAllExtensions` |



## 修改默认快捷键

打开默认键盘快捷方式设置：
`File -> Preferences -> Keyboard Shortcuts`

修改` keybindings.json`：

```json
[
  // ctrl+space 被切换输入法快捷键占用
  {
  "key": "ctrl+alt+space",
  "command": "editor.action.triggerSuggest",
  "when": "editorTextFocus"
  },
  // ctrl+d 删除一行
  {
  "key": "ctrl+d",
  "command": "editor.action.deleteLines",
  "when": "editorTextFocus"
  },
  // 与删除一行的快捷键互换
  {
  "key": "ctrl+shift+k",
  "command": "editor.action.addSelectionToNextFindMatch",
  "when": "editorFocus"
  },
  // ctrl+shift+/多行注释
  {
  "key":"ctrl+shift+/",
  "command": "editor.action.blockComment",
  "when": "editorTextFocus"
  },
  // 定制与 sublime 相同的大小写转换快捷键，需安装 TextTransform 插件
  {
  "key": "ctrl+k ctrl+u",
  "command": "uppercase",
  "when": "editorTextFocus"
  },
  {
  "key": "ctrl+k ctrl+l",
  "command": "lowercase",
  "when": "editorTextFocus"
  }
]
```


## 前端开发必备插件

- PostCSS Sorting
- stylelint
- stylefmt
- ESLint
- javascript standard format
- beautify
- Babel ES6/ES7
- Debugger for Chrome
- Add jsdoc comments
- javascript(ES6) code snippets
- vue
- weex
- Reactjs code snippets
- React Native Tools
- Npm Intellisense
- Instant Markdown
- Markdown Shortcuts
- TextTransform



## 相关参考

[官方快捷键](https://code.visualstudio.com/docs/customization/keybindings)
