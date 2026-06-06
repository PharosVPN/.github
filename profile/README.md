<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="./logo-inverse.svg">
    <img src="./logo.svg" alt="PharosVPN" width="140" height="140">
  </picture>
</p>

<h1 align="center">PharosVPN</h1>

<p align="center">
  <em>A self-hostable, open-source, dual-protocol VPN fleet platform.</em><br>
  Run your own VPN — for yourself, or for a whole organization.
</p>

---

Named for the **Lighthouse of Alexandria** — a trusted beacon that guided
travellers safely past hazards. PharosVPN does the same for network traffic:
a guide, not a wall.

## How it fits together

A private controller drives a fleet of public VPN nodes over outbound mTLS,
reaches end-users through an optional relay, and serves them a mobile client.
The control plane has **no inbound ports** and assumes it will be attacked;
the nodes are dumb and act only on cryptographically validated instructions.

| Repo | Role |
|---|---|
| **[helm](https://github.com/PharosVPN/helm)** | Controller / management plane + admin UI |
| **[buoy](https://github.com/PharosVPN/buoy)** | VPN node agent — runs the data plane |
| **[beacon](https://github.com/PharosVPN/beacon)** | Relay — public ingress for clients |
| **[caravel](https://github.com/PharosVPN/caravel)** | Mobile client — the actual VPN app |
| **[docs](https://github.com/PharosVPN/docs)** | Platform design & build conventions |

Data plane: **AmneziaWG** (obfuscated WireGuard) + **XRay (VLESS + REALITY)**.

## License

Every PharosVPN repo is **AGPL-3.0-or-later**. Use it, run it, fork it — if you
run a modified version as a service, share your changes back. Contributions are
accepted under the DCO; no CLA.
