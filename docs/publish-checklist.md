# Chrome Web Store publication checklist

This is an operator checklist. Completing it requires an authenticated Chrome Web Store developer account and public web hosting; this repository does not perform any Dashboard action or publish any URL.

## 1. Build the upload package

- [ ] Run `bun run package`.
- [ ] Upload `release/tab-lifecycle-<manifest-version>.zip`. The ZIP must open with `manifest.json` at its root, not inside a `dist/` directory.
- [ ] Do not add `release/` or its generated ZIP to version control.

## 2. Prepare the Store listing

- [ ] **[User-owned: Dashboard account]** Sign in to the Chrome Web Store Developer Dashboard and upload the ZIP as a new item or update.
- [ ] **[User-owned: Dashboard entry]** Set the category to **Productivity** and provide the English and Simplified Chinese listing content that matches the extension's supported locales.
- [ ] **[User-owned: Dashboard upload]** Upload the repository's exact 128×128 store icon from `src/icons`.
- [ ] **[User-owned: Dashboard upload]** Upload `assets/store/small-promo.png` as the 440×280 small promo image.
- [ ] **[User-owned: Dashboard upload]** Upload `assets/store/screenshot-settings-zh-CN.png` (1280×800) for Simplified Chinese; add a matching English screenshot before submitting an English-localized listing, or use the dashboard's global-screenshot flow intentionally.
- [ ] **[User-owned: Dashboard upload, optional]** Upload `assets/store/marquee-promo.png` as the 1400×560 marquee promo image if a marquee tile is wanted.
- [ ] **[User-owned: Dashboard entry]** Verify that the title, description, screenshots, and promotional images describe only the implemented local tab lifecycle manager.

## 3. Complete Privacy practices

- [ ] **[User-owned: Dashboard entry]** State the narrow single purpose: managing long-inactive tabs locally through native discard, user review or an enabled automatic-close choice, and local URL recovery after a close.
- [ ] **[User-owned: Dashboard entry]** Justify the manifest permissions accurately: `alarms` schedules local lifecycle scans, `storage` retains local settings and archive records, and `tabs` reads required tab metadata and performs lifecycle actions. Use `docs/permission-rationale.md` as the supporting source.
- [ ] **[User-owned: Dashboard entry]** Confirm the remote-code declaration against the uploaded package. For the current local-only implementation, select that no remote code is used.
- [ ] **[User-owned: Dashboard entry]** Complete the data-use and Limited Use certifications truthfully. Disclose the local processing and storage of tab URLs, titles, and related lifecycle metadata as described in `docs/privacy-policy.md`; do not claim that data is sent to a service.
- [ ] **[User-owned: public HTTPS hosting]** Host `docs/privacy-policy.md` unchanged or equivalently on a public HTTPS URL, then enter that exact URL in the Dashboard privacy-policy field. No hosting or policy URL is supplied by this repository.

## 4. Set distribution and support

- [ ] **[User-owned: Dashboard entry]** Complete every Distribution field, including the intended visibility, countries/regions, and any pricing choice. Select only the distribution terms the account owner intends to support.
- [ ] **[User-owned: Dashboard support]** Configure a monitored support path in the Dashboard—its Support hub and/or a support URL—and ensure the responsible owner can receive and respond to users. Do not use a placeholder contact or URL.
- [ ] **[User-owned: developer account]** Confirm the developer account's contact details and review notifications are monitored.

## 5. Submit

- [ ] **[User-owned: final Dashboard action]** Recheck the uploaded package and all Dashboard fields, then select **Submit for review**. Choose immediate or deferred publishing intentionally.

## Official references

- [Publish in the Chrome Web Store](https://developer.chrome.com/docs/webstore/publish)
- [Complete your listing information](https://developer.chrome.com/docs/webstore/cws-dashboard-listing)
- [Fill out the privacy fields](https://developer.chrome.com/docs/webstore/cws-dashboard-privacy)
- [Chrome Web Store Program Policies](https://developer.chrome.com/docs/webstore/program-policies/policies)
