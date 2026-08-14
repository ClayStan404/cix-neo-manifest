# CIX Neo Manifest

Minimal Android `repo` manifest for the native ARM64 Debian build system.

The default manifest contains only projects used by the current build system:

- CIX development and stable-kernel inputs
- CIX GPU, Bluetooth, VPU, NPU, ISP, and WLAN driver sources
- CIX graphics, multimedia, and AI runtime sources
- Revision-pinned Debian Salsa packaging for the Linux 7.0 media stack
- Selected CIX proprietary firmware and userspace payloads
- CIX Neo build scripts
- CIX Neo Debian packaging metadata

Projects are added incrementally when their first package target is
implemented; this manifest is not a copy of the legacy workspace manifest.
The Salsa projects preserve Debian's source-package history and package split;
CIX changes remain separate quilt overlays in the Debian metadata project.

## Initialize a workspace

Use Debian's package-managed `repo` launcher. Configure it once per user to
fetch the upstream Repo implementation from the internal CIX mirror by adding
these settings to `~/.profile`:

```bash
export REPO_URL='ssh://git@gitmirror.cixcomputing.com/android_repo/git-repo'
export REPO_REV='stable'
```

Start a new login shell or run `source ~/.profile`, then initialize and sync
the workspace:

```bash
mkdir cix-neo-bs
cd cix-neo-bs

repo init \
  -u git@github.com:ClayStan404/cix-neo-manifest.git \
  -b master

repo sync
```

The internal `stable` branch mirrors the upstream Repo implementation. Do not
use the legacy `cix-stable` branch, which loads CIX extensions that are not
part of this rewritten build system.

Access to the internal CIX Git mirror is required to synchronize the source
projects declared by the manifest. Because this manifest repository is
private, the host must also have an SSH key authorized for the GitHub account
or organization that can access it.

The build scripts and Debian packaging repositories are temporarily hosted on
GitHub. Their manifest entries will move to the internal Git service when the
new build system is ready and the internal projects have been created.
