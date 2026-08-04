# Permission Rationale — Tab Lifecycle / 标签页生命周期

> **Current manifest permissions:** `alarms`, `storage`, and `tabs` only. This is ready-to-edit supporting copy for Chrome Web Store review and the product listing. It describes the current Manifest V3 MVP, not a future roadmap.

## English

### Scope and single purpose

Tab Lifecycle has one purpose: manage long-inactive open tabs in stages—native discard first, user-reviewed close later by default, and local URL recovery after a close. All processing occurs in the extension on the current device. The extension requests only the three permissions used by that purpose: `alarms`, `storage`, and `tabs`.

### `alarms`

**Why it is needed:** Manifest V3 service workers do not stay running continuously. `alarms` schedules a local periodic wake-up so the extension can check the lifecycle rules after it has been enabled.

**How it is used:** The extension creates one named alarm with a 60-minute period after installation or browser startup. When it fires, the extension performs a local lifecycle scan. If lifecycle management is disabled or paused, the scan safely exits without managing tabs.

**What it does not do:** The alarm does not contact a server, create reminders for the user, or transmit timing information.

### `storage`

**Why it is needed:** `storage` keeps the user’s lifecycle choices and local recovery archive durable across service-worker restarts and browser restarts.

**How it is used:** The extension uses `chrome.storage.local`, not Chrome sync. It stores:

- settings: enabled state; sleep and review thresholds; automatic-close choice; minimum open-tab count; grouped-tab protection; exact protected HTTP(S) origins; archive capacity; and pause-until time;
- local archive records for tabs that are closed by this extension: a generated archive ID, the full HTTP(S) URL, which can include query parameters or search terms, title, optional favicon URL, close time, Chrome `lastAccessed` time, source-window identifier when available, and manual/automatic close reason.

The archive is used only to display locally closed entries and reopen their saved URLs. A skip action hides candidates only in the currently loaded review page/view; it is not stored as a browser-session-wide setting.

The extension does not persist Chrome tab IDs as an archive identity, page bodies, form fields, keyboard or mouse events, scroll activity, or a browsing-history log. It does not separately read or collect search-box input; search terms can nevertheless appear in a saved full URL.

**User control and retention:** The archive is limited by the user-configured capacity (50 entries by default). When saving a new entry would exceed that capacity, the oldest entries are removed. After a restored tab is created, the extension attempts to remove its archive record. The “Clear local data” control removes settings and archived tabs from local extension storage.

### `tabs`

**Why it is needed:** `tabs` is necessary to evaluate open tabs safely, present a review queue, invoke Chrome’s native discard action, close user-selected or expressly opted-in automatic candidates, reopen archived URLs, and pin a reviewed tab when the user requests it.

**Data read locally and its purpose:**

| Tab data | Local purpose |
| --- | --- |
| Title | Shows an identifiable label in the review queue and local archive. |
| URL | Limits lifecycle actions to HTTP(S) URLs, applies exact protected-origin rules, shows the site in review, and saves the full address needed for local recovery. That address can include query parameters or search terms; the extension does not separately read or collect search-box input. |
| `lastAccessed` | Compares the tab’s elapsed inactive time with the user’s thresholds. Chrome defines this as when the tab last **became active**—not a record of clicks, typing, form input, scrolling, mouse movement, touch, or page-content interaction. |
| Active, pinned, audible, group, auto-discardable, discarded, and window/count state | Enforces safeguards, such as skipping active, pinned, audible, protected-group, non-discardable, last-in-window, and protected-origin tabs. |
| Optional favicon URL | Displays a browser-provided icon in review or the local archive when available. |

**Actions performed locally:** The extension queries current tabs, asks Chrome to discard eligible tabs, removes only a revalidated close candidate after a local archive write succeeds, creates an inactive tab from an archived URL during restore, and pins a tab only when the user chooses that review action. Before every close, it fetches current tab state and evaluates the safeguards again.

**Sensitive-data boundary:** Titles and URLs can be sensitive. They remain within the extension’s local processing and local storage for the purposes above. The extension has no host permissions or content scripts, so it does not read web-page bodies or inspect page DOM content.

### Explicitly not requested or included

The current MVP does **not** request or include:

- host permissions such as `http://*/*`, `https://*/*`, or `<all_urls>`;
- `activeTab`, `history`, `sessions`, `scripting`, `webRequest`, `webRequestBlocking`, or `cookies` permissions;
- content scripts or page-DOM access;
- remote code, remote configuration, accounts, cloud sync, or cloud backup;
- analytics, telemetry, advertising, sale/sharing of tab data, or transmission of tab data to a server.

In particular, the MVP does not request `sessions`; recovery reopens the locally saved URL and does not claim to restore a full browser session.

### Future permission changes

Any future version that needs a new permission must request it through Chrome’s permission flow and update the Chrome Web Store listing and privacy materials before publication. No such additional permission is part of the current manifest.

---

## 简体中文

### 范围与单一用途

