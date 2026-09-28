# 工作记录仪 / Work Timeline Tracker

[简体中文](#简体中文) · [English](#english)

🌐 **[在线使用 / Live Demo](https://seaout.github.io/worklog-timeline/)**

## 简体中文

工作记录仪基于 [adtpdn/work-timeline](https://github.com/adtpdn/work-timeline) 修改和扩展。原项目提供了单文件时间轴与任务管理的基础实现；本项目在此基础上重新设计了界面，并加入每日记录、任务拖拽排序、多轨道时间轴、搜索、主题与语言设置、数据导入导出等功能。所有功能都包含在 `工作记录仪.html` 中，可离线使用，无需安装、注册或连接服务器。

## 快速开始

1. 用较新的 Chrome 或 Edge 打开 `工作记录仪.html`。首次打开会显示一个名为「工作记录仪」的空白工作区和「待办」阶段。

2. 点击「＋ 阶段」建立分类，再点击「＋ 任务」填写名称、所属阶段、开始日期和结束日期。

3. 点击时间轴上的任务条，在下方的「任务详情」编辑日期、状态、阶段、描述和子任务。右侧「每日记录」填写当天的内容。

4. 编辑结束后点击顶部「保存 JSON」，确认浏览器已经下载文件。下次打开 HTML 时，点击「导入 JSON」选择这份文件继续使用。

> **任务和日志不会自动保存。** 当前数据只在打开的页面内存中；刷新或关闭页面前，请下载 JSON 备份。主题和分栏尺寸会保存在当前浏览器，但不包含任务与日志。

新增任务时会记住上次成功创建任务所选的阶段；连续录入同一阶段无需重复选择。若该阶段已删除，会优先使用当前选中任务所属阶段，否则选择第一个阶段。

## 时间轴与任务

### 阶段和轨道

* 阶段左侧的「⋮⋮」是排序握柄，上下拖动它可调整阶段顺序；点击小色块可更改阶段颜色，点击阶段名称可编辑或删除阶段。

* 日期不重叠的多个任务可以放在同一轨道。将任务拖到其他轨道、轨道之间或另一个阶段，可改变它的位置；出现日期重叠时会自动建立新轨道。没有任务的轨道会自动清理。

* 删除阶段会一并删除其中的任务，页面会先询问确认；删除单个任务也需要确认。

### 拖动任务

| 操作         | 结果                   |
| ---------- | -------------------- |
| 左右拖动任务条中部  | 起止日期一起移动，任务持续天数不变    |
| 拖动任务条左端或右端 | 只调整开始日期或结束日期，任务最短为一天 |
| 上下拖动任务条    | 更换轨道，或拖到另一阶段         |

横向位移超过当前日期宽度的一半，才会跨到相邻一天。拖动时会显示目标日期和阶段，松手后才应用修改。缩放得很小时，仍可在「任务详情」的日期栏精确输入日期。拖动超出当前显示范围时，时间轴会扩展范围以显示任务。

选中任务后按 **Ctrl+C**（macOS 为 **⌘C**）复制，移动日期游标，再按 **Ctrl+V**（macOS 为 **⌘V**）粘贴。副本从游标日期开始，保持原任务的持续天数、名称和所属阶段；原轨道可容纳时沿用原轨道，日期重叠时新建轨道。超出显示范围会自动扩展，任务及子任务均获得新 ID。新建工作区或导入、合并 JSON 后，复制缓冲区会清空。

### 日期与缩放

* 「显示起点」「显示终点」决定当前时间轴窗口；填写后点击「设定范围」。它们是显示设置，不会修改任务日期。

* 拖动「缩放」滑块或点击两侧的加减按钮，可改变每天在时间轴上的宽度。按住 **Alt** 并在时间轴上滚动鼠标滚轮，会以鼠标位置为中心缩放；普通滚轮仍用于滚动。

* 点击或按住拖动顶部日期标尺可选择查看日期；日期文字不会被选中。也可使用「查看日期」、前后一天按钮或「今天」。选中日期会以亮色方块和竖线标示，周一会加粗并有周起始线。

* 在时间轴空白处按住鼠标拖动，可横向浏览。右侧日志的日期与时间轴当前查看日期对应。

## 每日记录

右侧按「今日完成」「遇到的问题」「明日计划」「备注」记录内容。前三组可以逐条添加，条目自动编号；在条目末尾按 **Enter** 新增下一条，按 **Shift+Enter** 在当前条内换行，空条目按 **Backspace** 可删除。点击「载入昨日计划 → 今日完成」会把昨天非空的计划复制到今天的完成列表，并跳过今天已有的相同文本；昨天的记录不会被改动。

「当日相关任务」显示起止日期覆盖当天的任务，点击可跳转到任务详情。右侧按钮可以单独折叠任务列表，下面的每日记录仍可正常使用；折叠状态会留在当前浏览器。任务不会自动写入日志。

## 搜索与界面设置

顶部搜索框可查找阶段、任务名称和描述、子任务，以及日志条目和备注；点击结果可跳到对应任务或日期。底部和侧边的分隔条可调整任务详情与日志的大小，双击分隔条恢复默认尺寸，两栏也可以分别收起。

在「设置」中可以选择简体中文或 English，也可以选暗色、浅色或柔和主题，并分别调整界面颜色、「保存 JSON」和「添加任务」按钮颜色。界面缩放（75%～125%）调整控件大小，字体大小（80%～140%）独立调整文字；「恢复显示默认值」只把这两项恢复到 100%。界面缩放、字体大小和时间轴的每天像素数是三个独立设置。切换语言会同步切换界面、弹窗和导出 Markdown 的栏目标题；你自己输入的任务名与日志正文不会被自动翻译。语言、外观、界面与字体缩放、分栏尺寸和折叠状态保存在当前浏览器，不写入项目 JSON。

## 保存、导入和导出

| 功能                | 用途                                                       |
| ----------------- | -------------------------------------------------------- |
| 保存 JSON           | 下载完整工作区数据，包含阶段顺序、轨道、任务、子任务、每日记录、时间轴显示起止日期、当前查看日期和缩放比例    |
| 导入 JSON → 替换当前数据  | 用所选备份覆盖当前工作区，并恢复保存时的时间轴视图；操作前先保存当前内容                     |
| 导入 JSON → 合并到当前数据 | 将其他备份合进当前工作区；可一次选择多个 JSON，并扩大显示范围以涵盖当前范围、所有导入文件范围和实际数据日期 |
| 导出 Markdown       | 生成适合阅读的任务与日志文本，不能作为可恢复的完整备份                              |

合并时，同 ID 的内容采用更新时间较新的版本，不同 ID 的内容会加入；阶段顺序采用较新的排序记录。同一天的日志条目会汇合，完全相同的新增文本会跳过。同轨道出现任务日期重叠时会自动分开。合并会自动扩大显示范围，通常无需再次手动调整。旧版 JSON 可以导入，缺少轨道信息的任务会自动分配轨道；旧文件没有视图状态时，会用任务和日志日期推断可见范围，无法推断原有的空白范围。旧任务非空的负责人和链接会追加到任务描述，不会丢失；新版任务不再单独保存这两个字段。合并完成后，记得重新保存一份完整 JSON。

「任务详情」中的「保存修改」只表示页面内的修改已经应用；要保留到下次打开，仍需点击顶部「保存 JSON」。页面显示「有未保存修改」时，应先下载备份再关闭。即使页面显示已保存，也请确认浏览器确实完成了下载。

## 快捷键

| 快捷键                              | 操作                        |
| -------------------------------- | ------------------------- |
| Ctrl+S（macOS：⌘S）                 | 下载完整 JSON                 |
| Ctrl+F（macOS：⌘F）                 | 聚焦应用内搜索框                  |
| Ctrl+C（macOS：⌘C）                 | 复制当前选中的任务                 |
| Ctrl+V（macOS：⌘V）                 | 从当前日期游标粘贴任务副本，保持持续天数和所属阶段 |
| Delete                           | 删除当前选中的任务，先弹出确认窗口         |
| Ctrl+Z（macOS：⌘Z）                 | 撤销最近的内容修改                 |
| Ctrl+Shift+Z 或 Ctrl+Y（macOS：⌘⇧Z） | 重做                        |

当光标位于输入框、文本框、下拉框或可编辑区域时，复制、粘贴和 Delete 仍按正常文字编辑方式工作，不触发任务操作。任务复制仅在本次打开页面期间可用。

「新建」会清空当前页面的工作区，开始前请先保存已有内容。日期按钮中的「今天」按中国标准时间计算。时间轴范围、时间轴缩放和当前查看日期写入 JSON；主题、自定义颜色、语言、界面缩放、字体大小、分栏尺寸与折叠状态、上次新增任务所选阶段保存在当前浏览器。

## English

Work Timeline Tracker is based on [adtpdn/work-timeline](https://github.com/adtpdn/work-timeline). The original project provides a single-file timeline and basic task management. This version redesigns the interface and adds a daily journal, drag-and-drop task ordering, multiple timeline lanes, search, theme and language settings, and data import and export. Everything runs offline from `工作记录仪.html`; no installation, account, or server is required.

### Quick start

1. Open `工作记录仪.html` in a recent version of Chrome or Edge. A new workspace starts with one “To Do” phase. If the page opens in Chinese, go to **Settings → Interface language → English**.

2. Select **＋ Phase** to create a group, then **＋ Task** to enter its name, phase, start date, and end date.

3. Select a task bar to edit its dates, status, phase, description, and subtasks in **Task details**. Write entries for the selected date in the **Daily journal**.

4. Select **Save JSON** and confirm that your browser downloaded the file. Next time, open the HTML and choose **Import JSON** to continue.

> **Tasks and journal entries are not saved automatically.** They exist only in the open page until you download a JSON backup. Refreshing or closing the page can lose unsaved changes. The browser remembers appearance and layout preferences, but not your task or journal data.

The add task form remembers the phase used for the last successfully created task. If that phase was deleted, it uses the selected task’s phase or the first available phase.

### Timeline and tasks

#### Phases and lanes

* Drag the “⋮⋮” handle to reorder phases. Select the small square to change a phase’s color, or its name to edit or delete the phase.

* Tasks with nonoverlapping dates can share a lane. Drag a task onto another lane, between lanes, or into another phase to move it. A new lane is created when dates would overlap; empty lanes are removed automatically.

* Deleting a phase also deletes its tasks. The page asks for confirmation before deleting a phase or task.

#### Dragging tasks

| Action                                  | Result                                                           |
| --------------------------------------- | ---------------------------------------------------------------- |
| Drag the center of a task left or right | Move its start and end together without changing its duration    |
| Drag the left or right edge             | Change just the start or end date; a task lasts at least one day |
| Drag a task up or down                  | Change its lane or phase                                         |

A horizontal drag crosses into the next day only after moving more than half the current day width. The proposed dates and phase appear while dragging; changes apply when you release the pointer. At a very small zoom level, use the date fields in **Task details** for precise edits. If a task moves outside the visible date range, the range expands to show it.

Select a task and press **Ctrl+C** (**⌘C** on macOS), move the date cursor, then press **Ctrl+V** (**⌘V** on macOS). The copy starts on the selected date and keeps the original duration, name, and phase. It uses the original lane if the new dates fit; otherwise a new lane is created. The visible range expands if needed, and the task and all subtasks receive new IDs. Creating a new workspace or importing or merging JSON clears the task copy buffer.

#### Dates and zoom

* **Start** and **End** beside **＋ Task** set the visible timeline range. Enter both dates and select **Set range**. This changes the view, not task dates.

* Use the **Zoom** slider or its plus and minus buttons to change the width of each day. Hold **Alt** while scrolling over the timeline to zoom around the pointer; ordinary scrolling still scrolls.

* Select or drag along the date ruler to choose the journal date; its date text cannot be selected while dragging. You can also use **View date**, the previous/next day controls, or **Today**. The selected day has a highlighted label and vertical line; Mondays are bold with a week-start line.

* Drag an empty area of the timeline to scroll horizontally. The journal on the right follows the currently selected date.

### Daily journal

The journal has **Completed today**, **Issues encountered**, **Tomorrow’s plan**, and **Notes**. The first three sections contain numbered entries. Press **Enter** to add an entry, **Shift+Enter** for a line break in the current entry, or **Backspace** in an empty entry to remove it. **Copy yesterday’s plan → completed today** copies nonempty plan entries without duplicating identical text or changing yesterday’s entries.

**Tasks on this day** lists tasks whose date ranges include the selected date. Its button collapses just the task list; the journal sections below stay available. The collapsed state is saved in this browser. Selecting a task opens its details; tasks are not automatically copied into journal text.

### Search, appearance, and language

Search the phase and task names, descriptions, subtasks, journal entries, and notes from the top bar. Select a result to open its task or date. Drag the horizontal and vertical dividers to resize the details and journal panels; double-click a divider to restore its default size. Either panel can be collapsed.

Under **Settings**, choose **简体中文** or **English** and select a Dark, Light, or Soft theme. You can also customize interface colors and the **Save JSON** and **Add task** button colors. **UI scale** (75%–125%) changes control sizes; **Font size** (80%–140%) changes text size independently. **Reset display size** returns only these two values to 100%. UI scale, font size, and timeline pixels per day are three separate settings. The language choice changes the interface, dialogs, and headings and status labels in exported Markdown. Text that you typed yourself, including task names and journal entries, remains unchanged. Language, appearance, UI and font scales, panel sizes, and collapsed states are stored in this browser and are not included in the JSON backup.

### Save, import, and export

| Action                                | Purpose                                                                                                                                        |
| ------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| Save JSON                             | Download the workspace, including phases, lanes, tasks, subtasks, daily journal, visible timeline start and end, selected date, and zoom scale |
| Import JSON → Replace current data    | Replace the current workspace and restore its saved timeline view; save the current workspace first if needed                                  |
| Import JSON → Merge into current data | Combine one or more backups and expand the visible range to include the current range, all imported ranges, and actual task and journal dates  |
| Export Markdown                       | Download a readable task and journal document in the current interface language; it is not a restorable backup                                 |

When merging, matching IDs use the more recently updated content and new IDs are added. The newer phase ordering is used; journal entries for the same date are combined, and identical new text is skipped. If merged tasks overlap in one lane, they are moved apart automatically. The visible range expands automatically, so you usually do not need to set it again. Older JSON backups are accepted; tasks without lane information are assigned lanes. For backups without a saved view, the visible range is inferred from task and journal dates; an empty part of the old view cannot be recovered. Nonempty assignee and link values in old tasks are appended to their descriptions and are no longer stored as separate task fields. Save a new complete JSON backup after a merge.

**Apply changes** in Task details only applies edits to the current page. You still need **Save JSON** to keep them for the next session. If the page shows **Unsaved changes**, download a backup before closing. Confirm that the browser finished the download even if the page displays “Saved.”

### Keyboard shortcuts

| Shortcut                            | Action                                                                     |
| ----------------------------------- | -------------------------------------------------------------------------- |
| Ctrl+S (macOS: ⌘S)                  | Download the complete JSON                                                 |
| Ctrl+F (macOS: ⌘F)                  | Focus the app’s search box                                                 |
| Ctrl+C (macOS: ⌘C)                  | Copy the selected task                                                     |
| Ctrl+V (macOS: ⌘V)                  | Paste a task starting at the date cursor, retaining its duration and phase |
| Delete                              | Delete the selected task after confirmation                                |
| Ctrl+Z (macOS: ⌘Z)                  | Undo the latest content change                                             |
| Ctrl+Shift+Z or Ctrl+Y (macOS: ⌘⇧Z) | Redo                                                                       |

Inside an input, text area, select box, or editable region, copy, paste, and Delete still work as normal text editing and do not trigger task actions. A copied task remains available only while the page stays open.

**New** clears the current workspace from the page, so save existing work first. **Today** uses China Standard Time. The visible range, timeline zoom, and selected date are saved in JSON. Theme, custom colors, language, UI scale, font size, panel sizes and collapsed states, and the last phase used in the add task form stay in this browser.
