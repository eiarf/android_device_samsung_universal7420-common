# Exynos 7420 common device tree
Common device tree for Exynos 7420 devices <br>

Based off the Exynos7420 source code found at https://github.com/Exynos7420/android_device_samsung_universal7420-common/tree/lineage-18.1 with various improvements

## Building Lineage 24.0 (Android 17)

I build the zeroflte ROM from the `lineage-24.0-KRNL6.18` branches of my
four repos. `manifests/lineage-24.0.xml` is the local manifest for that
tree:

```sh
repo init -u https://github.com/LineageOS/android.git -b lineage-24.0 --git-lfs --depth=1
mkdir -p .repo/local_manifests
curl -o .repo/local_manifests/s6.xml https://raw.githubusercontent.com/farovitus/android_device_samsung_universal7420-common/lineage-24.0-KRNL6.18/manifests/lineage-24.0.xml
repo sync -c -j16 --force-sync --no-tags --no-clone-bundle
bash device/samsung/universal7420-common/patches/apply.sh "$PWD"
source build/envsetup.sh
lunch lineage_zeroflte-cp2a-userdebug
m bacon
```

`patches/apply.sh` applies my changes to Lineage's own projects (one
directory per project under `patches/`); run it again after every
`repo sync`. The kernel is the prebuilt 6.18 Image in `prebuilt/`, built
outside the ROM; see `prebuilt/README`.
