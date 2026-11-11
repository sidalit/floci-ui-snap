<div align="center">

<img src="snap/gui/floci-ui.png" alt="Floci UI logo" width="128" />

# Floci UI

**The web console for the Floci local cloud emulators.**

[![floci-ui](https://snapcraft.io/floci-ui/badge.svg)](https://snapcraft.io/floci-ui)
[![Base: core26](https://img.shields.io/badge/Base-core26-2C8C3C?logo=canonical&logoColor=white)](https://snapcraft.io/core26)
![Confinement: strict](https://img.shields.io/badge/Confinement-strict-2C8C3C)
[![Maintainer: sidaliteir](https://img.shields.io/badge/Maintainer-sidaliteir-2C8C3C?logo=snapcraft&logoColor=white)](https://snapcraft.io/publisher/sidaliteir)
![Architectures: amd64 and arm64](https://img.shields.io/badge/Architectures-amd64%20%7C%20arm64-2C8C3C?logo=linux&logoColor=white)

[Getting Started](#getting-started) · [Configure](#configure) · [Limitations](#limitations) · [Build](#build) · [Support](#support) · [License](#license)

Unofficial snap packaging for [Floci UI](https://github.com/floci-io/floci-ui), a browser console for the resources in the Floci AWS, Azure, GCP and OCI emulators.

</div>

---

## Getting Started

<a href="https://snapcraft.io/floci-ui"><img alt="Get it from the Snap Store" src="https://snapcraft.io/en/dark/install.svg" width="180"></a>

```bash
sudo snap install floci-ui
sudo snap install floci
```

Open [http://127.0.0.1:4500](http://127.0.0.1:4500). The service starts automatically. The second command installs the AWS emulator, which the console finds on its default port.

The console looks for each emulator on this machine: Floci (AWS) on port 4566, Floci-AZ on 4577, Floci-GCP on 4588 and Floci-OCI on 4599. A cloud whose emulator is not running shows as `Not connected`, and connects without a restart once the emulator is up.

This is the same console that Floci starts as a Docker container at `/_floci/ui`. The snap runs it as a service and needs no Docker.

## Configure

```bash
sudo snap set floci-ui port=4600 aws-endpoint=http://127.0.0.1:4567
sudo snap logs floci-ui
```

| Option | Default | Purpose |
|---|---|---|
| `addr` | `127.0.0.1` | Listen address: an IP address or hostname |
| `port` | `4500` | Console port, 1 to 65535 |
| `aws-endpoint` | `http://127.0.0.1:4566` | URL of the Floci (AWS) emulator |
| `azure-endpoint` | `http://127.0.0.1:4577` | URL of the Floci-AZ emulator |
| `gcp-endpoint` | `http://127.0.0.1:4588` | URL of the Floci-GCP emulator |
| `oci-endpoint` | `http://127.0.0.1:4599` | URL of the Floci-OCI emulator |
| `region` | `us-east-1` | AWS region the console works in |
| `allow-unsafe-network-exposure` | `false` | Required to bind outside loopback |

Endpoints are `http://` or `https://` URLs without a trailing slash. Changes restart an enabled or running service. To reach the console from other devices at `http://<computer-ip>:4500` on a trusted development network:

```bash
sudo snap set floci-ui addr=0.0.0.0 allow-unsafe-network-exposure=true
```

Other [upstream variables](https://github.com/floci-io/floci-ui#configuration), such as `FLOCI_AZURE_ACCOUNT_NAME`, `FLOCI_GCP_PROJECT` or `FLOCI_DEFAULT_ACCOUNT_ID`, go in `/var/snap/floci-ui/common/config/floci-ui.env` as `NAME=value` lines; run `sudo snap restart floci-ui` after editing. The options above take precedence over that file.

The console keeps no data of its own. Resources live in the emulators, and preferences such as the theme and the selected account stay in your browser.

## Limitations

- The console has no login. Anyone who can reach it can read and change every emulated resource, including secrets. `allow-unsafe-network-exposure` is a check made by this snap, not an upstream feature.
- The console that Floci starts itself with Docker also uses port 4500. Use one of the two, or move this one with `port`.
- HTTPS is not served, and the console must sit at the root of its own origin. Behind a reverse proxy, give it a hostname of its own instead of a path prefix.
- The browser loads the interface fonts from Google Fonts and falls back to system fonts without internet access.
- Remote access also requires the chosen port to be allowed by your firewall.

## Build

```bash
git clone https://github.com/sidalit/floci-ui-snap.git
cd floci-ui-snap
sudo snap install snapcraft --classic
snapcraft pack
```

## Support

- **Installation or snap issues:** [open a packaging issue](https://github.com/sidalit/floci-ui-snap/issues).
- **Application bugs:** [report them upstream](https://github.com/floci-io/floci-ui/issues).

## License

Snap packaging: [MIT](https://github.com/sidalit/floci-ui-snap/blob/main/LICENSE).
