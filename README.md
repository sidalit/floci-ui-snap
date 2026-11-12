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
```

Open [http://127.0.0.1:4500](http://127.0.0.1:4500). The service starts automatically and connects to each emulator once it runs, for example after `sudo snap install floci`.

## Configure

| Option | Default | Purpose |
|---|---|---|
| `addr` | `127.0.0.1` | Listen address |
| `port` | `4500` | Console port |
| `aws-endpoint` | `http://127.0.0.1:4566` | Floci (AWS) emulator |
| `azure-endpoint` | `http://127.0.0.1:4577` | Floci AZ emulator |
| `gcp-endpoint` | `http://127.0.0.1:4588` | Floci GCP emulator |
| `oci-endpoint` | `http://127.0.0.1:4599` | Floci OCI emulator |
| `region` | `us-east-1` | AWS region |
| `allow-unsafe-network-exposure` | `false` | Required to listen outside loopback |

```bash
sudo snap set floci-ui port=4600
```

Other [upstream variables](https://github.com/floci-io/floci-ui#configuration) go in `/var/snap/floci-ui/common/config/floci-ui.env`; restart the service after editing.

## Limitations

- The console has no login: keep it on loopback or a trusted network.
- Floci's own Docker console also uses port 4500; run one of the two, or change `port`.

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
