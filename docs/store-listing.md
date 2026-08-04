# Chrome Web Store Listing Copy — Tab Lifecycle / 标签页生命周期


## English

### Short description

Put inactive tabs to sleep, review them before closing, and reopen their locally archived addresses.

### Detailed description

Tab Lifecycle has one purpose: manage long-inactive open tabs in stages. When you enable it, the extension runs local periodic scans and can use Chrome’s native tab discard for eligible inactive tabs. Older eligible tabs are placed in a review queue rather than being closed by default.

From the review queue, you decide whether to close selected tabs, hide candidates only in the currently loaded review page/view, protect a site, pin a tab, or pause lifecycle processing. Before a tab is closed, Tab Lifecycle rechecks its current browser state and writes a local archive record. If that archive write fails, the tab is left open.

A restored archive entry reopens the saved address in a new inactive tab. The extension has no account, cloud service, analytics, or telemetry, and it does not transmit tab data to a server; its settings and archive stay in local extension storage on this device.

### Key features

- **Native discard first:** Uses Chrome’s native discard action for eligible inactive tabs; the tab remains open.
- **Review before closing by default:** Tabs past the closing threshold enter a review queue. Automatic closing is available only as an explicit setting and is off by default.
- **Configurable lifecycle:** Choose the sleep threshold, review threshold, minimum number of open tabs to keep, grouped-tab protection, protected HTTP(S) origins, and archive capacity.
- **Review controls:** Scan now, pause for 24 hours, close selected tabs, hide candidates only in the currently loaded review page/view, protect a site, or pin a tab.
- **Local recovery:** Restore one or more archived entries by reopening their saved URLs. The archive is ordered newest first.
- **Local-only data:** No account, sync, cloud backup, content script, or telemetry is included in this MVP.

### Safety model

The current evaluator skips a tab when lifecycle management is disabled or paused, when its browser state is incomplete, or when it is not an eligible HTTP(S) tab. It also skips:

- the active tab;
- pinned or audible tabs;
- grouped tabs while grouped-tab protection is enabled (the default);
- tabs Chrome marks as not auto-discardable;
- the last tab in a window;
- tabs when the total open-tab count is at or below your configured minimum; and
- tabs at an exact HTTP(S) origin you have protected.

The extension evaluates live state again immediately before each close. It does not inspect page contents or detect unsaved forms, typing, clicks, scrolling, or touch input. For that reason, keep automatic closing off unless you accept the risk of closing a tab without reviewing it first.

### Local recovery

Before a close, the local archive can retain the saved full HTTP(S) URL, which can include query parameters or search terms, title, optional favicon URL, close time, Chrome’s `lastAccessed` timestamp, source-window identifier when available, and whether the close was manual or automatic. It does not separately read or collect search-box input, and it does not store page contents or a browsing-history log.

Restore reopens the saved URL in an inactive tab, preferring the original window when that window still exists. It does **not** restore a browser session, navigation history, scroll position, form data, or other page state. A site may show different content when reopened. The default archive capacity is 50 entries. When saving a new archive entry would exceed the current configured capacity, the oldest entries are removed. You can clear local settings and archived tabs from Settings.

### First use and defaults

Lifecycle management is **disabled by default**. On first use, Tab Lifecycle does not scan, discard, queue, or close tabs until you explicitly enable it in Settings.

| Setting | Default |
| --- | --- |
| Sleep threshold | 1,440 minutes (24 hours) |
| Review threshold | 10,080 minutes (7 days) |
| Automatic closing | Off |
| Minimum open tabs to keep | 10 |
| Protect grouped tabs | On |
| Protected sites | None |
| Local archive capacity | 50 entries |

Once enabled, the extension schedules a local check every 60 minutes. You can also request a scan manually.

### Limitations

- Only HTTP and HTTPS tabs are eligible for lifecycle actions; special, malformed, and unsupported URLs are skipped.
- “Last accessed” uses Chrome’s `Tab.lastAccessed`: the time the tab last **became active**. It is not click, keyboard, form, scroll, mouse, touch, or content-interaction tracking.
- Native discard and URL reopening may not preserve unsaved page state. Save work on a site before choosing to close a tab or enabling automatic closing.
- Recovery opens a URL only. This MVP does not request the `sessions` permission and does not offer full session restoration.
- The extension does not inspect page content, restore remote data, synchronize data, or provide a cloud backup.

### Permission and privacy disclosure

Tab Lifecycle requests only `alarms`, `storage`, and `tabs`. The `tabs` permission lets it use current tab titles, URLs, `lastAccessed`, and safety-related tab state locally to evaluate tabs, show the review queue, apply protected-origin rules, create local recovery records, and perform discard, close, restore, or user-requested pin actions. `alarms` schedules local periodic checks; `storage` holds local settings and the archive.

No host permissions, content scripts, `history`, `sessions`, `scripting`, `webRequest`, remote code, analytics, or telemetry are requested or included. Tab data is not transmitted to a server.

---

## 简体中文

### 简短说明

让不活跃的标签页先休眠，关闭前进入审核，并重新打开本地归档的地址。

### 详细说明

