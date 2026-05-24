# SVT-AV1 Windows Builds

This repository builds Windows x64 executable packages from upstream
[SVT-AV1](https://gitlab.com/AOMediaCodec/SVT-AV1) GitLab releases.

The workflow checks the latest upstream release every day and can also be run
manually for a specific tag. When the target GitHub release already exists, the
scheduled job exits without rebuilding it.

## Output

Each GitHub release contains:

- `SvtAv1EncApp.exe`
- `SvtAv1Enc.dll`
- related runtime files produced in upstream `Bin/Release`
- `BUILD_INFO.txt` with the source tag, commit, and build settings

The packaged archive name is:

```text
SVT-AV1-<tag>-windows-x64.zip
```

## Manual Build

Open the `Build SVT-AV1 Windows x64` workflow and run it with:

- `tag`: optional upstream tag, for example `v4.1.0`
- `force`: rebuild and replace release assets if the release already exists

If `tag` is empty, the workflow uses the latest GitLab release.

## Build Details

The GitHub Actions job runs on `windows-2022` and follows the upstream Windows
build path:

```powershell
git clone --branch <tag> --depth 1 https://gitlab.com/AOMediaCodec/SVT-AV1.git
cd SVT-AV1/Build/windows
./build.bat 2022 release shared
```

NASM is installed with Chocolatey before the build. The upstream build writes
the final binaries to `SVT-AV1/Bin/Release`.

## Upstream Licenses

This repository only contains automation. Built SVT-AV1 binaries are subject to
the upstream SVT-AV1 license terms. See the upstream project:

- https://gitlab.com/AOMediaCodec/SVT-AV1
- https://gitlab.com/AOMediaCodec/SVT-AV1/-/blob/master/LICENSE.md
- https://gitlab.com/AOMediaCodec/SVT-AV1/-/blob/master/PATENTS.md
