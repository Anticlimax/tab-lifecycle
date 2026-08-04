# Privacy Policy / 隐私政策

**Product / 产品：** Tab Lifecycle / 标签页生命周期

**Effective date / 生效日期：** 2026-08-03

## 1. Scope and single purpose / 适用范围与单一用途

**English.** This policy describes the current data practices of the Tab Lifecycle Chrome extension. Its single purpose is to manage long-inactive tabs locally: it asks Chrome to natively discard eligible tabs first, identifies later close candidates for review or an enabled automatic-close setting, and keeps a local archive so a closed tab can be reopened from its saved address. The extension is not a cloud service and has no account system.

**简体中文。** 本政策说明 Tab Lifecycle Chrome 扩展当前的数据处理方式。它只有一个用途：在本机管理长期未访问的标签页——先让 Chrome 原生休眠符合条件的标签页，再将达到更长条件的标签页列为待关闭项，供用户审核，或在用户启用自动关闭后执行关闭；同时保留本地归档，以便根据已保存的地址重新打开已关闭的标签页。本扩展不是云服务，也没有账户系统。

## 2. Information the extension processes locally / 扩展在本机处理的信息

**English.** The extension processes the following information only inside Chrome on the device where it is installed. A URL or title can contain sensitive information, for example a search term, document name, account identifier, or query parameter.

1. **Metadata for currently open tabs.** When evaluating tabs or building a review list, the extension may process the tab's URL, title, favicon URL (when Chrome provides one), and `lastAccessed` timestamp. It may also process window metadata such as the current window ID, source window ID where applicable, and the number of tabs in a window. Temporary safety metadata—including whether a tab is active, pinned, audible, grouped, discardable, or already discarded—may be processed in memory.
   - **Purpose:** determine whether an HTTP(S) tab is eligible; apply safety rules; calculate how long it has been since the tab was last active; honor protected sites; avoid acting on the last tab in a window; show a review preview; natively discard a tab; and prepare a record only when a tab is being closed.
   - `lastAccessed` means the time Chrome reports that the tab last became active. It is **not** a record of clicks, typing, scrolling, mouse movement, touch, or other interaction.
   - The extension uses a favicon URL only as Chrome-supplied tab metadata. It does not fetch the favicon, including from the review interface, or inspect the webpage behind it.

2. **Settings and protected origins.** The extension stores the settings needed to follow the user's choices: whether the feature is enabled; discard and close thresholds; the automatic-close preference; the minimum number of open tabs to leave alone; grouped-tab protection; a pause-until time; and the archive capacity (`archiveLimit`). It also stores the exact HTTP(S) origins the user chooses to protect.
   - **Purpose:** apply the user's selected lifecycle rules locally. Protected origins are matched locally so their tabs are skipped rather than discarded or closed.

3. **Local archive records for tabs the extension closes.** A record may contain a locally generated archive ID, the tab URL, title, optional favicon URL, the time it was closed, its `lastAccessed` time, an optional source window ID, and whether the close was initiated from manual review or automatic closing.
   - **Purpose:** explain a closed tab in the archive and reopen its saved URL, preferably in the source window when that window still exists.
   - The saved tab URL is the full URL Chrome supplies for the tab and can therefore incidentally retain query parameters, including search terms. The extension does not separately inspect or collect those parameters or any search input.
   - The archive does not retain the browser's tab ID as a permanent identifier.

**简体中文。** 扩展仅在安装它的设备上的 Chrome 内处理以下信息。网址或标题可能包含敏感信息，例如搜索词、文档名称、账户标识或查询参数。

