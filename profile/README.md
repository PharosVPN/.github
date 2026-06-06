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
| **[amneziawg-go](https://github.com/PharosVPN/amneziawg-go)** | AmneziaWG — obfuscated WireGuard, the primary data-plane transport |

### Clients — *caravel*

| Repo | Role |
|---|---|
| **[caravel](https://github.com/PharosVPN/caravel)** | Shared client core (Go) — profile parsing, account sync, the tunnel engine |
| **[caravel-mac](https://github.com/PharosVPN/caravel-mac)** | macOS app |
| **[caravel-ios](https://github.com/PharosVPN/caravel-ios)** | iOS app |
| **[caravel-android](https://github.com/PharosVPN/caravel-android)** | Android app |
| **[caravel-opnsense](https://github.com/PharosVPN/caravel-opnsense)** | OPNsense plugin — client + server (userspace amneziawg-go) |
| **[caravel-openwrt](https://github.com/PharosVPN/caravel-openwrt)** | OpenWRT package — client + server (userspace amneziawg-go) |

### Design

| Repo | Role |
|---|---|
| **[docs](https://github.com/PharosVPN/docs)** | Platform design, the sync / profile contracts, and build conventions |

## Principles

- **Self-hostable first.** Your controller, your nodes, your keys — no PharosVPN servers in the path.
- **Unlinkable by design.** The controller hides behind relays; nodes never trace back to it or to each other.
- **Ephemeral controller.** Configure the fleet, then turn the controller off — the data plane runs on its own.
- **End-to-end sealed profiles.** The controller only ever stores ciphertext; profiles are decrypted on your device.

## License

Every PharosVPN repo is **Apache-2.0**. Use it, run it, fork it, build on it.
Contributions are accepted under the DCO; no CLA.
