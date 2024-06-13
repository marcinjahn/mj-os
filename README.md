# mj-os &nbsp; [![build-ublue](https://github.com/marcinjahn/mj-os/actions/workflows/build.yml/badge.svg)](https://github.com/marcinjahn/mj-os/actions/workflows/build.yml)

Fedora-based atomic (container-based) OS adhered to my needs, made possible by the [Universal Blue](https://universal-blue.org/) initiative and [Fedora Silverblue](https://fedoraproject.org/atomic-desktops/silverblue/).
## Installation

To rebase an existing atomic Fedora installation to the latest build:

- First rebase to the unsigned image, to get the proper signing keys and policies installed:
  ```
  rpm-ostree rebase ostree-unverified-registry:ghcr.io/marcinjahn/mj-os:latest
  ```
- Reboot to complete the rebase:
  ```
  systemctl reboot
  ```
- Then rebase to the signed image, like so:
  ```
  rpm-ostree rebase ostree-image-signed:docker://ghcr.io/marcinjahn/mj-os:latest
  ```
- Reboot again to complete the installation
  ```
  systemctl reboot
  ```

The `latest` tag will automatically point to the latest build. That build will still always use the Fedora version specified in `recipe.yml`, so you won't get accidentally updated to the next major version.

## ISO

If build on Fedora Atomic, you can generate an offline ISO with the instructions available [here](https://blue-build.org/learn/universal-blue/#fresh-install-from-an-iso).

## Verification

These images are signed with [Sigstore](https://www.sigstore.dev/)'s [cosign](https://github.com/sigstore/cosign). You can verify the signature by downloading the `cosign.pub` file from this repo and running the following command:

```bash
cosign verify --key cosign.pub ghcr.io/marcinjahn/mj-os
```