1. **当前打开标签页的元数据。** 在评估标签页或生成待审核列表时，扩展可能处理标签页的网址、标题、favicon 网址（仅在 Chrome 提供时）和 `lastAccessed` 时间戳。它也可能处理窗口元数据，例如当前窗口 ID、适用时的来源窗口 ID，以及窗口中的标签页数量。扩展还可能仅在内存中处理临时安全状态，例如标签页是否处于活动状态、已固定、正在播放声音、位于标签组中、允许休眠或已经休眠。
   - **用途：** 判断 HTTP(S) 标签页是否符合条件；执行安全规则；计算标签页自上次成为活动标签页以来经过的时间；遵守受保护网站规则；避免处理窗口中的最后一个标签页；展示审核预览；调用 Chrome 原生休眠；以及仅在将要关闭标签页时准备归档记录。
   - `lastAccessed` 是 Chrome 报告的该标签页上次成为活动标签页的时间。它**不是**点击、输入、滚动、鼠标移动、触摸或其他交互行为的记录。
   - 扩展仅将 favicon 网址作为 Chrome 提供的标签页元数据使用，包括审核界面在内都不会抓取 favicon，也不会检查其背后的网页。

2. **设置和受保护来源。** 扩展会保存实现用户选择所需的设置：功能是否启用、休眠和关闭阈值、自动关闭偏好、最少保留的打开标签页数量、标签组保护、暂停截止时间和归档容量（`archiveLimit`）。它还会保存用户选择保护的精确 HTTP(S) 来源。
   - **用途：** 在本机执行用户选择的标签页生命周期规则。受保护来源仅在本机匹配，使其标签页被跳过而不会被休眠或关闭。

3. **扩展关闭标签页时生成的本地归档记录。** 一条记录可能包含本机生成的归档 ID、标签页网址、标题、可选 favicon 网址、关闭时间、`lastAccessed` 时间、可选来源窗口 ID，以及关闭是来自人工审核还是自动关闭。
   - **用途：** 在归档中说明已关闭标签页，并根据已保存的网址重新打开它；如果来源窗口仍存在，则优先在该窗口中打开。
   - 保存的标签页网址是 Chrome 为该标签页提供的完整网址，因此可能附带保留查询参数，包括搜索词。扩展不会单独检查或收集这些参数或任何搜索输入。
   - 归档不会将浏览器的标签页 ID 作为永久标识保存。

## 3. Information the extension does not access or track / 扩展不访问或跟踪的信息

**English.** The extension does not inspect webpage body text, DOM content, page form fields, passwords, or other typed input. It does not use content scripts and does not monitor keystrokes, mouse movement, clicks, scrolling, touch, selections, or whether a page has unsaved input. It does not request or access Chrome's browsing-history permission or history database, and it does not create a general browsing-history log.

The local archive is not a general history feature. It can retain the URL and title of a tab that this extension closed until that record is removed; those entries are described in Section 2 and can still be sensitive.

**简体中文。** 扩展不会检查网页正文文本、DOM 内容、网页表单字段、密码或其他输入内容。它不使用内容脚本，也不会监控按键、鼠标移动、点击、滚动、触摸、选择操作或网页是否存在未保存输入。它不请求也不访问 Chrome 的浏览历史权限或历史数据库，并且不会创建通用浏览历史日志。

本地归档不是通用历史记录功能。它可能保留由本扩展关闭的标签页的网址和标题，直到该归档记录被删除；这些记录见第 2 节，且仍可能包含敏感信息。

## 4. Permissions and local use / 权限及本地用途

**English.** The current manifest requests exactly these permissions:

- **`tabs`:** lets the extension read the tab metadata described above—including titles, URLs, favicon URLs, `lastAccessed`, and necessary window/safety state—and use Chrome tab operations to discard, close, and reopen tabs. This information is used locally for lifecycle evaluation, review, protection rules, archiving, and restoration.
- **`storage`:** lets the extension save settings, protected origins, and archive records in `chrome.storage.local`.
- **`alarms`:** lets the Manifest V3 background service worker wake periodically to run a local lifecycle scan. An alarm does not send data anywhere.

The current manifest does **not** request host permissions, `history`, `scripting`, `webRequest`, or `sessions`, and the extension has no content scripts.