标签页生命周期只有一个用途：分阶段管理长时间未重新激活的打开标签页。启用后，扩展会在本机定期扫描，并可对符合条件的不活跃标签页调用 Chrome 原生休眠。达到更长阈值的符合条件标签页默认进入审核队列，而不是直接关闭。

你可以在审核队列中决定关闭选中的标签页、仅在当前已加载的审核页面/视图中隐藏候选项、保护网站、固定标签页，或暂停生命周期处理。每次关闭前，标签页生命周期都会重新检查浏览器中的当前状态，并先写入本地归档记录；归档写入失败时，标签页会保持打开。

恢复归档会在新的非活动标签页中重新打开保存的地址。扩展没有账户、云服务、分析或遥测，也不会将标签页数据传输到服务器；设置和归档只保存在此设备的扩展本地存储中。

### 主要功能

- **先原生休眠：** 对符合条件的不活跃标签页使用 Chrome 原生休眠，标签页仍保持打开。
- **默认先审核再关闭：** 超过关闭阈值的标签页进入审核队列。自动关闭仅在你明确开启后使用，默认关闭。
- **可配置生命周期：** 可设置休眠阈值、审核阈值、最少保留打开标签页数量、分组保护、受保护的 HTTP(S) 源和归档容量。
- **审核操作：** 可立即扫描、暂停 24 小时、关闭所选项、仅在当前已加载的审核页面/视图中隐藏候选项、保护网站或固定标签页。
- **本地恢复：** 可恢复一个或多个归档项，重新打开保存的 URL；归档按最新在前排序。
- **仅本地数据：** 此 MVP 不包含账户、同步、云备份、内容脚本或遥测。

### 安全模型

当生命周期管理被关闭或暂停、浏览器状态不完整，或标签页不是符合条件的 HTTP(S) 标签页时，当前规则会跳过该标签页。规则也会跳过：

- 当前活动标签页；
- 已固定或正在播放声音的标签页；
- 启用分组标签页保护时的分组标签页（默认启用）；
- Chrome 标记为不可自动休眠的标签页；
- 窗口中的最后一个标签页；
- 打开标签页总数不高于你设置下限时的标签页；以及
- 你保护的精确 HTTP(S) 源中的标签页。

扩展会在每次关闭前立即再次检查实时状态。它不检查页面内容，也不会检测未保存的表单、输入、点击、滚动或触摸操作。因此，除非你接受不经审核就关闭标签页的风险，否则请保持自动关闭为关闭状态。

### 本地恢复

关闭前，本地归档可保留保存的完整 HTTP(S) URL（其中可能包含查询参数或搜索词）、标题、可选 favicon URL、关闭时间、Chrome 的 `lastAccessed` 时间戳、可用时的来源窗口标识，以及关闭是手动还是自动。扩展不会单独读取或收集搜索框输入，也不保存页面内容或浏览历史日志。

恢复会在非活动标签页中重新打开保存的 URL；原窗口仍存在时优先在该窗口中打开。它**不会**恢复浏览器会话、导航历史、滚动位置、表单数据或其他页面状态；重新打开后，网站内容也可能不同。默认归档容量为 50 项。当保存新的归档项会超过当前设定容量时，最旧的归档项会被移除。你可以在“设置”中清除本地设置和已归档标签页。

### 首次使用与默认值

生命周期管理默认**关闭**。首次使用时，除非你在“设置”中明确启用它，标签页生命周期不会扫描、休眠、加入审核队列或关闭任何标签页。

| 设置 | 默认值 |
| --- | --- |
| 休眠阈值 | 1,440 分钟（24 小时） |
| 审核阈值 | 10,080 分钟（7 天） |
| 自动关闭 | 关闭 |
| 最少保留打开标签页 | 10 个 |
| 保护分组标签页 | 开启 |
| 受保护的网站 | 无 |
| 本地归档容量 | 50 项 |

启用后，扩展每 60 分钟安排一次本地检查；你也可以手动请求扫描。

### 限制

- 只有 HTTP 和 HTTPS 标签页符合生命周期操作条件；特殊、格式错误或不支持的 URL 会被跳过。
- “最后访问”使用 Chrome 的 `Tab.lastAccessed`：即标签页上一次**成为活动标签页**的时间，不是点击、键盘、表单、滚动、鼠标、触摸或页面内容交互的追踪。
- 原生休眠和通过 URL 重新打开可能无法保留未保存的页面状态。关闭标签页或开启自动关闭前，请先在网站中保存工作内容。
- 恢复只会重新打开 URL。本 MVP 不申请 `sessions` 权限，也不提供完整会话恢复。
- 扩展不检查页面内容、不恢复远程数据、不同步数据，也不提供云备份。

### 权限与隐私披露

标签页生命周期只请求 `alarms`、`storage` 和 `tabs`。`tabs` 权限让扩展仅在本机使用当前标签页标题、URL、`lastAccessed` 和与安全相关的标签页状态，用于评估标签页、显示审核队列、应用受保护源规则、创建本地恢复记录，以及执行休眠、关闭、恢复或用户要求的固定操作。`alarms` 用于安排本地定期检查；`storage` 用于保存本地设置和归档。

扩展不请求也不包含主机权限、内容脚本、`history`、`sessions`、`scripting`、`webRequest`、远程代码、分析或遥测，也不会将标签页数据传输到服务器。
