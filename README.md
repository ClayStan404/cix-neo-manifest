# CIX Neo Manifest

Minimal Android `repo` manifest for the native ARM64 Debian build system.

The default manifest currently contains:

- CIX Linux kernel
- CIX GPU kernel driver used by the GPU DKMS package
- CIX Neo build scripts
- CIX Neo Debian packaging metadata

## Initialize a workspace

```bash
mkdir cix-neo-bs
cd cix-neo-bs

repo init \
  -u git@github.com:ClayStan404/cix-neo-manifest.git \
  -b master

repo sync --current-branch --no-tags
```

Access to the internal CIX Git mirror is required to synchronize the source
projects declared by the manifest. Because this manifest repository is
private, the host must also have an SSH key authorized for the GitHub account
or organization that can access it.

The build scripts and Debian packaging repositories are temporarily hosted on
GitHub. Their manifest entries will move to the internal Git service when the
new build system is ready and the internal projects have been created.
