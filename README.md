# Maestro mobile tests — markolosic.github.io

End-to-end mobile web tests for [markolosic.github.io](https://markolosic.github.io), written with [Maestro](https://maestro.mobile.dev).
The flows drive a real mobile browser — **Chrome on Android** or **Safari on iOS** — and check the portfolio site the way a phone user sees it.

## Flows

| Flow | What it checks |
|------|----------------|
| `01_home_page.yaml` | Hero section loads (headline, "Let's talk", "Download CV") |
| `02_mobile_menu_navigation.yaml` | Hamburger menu navigates to Experience and Contact |
| `03_language_switch.yaml` | EN → SR → EN language toggle |
| `04_copy_email.yaml` | "Copy email" button shows the "Copied ✓" confirmation |
| `05_blog.yaml` | Blog page opens from the menu and lists posts |

`flows/subflows/open_site.yaml` launches the browser, dismisses first-run dialogs and opens the site.

## Requirements

- Maestro CLI: `curl -fsSL "https://get.maestro.mobile.dev" | bash`
- An Android emulator with Chrome, or an iOS simulator (Xcode)

## Run

```bash
# Android (Chrome) — default
maestro test flows/

# iOS (Safari)
maestro test -e BROWSER=com.apple.mobilesafari flows/

# A single flow / by tag
maestro test flows/01_home_page.yaml
maestro test --include-tags smoke flows/

# JUnit report
maestro test --format junit --output report.xml flows/
```

Override the target URL with `-e URL=https://...`.

## CI

`.github/workflows/maestro.yml` runs the suite on an Android emulator in GitHub Actions on every push, pull request and manual dispatch.