**简体中文。** 当前清单文件仅请求以下权限：

- **`tabs`：** 允许扩展读取上文所述的标签页元数据，包括标题、网址、favicon 网址、`lastAccessed` 和必要的窗口/安全状态，并使用 Chrome 的标签页操作来休眠、关闭和重新打开标签页。这些信息仅在本机用于生命周期评估、审核、保护规则、归档和恢复。
- **`storage`：** 允许扩展通过 `chrome.storage.local` 保存设置、受保护来源和归档记录。
- **`alarms`：** 允许 Manifest V3 后台 service worker 定期唤醒并运行本地生命周期扫描。闹钟不会向任何地方发送数据。

当前清单文件**不**请求主机权限、`history`、`scripting`、`webRequest` 或 `sessions`，扩展也没有内容脚本。

## 5. No transmission, accounts, or commercial sharing / 不传输、无账户、不作商业共享

**English.** This version of the extension makes no network requests for its features. It does not operate a server or backend, create accounts, require sign-in, use analytics, use telemetry, use advertising SDKs, or transmit tab metadata, settings, protected origins, or archive records to the extension's developer or any other recipient.

The extension does not sell, rent, share, or disclose this information for advertising, analytics, profiling, or commercial purposes. There is no cloud copy managed by this extension.

This statement describes the extension itself. Chrome, an operating system, device backup, an enterprise browser policy, the Chrome Web Store, and websites that a user visits are separate products or services with their own data practices; the extension does not control them.

**简体中文。** 当前版本的扩展不会为其功能发起网络请求。它不运行服务器或后端、不创建账户、不要求登录、不使用分析工具、不使用遥测、不使用广告 SDK，也不会将标签页元数据、设置、受保护来源或归档记录传输给扩展开发者或任何其他接收方。

扩展不会为广告、分析、画像或商业目的出售、出租、共享或披露这些信息。本扩展不会管理任何云端副本。

本说明仅描述扩展自身。Chrome、操作系统、设备备份、企业浏览器策略、Chrome Web Store 以及用户访问的网站，都是具有各自数据处理方式的独立产品或服务；扩展无法控制它们。

## 6. Retention and deletion / 保留与删除

**English.** Open-tab metadata is used while Chrome is evaluating tabs or showing a review list; the extension does not persist a general scan log. Settings remain in local extension storage until they are changed or cleared.

Archive retention is controlled by the user's `archiveLimit` setting. Whenever a new archive record is written, the extension keeps at most that many newest records and removes the oldest records above the configured capacity. There is no server-side retention period because the extension has no server. After a successful restore, the corresponding local archive record is removed.

The **Clear local data** control removes the extension's stored settings and archive records from local extension storage. It does not erase open tabs, website data, Chrome history, or data handled by other apps or services. Before uninstalling the extension, use this control if you want to remove the extension's local settings and archive records. Chrome and device-level retention behavior outside the extension is controlled by the browser, operating system, backups, or applicable administrator policies.

**简体中文。** 当前打开标签页的元数据仅在 Chrome 评估标签页或展示审核列表期间使用；扩展不会持久保存通用扫描日志。设置会保留在本地扩展存储中，直到被修改或清除。

归档保留由用户的 `archiveLimit` 设置控制。每当写入新的归档记录时，扩展最多保留该数量的最新记录，并删除超过已设容量的最旧记录。由于扩展没有服务器，因此不存在服务器端保留期限。成功恢复标签页后，对应的本地归档记录会被删除。

**清除本地数据**控件会从本地扩展存储中删除扩展保存的设置和归档记录。它不会删除打开的标签页、网站数据、Chrome 历史记录或其他应用和服务处理的数据。如果希望在卸载扩展前删除扩展的本地设置和归档记录，请先使用该控件。扩展无法控制 Chrome、操作系统、备份或适用管理员策略在扩展之外的数据保留方式。

## 7. Security boundary / 安全边界

