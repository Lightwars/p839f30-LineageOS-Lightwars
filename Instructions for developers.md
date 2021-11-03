## Steps:
##### 1. Find your device tree, kernel tree, and vendor tree, [here](https://github.com/Lightwars/).
##### 2. Initialize the LineageOS Source

`repo init --depth=1 -u git://github.com/LineageOS/android.git -b lineage-16.0`

##### 3. Change repository of LineageOS if needed by removing and reclonig them, or by using [local manifest](https://forum.xda-developers.com/t/learn-about-the-repo-tool-manifests-and-local-manifests-and-5-important-tips.2329228/).

You can also clone device tree, common device tree, kernel tree, vendor tree by local manifist too.

`git clone https://github.com/Lightwars/local_manifest.git --depth 1 -b master .repo/local_manifests`

##### 4. Sync the source.

`repo sync -c --no-clone-bundle --no-tags --optimized-fetch --prune --force-sync -j8`

##### 5. Clone device tree, common device tree, kernel tree and vendor tree for ZTE Blade S6 to specific folder. Where to clone trees is told inside BoardConfig.mk file.

We need to clone device tree in device/zte/p839f30 said in [here](https://github.com/Lightwars/android_device_zte_p839f30/blame/lineage-16.0/BoardConfig.mk#L20).
We need to clone common device tree in device/zte/msm8939-common said in [here](https://github.com/Lightwars/android_device_zte_p839f30/blame/lineage-16.0/BoardConfig.mk#L18).

We need to clone kernel tree in kernel/zte/msm8939 said in [here](https://github.com/Lightwars/android_device_zte_p839f30/blame/lineage-16.0/BoardConfig.mk#L26).

We need to clone vendor tree in vendor/zte said in [here](https://github.com/Lightwars/android_device_zte_p839f30/blame/lineage-16.0/BoardConfig.mk#L52).

```
git clone -b lineage-16.0 https://github.com/Lightwars/android_device_zte_p839f30 device/zte/p839f30 --depth=1
git clone -b lineage-16.0 https://github.com/Lightwars/android_device_zte_msm8939-common device/zte/msm8939-common --depth=1
git clone -b lineage-16.0 https://github.com/Lightwars/android_kernel_zte_msm8939 kernel/zte/msm8939 --depth=1
git clone -b lineage-16.0 https://github.com/Lightwars/android_vendor_zte vendor/zte --depth=1
```

If you used local manifest to clone these trees, you must skip cloning these trees in this step.

##### 6. Run the build commands for building LineageOS

```
source build/envsetup.sh
brunch lineage_p839f30-userdebug
```

##### 7. Upload the output zip file (lineage-16.0-***-UNOFFICIAL-p839f30.zip) to a safe place
```
up(){
	curl --upload-file $1 https://transfer.sh/$(basename $1); echo
	# 14 days, 10 GB limit
}

up out/target/product/p839f30/*.zip
```
##### 8. All these steps should be inside build_rom.sh script like [this](https://github.com/Lightwars/p839f30-LineageOS-Lightwars/blob/main/build_rom.sh).
##### 9. If you want to update you device, kernel or vendor trees and learn more how to build ROMS and modify it according to your need, please check these links and search in google for more information.
https://github.com/AliHasan7671/guides/commit/33361bb2c78af01426350ef21167d742f44481fd
https://github.com/nathanchance/Android-Tools/blob/master/Guides/Building_AOSP.txt
##### 10. You can use this repository as a standard reference and edit things according to your device, ROM, and needs
