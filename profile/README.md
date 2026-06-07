<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="./logo-inverse.svg">
    <img src="./logo.svg" alt="PharosVPN" width="140" height="140">
  </picture>
</p>

<h1 align="center">PharosVPN</h1>

<p align="center">
  <em>A self-hostable, open-source, dual-protocol VPN fleet platform.</em><br>
  Run your own VPN — for yourself, your family, or a whole organization.
</p>

---

Named for the **Lighthouse of Alexandria** — a trusted beacon that guided
travellers safely past hazards. PharosVPN does the same for network traffic:
a guide, not a wall.

## How it fits together

A private **controller** drives a fleet of public VPN **nodes** over outbound
mTLS, optionally hides itself behind **relays**, and serves end-users native
**clients**. The control plane has **no inbound ports** and assumes it will be
attacked; the nodes act only on cryptographically validated instructions and
keep carrying traffic even if the controller goes away.

Each user has devices, and each device holds named **profiles** — pick where you
exit (a single node, or a multi-hop **cascade** entry → mid → exit) and how you
get there: **AmneziaWG** (obfuscated WireGuard), **XRay (VLESS + REALITY)**, or
both, chosen at connect.

### Control & data plane

| Repo | Role |
|---|---|
| **[coxswain](https://github.com/PharosVPN/coxswain)** | Controller / management plane — provisions the fleet, seals per-device profiles, admin web UI |
| **[node](https://github.com/PharosVPN/node)** | VPN node agent — the data plane (AmneziaWG + XRay/REALITY), including multi-hop cascades |
| **[relay](https://github.com/PharosVPN/relay)** | Control-plane relay — fixed egress hops that hide the controller's origin |

### Clients — *caravel*

| Repo | Role |
|---|---|
| **[caravel](https://github.com/PharosVPN/caravel)** | Shared client core (Go) — profile parsing, account sync, the tunnel engine |
| **[caravel-mac](https://github.com/PharosVPN/caravel-mac)** | macOS app |
| **[caravel-linux](https://github.com/PharosVPN/caravel-linux)** | Linux desktop app (Wails) — AppImage, x86_64 + aarch64 |
| **[caravel-ios](https://github.com/PharosVPN/caravel-ios)** | iOS app |
| **[caravel-android](https://github.com/PharosVPN/caravel-android)** | Android app |
| **[caravel-opnsense](https://github.com/PharosVPN/caravel-opnsense)** | OPNsense plugin — client + server (userspace amneziawg-go) |
| **[caravel-openwrt](https://github.com/PharosVPN/caravel-openwrt)** | OpenWRT package — client + server (userspace amneziawg-go) |

### Design

| Repo | Role |
|---|---|
| **[docs](https://github.com/PharosVPN/docs)** | Platform design, the sync / profile contracts, and build conventions |

## Download

First public builds — **`v0.1.0`, pre-alpha**. You connect them to *your own*
controller; there are no PharosVPN servers.

| Platform | Build | Get it |
|---|---|---|
| **macOS** | Signed + notarized `.dmg` (Developer ID — opens cleanly) | [caravel-mac releases](https://github.com/PharosVPN/caravel-mac/releases/latest) |
| **Linux** | `.AppImage` — **x86_64 + aarch64** | [caravel-linux releases](https://github.com/PharosVPN/caravel-linux/releases/latest) |
| **Android** | Debug `.apk` (sideload; not Play-signed) | [caravel-android releases](https://github.com/PharosVPN/caravel-android/releases/latest) |
| **iOS** | TestFlight — *coming* | — |

Every repo carries a `VERSION` file and ships under semantic-version git tags
(`vX.Y.Z`); `scripts/bump-version.sh` walks you through a patch/minor/major bump.

## Principles

- **Self-hostable first.** Your controller, your nodes, your keys — no PharosVPN servers in the path.
- **Unlinkable by design.** The controller hides behind relays; nodes never trace back to it or to each other.
- **Always-on, hideable controller.** It stays up to continuously keep the fleet correct and healthy, dials out with zero inbound ports, and hides behind relays — and the data plane keeps running if it's briefly down.
- **End-to-end sealed profiles.** The controller only ever stores ciphertext; profiles are decrypted on your device.

## License

Every PharosVPN repo is **Apache-2.0**. Use it, run it, fork it, build on it.
Contributions are accepted under the DCO; no CLA.
