# splitchat for Linux

Downloads and the auto-update feed for the [splitchat](https://splitchat.stackedtensor.com)
desktop app: log spending by chatting, and split bills with friends.
The source is private; this repository only builds and publishes releases.

## Install

Take the newest release from [Releases](../../releases/latest).

| Package                      | For                                                             | Updates                                  |
| ---------------------------- | --------------------------------------------------------------- | ---------------------------------------- |
| `splitchat_*_amd64.AppImage` | any distro: `chmod +x`, then run it                             | **automatic**: it updates itself, signed |
| `splitchat_*_amd64.deb`      | Ubuntu 22.04+, Debian 12+: `sudo apt install ./splitchat_*.deb` | download the new `.deb` from this page   |
| `splitchat-*.x86_64.rpm`     | Fedora: `sudo dnf install ./splitchat-*.rpm`                    | download the new `.rpm` from this page   |

Builds run on Ubuntu 22.04, which needs glibc 2.35 or newer.

## If the window is blank

Some NVIDIA setups show an empty window under WebKitGTK. Two fixes:

- In splitchat, turn on **You → Desktop → Safe rendering**.
- If the window is blank before you can reach that setting, start splitchat
  once with `WEBKIT_DISABLE_DMABUF_RENDERER=1 splitchat` (or set it on the
  AppImage).
- On Wayland with NVIDIA, also try `__NV_DISABLE_EXPLICIT_SYNC=1`.

## Wayland

The optional quick-add shortcut (Ctrl+Alt+E) may not register on Wayland. Use
the tray menu, or bind your desktop's own shortcut to `splitchat`.

## Privacy

Your sign-in token is kept in your desktop's keyring (Secret Service). See
the [privacy notice](https://splitchat.stackedtensor.com/privacy).

## For maintainers

`.github/workflows/release.yml` builds a tagged splitchat source ref and
publishes a release here, with `latest.json` for the updater. It only runs
from a manual dispatch. The source is checked out with a read-only deploy key.
The updater signing key and its password are this repository's secrets, and
are kept in AWS Secrets Manager as `stackedtensor/dev/splitchat/updater`.
Runbook: `infra/docs/splitchat-desktop-release.md` in the Stackedtensor hub.