**English.** The extension stores its durable data in `chrome.storage.local`, associated with the local Chrome profile. It does not independently encrypt data or provide a guarantee that local data can never be accessed. Protection of that data depends on the security of the Chrome profile, the operating-system account, the device, browser settings, and anyone or any software with access to them. Because URLs and titles may be sensitive, use an appropriately secured device and browser profile.

The extension uses local extension storage rather than a developer-operated server or `chrome.storage.sync`. It does not control Chrome profile sync, device backups, managed-browser configuration, malware, or physical access to an unlocked device.

**简体中文。** 扩展将持久数据保存在与本地 Chrome 配置文件关联的 `chrome.storage.local` 中。扩展不会自行加密数据，也不保证本地数据永远不会被访问。数据保护取决于 Chrome 配置文件、操作系统账户、设备、浏览器设置，以及能够访问它们的人员或软件的安全性。由于网址和标题可能包含敏感信息，请使用得到适当保护的设备和浏览器配置文件。

扩展使用本地扩展存储，而不是开发者运营的服务器或 `chrome.storage.sync`。它无法控制 Chrome 配置文件同步、设备备份、受管理浏览器配置、恶意软件或对已解锁设备的物理访问。

## 8. Your controls / 您的控制权

**English.** You can control the extension locally by:

- enabling or disabling lifecycle processing;
- setting discard and close thresholds, the minimum open-tab safety threshold, group protection, pause time, and archive capacity;
- adding or removing exact protected origins;
- reviewing close candidates before closing them under the default review path;
- choosing the automatic-close setting, which can close eligible candidates after its safety checks when you enable it;
- restoring available archive records; and
- using **Clear local data** to remove stored settings and archive records.

**简体中文。** 您可以在本机通过以下方式控制扩展：

- 启用或关闭生命周期处理；
- 设置休眠和关闭阈值、最少打开标签页安全阈值、标签组保护、暂停时间和归档容量；
- 添加或移除精确的受保护来源；
- 在默认审核流程下先审核待关闭项再关闭；
- 选择自动关闭设置；在您启用后，它可在安全检查通过时关闭符合条件的待关闭项；
- 恢复可用的归档记录；以及
- 使用**清除本地数据**删除已保存的设置和归档记录。

## 9. Children and general audience / 儿童与一般受众

**English.** The extension is designed for a general audience. Its local-only behavior is the same for every user: it does not run an account service, solicit personal information through a server, or use a separate data-collection service. The extension cannot independently determine a user's age. A parent or guardian who controls the relevant Chrome profile can use **Clear local data** or remove the extension. This section describes the extension's technical behavior and does not make claims about age classifications or legal compliance in every jurisdiction.

**简体中文。** 本扩展面向一般受众。它对所有用户采用相同的仅本地处理方式：不运行账户服务、不通过服务器索取个人信息，也不使用独立的数据收集服务。扩展无法自行判断用户年龄。控制相关 Chrome 配置文件的父母或监护人可以使用**清除本地数据**或移除扩展。本节仅说明扩展的技术行为，不对所有司法辖区的年龄分类或法律合规作出声明。

## 10. Changes to this policy / 本政策的变更

**English.** If a released version materially changes the information it processes, where that information is stored, whether it is transmitted, or its requested permissions, this policy should be updated before that change is published and the effective date should be revised. Review this policy when installing an update.

**简体中文。** 如果已发布版本将实质性改变其处理的信息、信息的存储位置、是否传输信息或请求的权限，应在发布该变更前更新本政策，并修改生效日期。安装更新时，请重新查看本政策。

## 11. Contact / 联系方式

**English.** For privacy inquiries, use the **Support** section of the Tab Lifecycle Chrome Web Store listing. Messages submitted through that section are received by the listing maintainer.

**简体中文。** 如有隐私相关咨询，请使用 Tab Lifecycle Chrome Web Store 商品详情页的**支持**部分。通过该部分提交的信息将由该商品详情页的维护者接收。