标签页生命周期只有一个用途：分阶段管理长时间未重新激活的打开标签页——先原生休眠，默认后续由用户审核后再关闭，关闭后可在本地通过 URL 恢复。所有处理都在当前设备上的扩展内进行。扩展只请求完成这一用途所用的三项权限：`alarms`、`storage` 和 `tabs`。

### `alarms`

**为何需要：** Manifest V3 的 service worker 不会持续运行。`alarms` 用于安排本地定期唤醒，以便扩展在启用后检查生命周期规则。

**如何使用：** 扩展会在安装后或浏览器启动后创建一个具名闹钟，周期为 60 分钟。闹钟触发时，扩展进行一次本地生命周期扫描。如果生命周期管理已关闭或暂停，扫描会安全退出，不会管理标签页。

**不会做什么：** 闹钟不会联系服务器、创建面向用户的提醒，也不会传输时间信息。

### `storage`

**为何需要：** `storage` 用于在 service worker 或浏览器重启后，持续保存用户的生命周期设置和本地恢复归档。

**如何使用：** 扩展使用 `chrome.storage.local`，不使用 Chrome 同步。它保存：

- 设置：启用状态、休眠和审核阈值、自动关闭选择、最少打开标签页数量、分组标签页保护、精确的受保护 HTTP(S) 源、归档容量和暂停截止时间；
- 由本扩展关闭的标签页的本地归档记录：生成的归档 ID、完整 HTTP(S) URL（其中可能包含查询参数或搜索词）、标题、可选 favicon URL、关闭时间、Chrome 的 `lastAccessed` 时间、可用时的来源窗口标识，以及手动/自动关闭原因。

归档只用于显示本地关闭的条目和重新打开其保存的 URL。“跳过”操作只会在当前已加载的审核页面/视图中隐藏候选项；它不会作为覆盖整个浏览器会话的设置被保存。

扩展不会把 Chrome 标签页 ID 作为归档身份长期保存，也不保存页面正文、表单字段、键盘或鼠标事件、滚动活动或浏览历史日志。扩展不会单独读取或收集搜索框输入；但保存的完整 URL 仍可能包含搜索词。

**用户控制与保留：** 归档受用户设置的容量限制（默认 50 项）。保存新的归档项会超过该容量时，最旧的归档项会被移除。恢复后的新标签页创建成功后，扩展会尝试移除对应归档记录。“清除本地数据”会从扩展本地存储中删除设置和已归档标签页。

### `tabs`

**为何需要：** `tabs` 用于安全评估打开的标签页、展示审核队列、调用 Chrome 原生休眠、关闭用户选中或用户明确选择自动关闭的候选项、重新打开归档 URL，以及在用户要求时固定审核中的标签页。

**在本地读取的数据及用途：**

| 标签页数据 | 本地用途 |
| --- | --- |
| 标题 | 在审核队列和本地归档中显示可识别的标签。 |
| URL | 将生命周期操作限制为 HTTP(S) URL，应用精确的受保护源规则，在审核中显示网站，并保存本地恢复所需的完整地址。该地址可能包含查询参数或搜索词；扩展不会单独读取或收集搜索框输入。 |
| `lastAccessed` | 将标签页已不活跃的时长与用户阈值比较。Chrome 将其定义为标签页上一次**成为活动标签页**的时间，而不是点击、输入、表单、滚动、鼠标移动、触摸或页面内容交互的记录。 |
| 活动、固定、声音、分组、可自动休眠、已休眠以及窗口/数量状态 | 实施安全规则，例如跳过活动、固定、发声、受保护分组、不可休眠、窗口最后一个和受保护源中的标签页。 |
| 可选 favicon URL | 可用时，在审核或本地归档中显示浏览器提供的图标。 |

**仅在本地执行的操作：** 扩展查询当前标签页，请 Chrome 休眠符合条件的标签页；只有本地归档写入成功后，才移除再次验证过的关闭候选项；恢复时根据归档 URL 创建非活动标签页；仅在用户选择审核操作时固定标签页。每次关闭前，扩展都会再次获取当前标签页状态并重新评估安全规则。

**敏感数据边界：** 标题和 URL 可能包含敏感信息。它们仅为上述目的留在扩展的本地处理和本地存储中。扩展没有主机权限或内容脚本，因此不读取网页正文或检查页面 DOM 内容。

### 明确不请求或不包含的能力

当前 MVP **不**请求或包含：

- `http://*/*`、`https://*/*` 或 `<all_urls>` 等主机权限；
- `activeTab`、`history`、`sessions`、`scripting`、`webRequest`、`webRequestBlocking` 或 `cookies` 权限；
- 内容脚本或页面 DOM 访问；
- 远程代码、远程配置、账户、云同步或云备份；
- 分析、遥测、广告、出售或共享标签页数据，或将标签页数据传输到服务器。

特别地，此 MVP 不请求 `sessions`；恢复只会重新打开本地保存的 URL，并不声称可以恢复完整浏览器会话。

### 未来权限变更

如果未来版本需要新权限，必须通过 Chrome 的权限流程请求，并在发布前更新 Chrome Web Store 说明和隐私材料。当前 manifest 不含此类额外权限。
