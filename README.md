# Sketchfab/ArtStation Ripper #
You can download any 3D model available on sketchfab for free using sketchfab ripper software
<br />
    <a href="https://github.com/babyroro1/Sketchfab-Ripper-/releases/latest/">Download</a>
    ·
    <img alt="Total Downloads" src="https://img.shields.io/github/downloads/babyroro1/Sketchfab-Ripper-/total?label=Downloads">
    ·
    <a href="https://github.com/babyroro1/Sketchfab-Ripper-/issues">Report Bugs</a>
  </p>
</p>
I DID NOT MAKE THIS SKETCHFAB RIPPPER

## Links: ##
- Discord: https://discord.gg/ReUnrvfdXa - If this tool is ever released elsewhere, the link in the tool's About screen (located in the options window) will automatically update.
- Version archive (does not include beta releases): https://mega.nz/folder/D1lRQY4L#_QHmdjEgAg4wMo-1vAZw6w

## Notes: ##
- An alternative to ZippyShare uploads is Telegram integration. Unlike ZippyShare, Telegram requires an account and configuration requires a few extra steps. You will need Telegram API credentials from https://my.telegram.org/apps, copy these to `tools\TelegramConfig.json`. Set the "Upload service" option to "Telegram" and you will be prompted for your account's phone number. When entered, a code should be sent to your Telegram app. Enter that code in the new prompt which appears. If you use a cloud password, an additional prompt will be shown. These login steps will only need to be performed once. Select the default chat and click "Use this chat". When the "Auto-package" option is enabled, compressed files should now be uploaded to Telegram.
- Improved vertex normal support for rigged/animated models is highly experimental, and must be enabled manually. To do so, set the "enableRiggedModeFixes" parameter in `SketchfabRipper.ini` to True. If experiencing issues, try changing the "enableFix" parameter in `tools\blender-292\_sfVertNormalsFix.py`.
- This tool is unrelated to https://sketchfab-ripper.com/, despite their page being named "Sketchfab Ripper v17.3". The free version includes a cryptocurrency miner (`AppData\synchronize.dpa`) and the paid version is a rip-off, considering that this tool and other methods are freely available.
- To improve `.blend` materials at the cost of breaking FBX textures, se    t the "EnableExtraFeatures" parameter in `tools\blender-292\_sfTex.py` to True.

## Prerequisites ##
- .NET Framework 4.8: https://go.microsoft.com/fwlink/?linkid=2088631
- Visual C++ redistributables: https://github.com/abbodi1406/vcredist/releases

## Plugins ##
Starting with v1.18.0, all site-specific code from `SketchfabRipper.exe` has been moved to separate plugins. Plugins are stored in the `plugins` folder and can be added or removed if necessary. This new system makes adding support for new sites much easier, and enables the creation of custom plugins - the https://p3d.in/ plugin's source code is included for reference. v1.18.0 includes 16 plugins:
- `AnvlPlugin.dll`: Supports characters created using https://anvl.co/. To download your own characters, click the "Share" button and paste the generated link (eg. https://anvl.co/share/12345678) into the tool.
- `ArtStationPlugin.dll`: Supports model (https://www.artstation.com/artwork/*), artist (https://www.artstation.com/[artist]) and embed (https://www.artstation.com/embed/012345678) links from ArtStation. Will only download data if a 3D viewer (Marmoset Viewer, Sketchfab) is present on the model's page.
- `CGTraderPlugin.dll`: Supports CGTrader (https://www.cgtrader.com/3d-models/*) models which contain Marmoset Viewer embeds.
- `CLOSETPlugin.dll`: Supports https://connect.clo-set.com/.
- `DayinPlugin.dll`: Supports http://www.dayin.la/.
- `GameModels3DPlugin.dll`: Supports https://gamemodels3d.com/. Models will be converted to OBJ and saved in `.zip` files regardless of whether the "Auto-package" option is set.
- `HeroForgePlugin.dll`: Supports characters created using https://www.heroforge.com/. Links must first be generated using the Hero > Share feature. 
- `NicoVideoPlugin.dll`: Supports most https://3d.nicovideo.jp/ models. Requires an account - setting `nicoEmail` and `nicoPass` in `SketchfabRipper.ini` is recommended to avoid logging in for each model.
- `P3DPlugin.dll`: Supports https://p3d.in/.
- `PlayboxPlugin.dll`: Supports https://www.aplaybox.com/. Exports in `.glb` format, bones not included. If the tool appears to be frozen, it's an issue with aplaybox's servers - the same applies to most `WebClient` errors. Retrying the download should fix most issues.
- `RigModelsPlugin.dll`: Supports https://rigmodels.com/.
- `SketchfabPlugin.dll`: For https://sketchfab.com/. Supported link formats:
    - https://sketchfab.com/[artist]
    - https://sketchfab.com/[artist]/collections/[collection]
    - https://sketchfab.com/[artist]/likes
    - https://sketchfab.com/3d-models/*
    - https://sketchfab.com/models/*
- `SketchupPlugin.dll`: Supports https://3dwarehouse.sketchup.com/. Downloads models in `.dae` format if available, otherwise Sketchup 2021 `.skp`.
- `ThreedingPlugin.dll`: Supports https://www.threeding.com/ models with a 3D viewer.
- `TurbosquidPlugin.dll`: Supports Marmoset Viewer embeds from https://www.turbosquid.com/.
- `VRoidPlugin.dll`: Supports https://hub.vroid.com/. Can download and decrypt `.vrm` (`.glb`) files, but conversion is currently not possible due to missing glTF extensions. Some older models do not use these extensions, and can be opened in software such as Blender. However, VRoidHub seems to manipulate the model with vertex shaders or JavaScript code once loaded - geometry will appear broken when opened in Blender. Future updates _may_ fix this.

Most of these plugins ignore or do not support the options from `SketchfabRipper.ini`, either because the downloaded files are already in a usable format or the options are Sketchfab-specific. It's also possible that certain sites do not provide the information necessary for some options to work - ArtStation, CGTrader, P3D.in, Sketchfab and TurboSquid provide the artist for each model, allowing the "Sort by artist" option to work. However, most other sites lack this information and the option will have no effect.

## Before reporting an issue... ##
Keep in mind that the Sketchfab conversion scripts (embedded within the tool's `BlenderScripts` class and written to `tools\blender\_sketchfab.py` at runtime) are <u>NOT</u> originally mine - I've only made some slight modifications (eg. dumping vertex normals to `_sfTemp\vertexNormalData`) to ensure compatibility with other parts of the tool. There are a number of known issues I can't fix, including but not limited to:
- Broken animations.
- Broken UVs.
- Marmoset Viewer bones and animations.
- Quad, morph target or point cloud support.
- Vertex normal issues in Rigged/Animated modes.

If your issue is related to any of the above, _please do not post about it in the Discord server_.

## Common issues: ##
> Normals appearing broken on converted models:
>
> Sketchfab compresses model data using a lossy algorithm, so certain meshes may appear broken. Static mode reads the vertex normals from the Sketchfab data if the "Apply materials" option is enabled, unlike Rigged and Animated modes which generate the normals. Since v1.15.2, Rigged and Animated modes are capable of reading vertex normals (if the option is enabled manually in `SketchfabRipper.ini`), but these may be rotated incorrectly, hence the need to enable the option manually. Try changing the "enableFix" parameter in `tools\blender-292\_sfVertNormalsFix.py` if experiencing issues.

> Converted models are split into chunks:
>
> Sketchfab automatically splits large meshes into 65,536-vertex chunks, "in order to support all graphics cards". See: https://help.sketchfab.com/hc/en-us/articles/201766675-Improving-Viewer-Performance#performance-meshes

> ArtStation links not working:
>
> ArtStation projects are only downloaded if they contain an interactive 3D viewer (Sketchfab/Marmoset Viewer). Projects without these will NOT be downloaded, so make sure your link contains at least one of these before reporting an issue.

> Certain animations broken:
>
> This is a known issue with the public Blender scripts, not the tool. See the "Before reporting an issue..." section above.

> Textures missing from the downloaded files:
>
> The model likely uses vertex colours.

> Converted models have broken UVs:
>
> Try changing the conversion mode to "Rigged" from the options menu.

> Marmoset Viewer models not rigged:
>
> The script used to convert `.mview` files does not support bones or animations.

> Exported models have an unusually small file size, and do not contain a mesh:
>
> This is an issue with the Blender scripts, not the tool. Try changing some options (specifically the conversion mode), then retry the download.

> Model doesn't export properly, even after trying the fixes listed above:
>
> Try moving the tool to a path without spaces or special characters - if it still doesn't work, try changing some other options or use the old manual method to convert the model.

> Antivirus flagging one or more files in this archive as malicious:
>
> False positive. Either disable it or whitelist the tool's folder. ~~The tool is written in C# and can be decompiled using https://github.com/icsharpcode/ILSpy if you wish to examine the code.~~ Since v1.16.2 this is no longer possible, see the changelogs for more information. Instead, use a service such as https://www.virustotal.com/ to scan for malicious code.

> `The system could not find the file specified` / `Access is denied` errors:
>
> Try moving the tool to a different path, preferably one without spaces or special characters. If that fails, check that your antivirus isn't blocking any of the tool's files.

> `The application has failed to start because its side-by-side configuration is incorrect`:
>
> Install this: https://github.com/abbodi1406/vcredist/releases

> `System.ComponentModel.Win32Exception: The system cannot find the file specified` error when attempting to update:
>
> `Updater.exe` is flagged by some antivirus software as malicious because it automatically downloads and unpacks a `.zip` file from the URL that is passed to it by SketchfabRipper. Whitelist it in your antivirus or update the tool manually.

> `System.Net.WebException: Unable to connect to the remote server`:
>
> Your firewall, antivirus or proxy/VPN is blocking network access.

> Issues not listed here:
>
> Try moving the tool to a path without spaces or special characters (eg. `C:\SketchfabRipper`), and make sure the tool is whitelisted in your antivirus/firewall.

## Changelog: ##
### Version 1.18.0 ###
#### Beta 2: ####
- Added a "Prerequisites" section to the README. New users should read this before running the tool, and existing users should try installing the software listed there if experiencing issues.
- Added a warning about https://sketchfab-ripper.com/.
- Fixed an issue where certain unsupported URLs could crash the tool.
- Fixed an issue which caused `SketchfabRipperCmd.exe` to fail on all non-Sketchfab/ArtStation URLs.
- Improved exception handling.
- Minor UI updates.
- New plugins:
    - `DayinPlugin.dll`: Supports http://www.dayin.la/.
    - `PlayboxPlugin.dll`: Supports https://www.aplaybox.com/. Exports in `.glb` format, bones not included. If the tool appears to be frozen, it's an issue with aplaybox's servers - the same applies to most `WebClient` errors. Retrying the download should fix most issues.
    - `SketchupPlugin.dll`: Supports https://3dwarehouse.sketchup.com/. Downloads models in `.dae` format if available, otherwise Sketchup 2021 `.skp`.
    - `ThreedingPlugin.dll`: Supports https://www.threeding.com/ models with a 3D viewer.
    - `VRoidPlugin.dll`: Supports https://hub.vroid.com/. Can download and decrypt `.vrm` (`.glb`) files, but conversion is currently not possible due to missing glTF extensions. Some older models do not use these extensions, and can be opened in software such as Blender. However, VRoidHub seems to manipulate the model with vertex shaders or JavaScript code once loaded - geometry will appear broken when opened in Blender. Future updates _may_ fix this.
- Plugin-specific:
    - CGTrader:
        - Marmoset Viewer files should be detected again.
    - GameModels3D:
        - Retrieving metadata for locked models now requires a valid session cookie, preventing unregistered users from downloading them. Attempting to download locked models will display an error message.
    - HeroForge:
        - Updated the `.ckb` importer, most meshes should now import properly.
    - NicoVideo:
        - Disabled NicoVideo support until further notice, their viewer uses a new format which is currently not possible to decompress.
    - P3D.in:
        - Fixed an issue caused by models with special characters in their names.
    - Sketchfab:
        - Added support for shortened https://skfb.ly/ links.
        - `.binz` files are now decrypted using a new tool (`binzDecrypt.exe`). Greatly reduces conversion times, and should fix most issues where the tool hung on "Dumping .binz files...".
        - Fixed a Python indentation error which broke Animated mode.
- Removed Chrome, nginx and binzDumper from the `tools` directory. Reduces the size of each update by approximately 50%.
- Replaced `extract_model.exe`, `extract_mview.exe` and `ExtractMarmosetTextures.exe` with `mviewExtractor.exe`.
- Temporarily removed Telegram integration until some issues are fixed.
- Updated the MEGA link for old versions in `README.md`.

#### Beta 1: ####
- Added support for https://p3d.in/, https://www.cgtrader.com/ & https://www.turbosquid.com/ (Marmoset Viewer embeds), https://heroforge.com/, https://anvl.co/, https://connect.clo-set.com/, https://3d.nicovideo.jp/, https://rigmodels.com/ and most models from https://gamemodels3d.com/.
- Added experimental Telegram integration as an alternative to the ZippyShare uploader.
- All JSON files are now properly formatted before being written to the `downloads` folder.
- Fixed an issue where Sketchfab background and environment data would always be downloaded, regardless of what the "Remove" option was set to. Applies only to non-encrypted (`.bin.gz`) models.
- Fixed an issue where error messages would be shown during the dumping phase, even when "Silent mode" was enabled.
- Improved regex matching for certain URLs.
- Introduced a new plugin-based system - site-specific code has been moved to separate plugins. Plugins are stored in the `plugins` folder and can be added or removed if necessary. Writing custom plugins is possible, the https://p3d.in/ plugin's source code is included for reference.
- Links imported using the "Import links" function are now queued normally, rather than being handled separately. This enables batch downloading of Sketchfab artists/collections, and fixes a number of other issues.
- Minor UI improvements.
- Rewrote and optimised large portions of the tool's code.
- Rewrote and updated the FAQ.
- The "Convert to quads" option should now work properly.
- The "Import model(s)" feature has been deprecated and will no longer work with the new plugin system. If you need this feature, download v1.17.3 or earlier from the link in `README.md`.
- Updated the Sketchfab addon for Blender, the "Enable IndexError fix" option is no longer necessary.
- Updated the message shown on the tool's first launch.
- Updated the offline Sketchfab viewer from v11.22.0 to v11.49.0.
- Various optimisations.

### Version 1.17.3 ###
- Added a `legacyMode` option which can be enabled manually in SketchfabRipper.ini - this option reverts some changes made in v1.17.2 and should only be enabled if experiencing issues where the tool hangs on "Importing/Exporting model...".
- Fixed an issue where vertex normals would not be applied correctly to certain models.
- Fixed various issues caused by Sketchfab API changes. Previous versions will no longer work for models using the new `.binz` format.
- The "Port 90 is in use" error should no longer appear if `nginx` is already running.
- Viewer data is now stored in memory - this should fix any issues related to `viewer_info.json`.
- When `binzDumper` crashes, the tool will attempt to recover any dumped files - if successful, the tool will continue normally.

### Version 1.17.2 ###
- Added basic error logging (only available in `SketchfabRipper.exe`) - output and errors thrown by the tool will be written to a new `logs` folder which is cleared on each launch. These files should be compressed and uploaded when reporting an issue.
- Fixed an issue where `binzDumper.exe` would crash if the decrypted data was already present in the model's folder.
- Greatly improved conversion times in Static/Rigged modes by exporting a `.blend` file from Blender 2.49 which is imported directly to Blender 2.92 - converting between ASCII and binary FBX formats is no longer necessary.
- Removed "FBX (ASCII)" from the list of available output formats.
- Removed some old code from `binzDumper.exe` which would cause it to crash when failing to contact Pastebin.
- Renamed the "FBX (Binary)" option to "FBX".
- Updated some error messages.

### Version 1.17.1 ###
- Decrypting `.binz` files is now possible without connecting to `sketchfab.com`. `nginx` is used to host the viewer data on port 90, and the HTML is generated by `binzDumper.exe`. If port 90 is unavailable, decryption will fail. An option to change the port will be available in a future version.
- Fixed an issue caused by the filenames in `file.osgjs`, where rigged and animated models using the new `.binz` format would not be converted properly.
- Fixed an issue where cancelling would not work while dumping `.binz` files. 
- Fixed an issue where `SketchfabRipperCmd.exe` could leave empty folders behind in the `downloads` directory.
- Fixed an issue where the progress bar would not reset when using "Import model(s)".
- Installing a new root certificate is no longer necessary to decrypt `.binz` files.

### Version 1.17.0 ###
- Added experimental support for models using Sketchfab's new encrypted `.binz` format. Note that the current decryption method is unstable, and may fail if Sketchfab makes major changes to their viewer scripts. Fixed versions may not be available for some time - see `tools\binzDumper\README.md` for more information.
- Fixed an issue in Rigged/Animated modes where the progress bar could reach 100% before conversion was complete.
- Fixed an issue where cancelling would not work while animations were being applied.
- Fixed an issue where downloaded textures would be deleted when using the third "Send to start pose" option.
- Fixed multiple issues which prevented materials from being applied to certain models.
- When downloading a model using the new `.binz` format, you may be asked to install a new root certificate. This is normal and necessary for the Titanium proxy to decrypt Sketchfab traffic - clicking "No" will cause `.binz` decryption to fail.

### Version 1.16.3 ###
- Added a "Convert to quads" option which automatically converts triangles in downloaded models to quads. This is based on Blender's built-in "Tris to Quads" feature, and will <u>not</u> restore the original topology. May increase conversion times, especially for high-poly models.
- Detailed conversion progress is now shown next to the Download button. Less accurate in Rigged or Animated modes due to issues with the Blender scripts. ArtStation models not yet supported.
- Fixed an issue where the "Sort by artist" option could leave empty folders behind in the `downloads` directory.
- Fixed an issue which prevented the tool from launching on Windows 7 systems.
- Improved error detection, the tool now reads Blender's output rather than  relying on the size of the converted model.
- Removed the "Enable IndexError fix" option.
- Removed the "Verbose mode" option - most console windows now appear blank due to the new updates, rendering this option useless.
- Renamed the "Apply materials" option to "Additional processing".

### Version 1.16.2 ###
- 7-Zip is now included in the `tools` folder, installing it is no longer required to compress downloaded files.
- Added a "Silent mode" option which hides any prompts requiring user interaction. Useful for batch downloads.
- Fixed an issue where downloading models could throw a `Could not create SSL/TLS secure channel` error.
- Merged the FAQ with a new README file, which also contains changelogs and additional information.
- Obfuscated portions of the tool's code and added some integrity checks to help prevent future versions from being modified and sold online. May increase loading times and raise the number of false positives.
- Removed obsolete parameters from `SketchfabRipper.ini`.
- Removed unused code from `SketchfabRipperCmd.exe`.
- Thumbnails now share the same name as their parent folders.
- Updated the FAQ.

### Version 1.16.1 ###
- Added a Discord link (based on the Zenhax post) to the FAQ since it's easier to find.
- Added a link to an archive of old and current versions to the FAQ.
- Failing to contact Pastebin for update data should no longer crash the tool.
- Fixed a rare crash which could occur when opening the options window.
- Moved the Blender addon to a new folder and added a version number to the `.zip` file.
- Removed some of the prompts which appear on new installations.
- Updated the JSON library, fixing a rare crash related to ArtStation models.

### Version 1.16.0 ###
- Added a dynamic invite link (based on the Zenhax post) to the tool's About screen - since the tool is now being spread online, it should help others find the server if they need support.
- Added an experimental command-line version of the ripper (`SketchfabRipperCmd.exe`), useful for automation or integrating with other tools.
- Added support for models with multiple UV channels (currently only available in Static mode). This should also fix any UV issues that were previously present in Static mode.
- Forced the use of the Aero2 theme, this should fix some UI issues on Windows 7 systems.
- Included an experimental Blender addon for downloading, converting and importing models directly within Blender.
- Minor UI fixes and performance improvements.
- Removed much of the old error logging code.
- Update checks are now performed asynchronously, fixing a short lag spike which would occur when clicking "Check for updates".
- Updated the FAQ.
- Various material improvements, mainly affecting `.blend` files:
    * Bump maps now use cubic interpolation, reducing visual artefacts.
    * Certain types of textures are now multiplied by a "factor" value in the Sketchfab data.
    * Fixes for normal maps with a flipped Y channel are no longer applied unless the "EnableExtraFeatures" parameter is set to "True" in `tools\blender-292\_sfTex.py`, fixing an issue with exported FBX files.
    * Textures mapped to different UV channels are now properly applied.

### Version 1.15.3 ###
- Added support for vertex normals stored in a `Float32Array`.
- Fixed an issue related to models on different drives when using the "Import Model(s)" feature.
- Fixed an issue where some materials would not apply correctly.
- Removed some integrity checks which would fail on new installations now that `DumpModelResources.exe` is no longer included.
- Removed some unused code which ran on each launch, startup times should be greatly improved.
- Removed `Utils.dll` and merged its code with `SketchfabRipper.exe`.
- Thumbnails shown in the model preview are now anti-aliased.
- Updated the FAQ.
- Vertex normal fixes from v1.15.2 can now be applied when using the Rigged and Animated conversion modes. This must be enabled manually.

### Version 1.15.2 ###
- ArtStation models are now downloaded using the internal dumping code, rendering `DumpModelResources.exe` obsolete. Updating existing models will be possible using the "Import model(s)" option in a future release.
- Blender scripts are now written to a single file regardless of conversion mode.
- Fixed an issue caused by some leftover code where the tool could throw an error while downloading a model.
- Improved the Sketchfab conversion scripts (currently only affects Static mode, other modes will benefit from these changes in a future release):
    * Reformatted and optimised the script.
    * Vertex normals are now read from the Sketchfab data instead of being calculated by Blender. This fixes several long-standing, normal-related issues such as seams or patches of incorrectly shaded geometry appearing on some models.
- Updated the FAQ and some old version strings.

### Version 1.15.1.1 ###
- Fixed an issue with the queueing system where the tool could get stuck in an infinite loop.
- Fixed thumbnails not downloading.
- Used a different method to download textures, since the WebClient functions could hang on certain files.

### Version 1.15.1 ###
- Added experimental queueing support, allowing additional links to be queued while downloading.
- Fixed an issue where the tool would continue to display "Processing..." when an invalid URL was entered.
- Parsing URLs is now done asynchronously.
- Removed some unnecessary code which was called on each download, reducing performance.
- URLs are now properly validated, entering an invalid or unsupported URL will display an error message.

### Version 1.15.0.1 ###
- Fixed an issue where the "textures" folder would remain empty when reusing a previously downloaded link.

### Version 1.15.0 ###
- Cancelling the current download queue is now possible.
- Downloads are automatically cancelled when closing the tool.
- Improved UI responsiveness.
- Removed the prompt which appeared when attempting to sign in while an access token was already present - selecting "No" would crash the tool.
- Rewrote portions of the tool's code to run asynchronously.
- The code from `DumpModelResources.exe` has been merged with `SketchfabRipper.exe`, allowing detailed output to be displayed without needing an additional window. `DumpModelResources.exe` will likely be removed in a future version.
- The tool's window can now be minimised and moved while downloading.

### Version 1.14.0 ###
- Attempted to improve performance when starting the tool for the first time.
- Fixed an issue where models with special characters in their name could download to incorrectly named folders.
Fixed a minor UI issue which was only visible when testing using a different PC or VM.
- Logging in using a Sketchfab account is now possible, this will allow original files to be downloaded if a model is free or owned by the given account. Two methods are available - email/password or session ID. Login details are never saved.
- Made the minimise button visible. Note that both the button and the rest of the UI will not work while downloading a model due to how the tool's code is written.
- Parameters are now automatically stripped from URLs.
- Updated the FAQ.

### Version 1.13.3 ###
- Fixed an issue where models would not be converted.
- Fixed an issue where some FBX files would have missing textures.

### Version 1.13.2 ###
- Fixed an issue caused by the stripped `.zip` metadata, where Blender would throw an `OverflowError: modification time overflows a 4 byte field` error during conversion.
- Moved and added some shared functions to a new library, `Utils.dll`.
- Tested the tool in a clean Windows 10 VM, revealing several new issues which have now been fixed.

### Version 1.13.1 ###
- Added support for vertex colours stored in a `Float32Array`.
- `Application.DoEvents()` is no longer used to update the UI, hopefully fixing a long-standing issue where the tool could hang on "Converting model..."
- Clicking the "Download" button is no longer necessary, pressing Enter after pasting a link should now work as well.
- Fixed an issue where low-resolution textures would be downloaded if they had a larger file size than their high-resolution counterparts. Mainly affected simple textures, such as pixel art.
- Fixed an issue where non-RGBA vertex colours would not apply correctly.
- Replaced the "Delete unnecessary files" option with a menu allowing the user to select which types of files are downloaded and kept after conversion.
- Rewrote some error messages and included possible solutions.
- Updated various tooltips to reflect the changes made in the last few versions.

### Version 1.13.0 ###
- Added an "EnableExtraFeatures" parameter to `tools\blender-292\_sfTex.py`, set it to "True" to enable extra .blend material features at the cost of breaking FBX textures.
- Added experimental vertex colour support. "Apply materials" must be enabled.
- Fixed an issue where `osg.Geometry` objects without an `osg.StateSet` property would break the texturing process.
- Updated the FAQ.

### Version 1.12.2.1 ###
- Reverted an unstable scaling change which could break some models.

### Version 1.12.2 ###
- Added an option to export as glTF, preserving most PBR materials which FBX doesn't support while being more compatible than `.blend` files. Animated models are not yet supported.
- Added support for downloading Sketchfab collections.
- Added support for downloading models liked by a Sketchfab user (URLs must end with "/likes").
- Enabled the "Save .blend" option by default on new installations, as the .blend materials are far superior than the FBX versions.
- Fixed a number of material-related issues:
    * Added support for materials using the albedo alpha.
    * Added support for ambient occlusion maps in `.blend` files. Disabled by default since it breaks FBX textures. Uncomment lines 105-116 in `tools\blender-292\_sfTex.py` to enable.
    * Automatically set the alpha blending method, some materials should no longer appear dithered.
    * Emissive values are now properly parsed.
- Fixed a rare conversion issue likely caused by malformed `.osgjs` files.
- Fixed some minor UI issues caused by the options renamed in v1.12.1.
- Internet shortcuts are now created in each model's folder (though not included in packaged files, and ArtStation models are not yet supported).
- Removed more invalid Discord invites from various scripts.
- Removed some testing code left over from v1.12.0.
- Reverted some internal UI changes which were causing issues.

### Version 1.12.1 ###
- Added a tooltip to the URL input field which lists the types of supported links.
- Fixed an issue where Python would fail to sort the list of objects numerically, causing models with 1000+ parts to break the automatic texturing process.
- `materialInfo.txt` and `thumbnail.jpeg` are no longer included in packaged files. Thumbnails will still be available in the `_packaged` folder, but will no longer be added to the `.zip` file.
- Removed any references to Discord invites which are now invalid.
- Renamed the "Apply textures" option to "Apply materials".
- Renamed the "Show progress" option to "Verbose mode".
- Tooltips no longer fade after 5 seconds.
- Updated the FAQ.

### Version 1.12.0 ###
- Added a third state to the "Send to start pose" option, allowing two versions of each model to be saved. Not yet compatible with .blend files.
- Blender 2.49 (used to convert Sketchfab models) no longer relies on the PythonPath variable being set, all necessary modules are now included in `python26.zip`.
- Completely rewrote the `.osgjs` parser to increase accuracy and parse the `.osgjs` file properly rather than rely on unstable methods.
- `DumpModelResources.exe` is now able to generate `materialInfo.txt` from an existing model if `file.osgjs`, `model_info.json` and optionally `texture_info.json` are present in the model's folder.
- Enabled the "Apply textures" option by default on new installations, it's now stable enough for regular use.
- Fixed an issue related to duplicate texture detection.
- Fixed an issue where clear-coat normals would cause visual artefacts since they weren't being passed through a Normal Map node in Blender.
- Fixed an issue where geometry using "Lines" mode would be included in `materialInfo.txt` and cause errors during the automatic texturing process.
- Minor UI changes in the About tab.
- Retargeted the tool to .NET 4.8.
- The FAQ now includes solutions for known issues such as broken UVs.
- Updated some error messages.
- Updated some tooltips in the options menu.

### Version 1.11.7 ###
- Fixed an issue where non-existent materials could appear in `materialInfo.txt` and break the automatic texturing process. This fix is experimental, and may break models which worked in earlier versions.
- Fixed an issue with duplicate texture detection.

### Version 1.11.6 ###
- Fixed a minor issue introduced in v1.11.5 where normal maps would not be applied during the automatic texturing phase.

### Version 1.11.5 ###
- Added the Monero address to the About tab and replaced the plaintext addresses with clickable links that copy each address to the clipboard.
- Fixed an issue caused by the Sketchfab API change workaround in v1.10.1, where textures found in `model_info.json` would not be included in the duplicate removal process.
- Fixed an issue which broke the "Apply textures" option when "Rigged" mode was enabled.
- Reduced the download size by around 100 MB by stripping the included Blender builds of unnecessary files not required to run the conversion scripts.
- Rewrote the mesh renaming code so it no longer relies on a specific format.
- The "Apply textures" option now supports OBJ files.
- The `mesh*.dat` files extracted from Marmoset Viewer models are now automatically converted to FBX since some software would fail to import the OBJ files.

### Version 1.11.4 ###
- Added tooltips to many of the newer settings which lack an explanation in the Options menu.
- Fixed another `.osgjs` parser issue related to duplicate material names.
- Removed `GenerateErrorReport.exe` from new installations until the error logging in `SketchfabRipper.exe` is updated.
- Updated the FAQ to include an alternative cryptocurrency (Monero) address.

### Version 1.11.3 ###
- Fixed an issue related to the new mesh renaming mode.
- Fixed an issue where the updater would display longer version numbers incorrectly.
- Improved `.osgjs` parsing, more models should work now.

### Version 1.11.2 ###
- Duplicate mesh names are now renamed by appending a number, fixing an issue where models with too many meshes which shared the same name would break the material parser.
- Reduced the time it takes to apply textures to models by several minutes.
- Fixed an issue where meshes with long names would cause the material parser to throw an error.
- Fixed an issue where Sketchfab models with quotes in their names would not display correctly in the preview.
- Fixed an issue which could occur if the "Albedo" value was set in the material's options, but a texture was present in either the "Diffuse" or "Diffuse colour" values.
- The "factor" value in `model_info.json` is now used when parsing materials, this fixes some cases where materials which rely entirely on the value would not display correctly.

### Version 1.11.1 ###
- Fixed a minor UI issue in the options window, where the "Delete unnecessary files" option would be greyed out unless "Enable IndexError fix" was enabled.
- Fixed an issue where textures with special characters in their filename would cause the material parser to throw an error.
- Improved and fixed some issues related to automatic material creation.
    * Clear-coat and transparent materials are now created properly.
    * Transparent materials use the "Alpha Hashed" blending method since it was the most compatible option. Unfortunately, this makes solid transparent surfaces (such as glass) appear dithered. To fix this, simply change the blending method to "Alpha Blend".
- Materials using single or RGB values instead of textures are now parsed.
- Normal map Y channels are now flipped when necessary.
- PBR textures are now imported into Blender using linear colour space, previously some surfaces could appear too glossy/metallic.
- Rewrote the `.osgjs` parser to increase stability, the automatic texturing option should now work with most models.

### Version 1.11.0 ###
- Added an experimental option to automatically apply textures to ripped models (only the "FBX (Binary)" output format is supported, optionally with "Save .blend" enabled).
- Added an option to manually enable the `IndexError: list index out of range` fix, since rigged/animated models have a larger filesize which breaks the auto-detection feature. Note that keeping this enabled will break models which don't need fixing, so enable it only when necessary.
- Meshes and materials are now renamed to their original names when the "Apply textures" option is enabled.
- Fixed an issue where meshes without a name and/or material would cause the material parser to throw an error.
- The addition of the "Apply textures" option has increased the filesize of the ripper by around 200 MB since Blender 2.92 now has to be included.
- Updated the FAQ.

### Version 1.10.1 ###
- Fixed an issue caused by Sketchfab API changes where some textures would not be downloaded.

### Version 1.10.0 ###
- Added experimental Sketchfab material parsing. The information is written to `materialInfo.txt` in each model's folder. Textures are not automatically applied.
- Fixed an issue where versions such as "1.10" would be displayed as "1.1.0" in the update window.

### Version 1.9.2 ###
- Added a Bitcoin address to the About screen and FAQ for those who want to support the tool's development by donating. Donating is entirely optional, the tool will remain free and features will not be limited or locked for those who don't.
- A warning message is now shown when the tool detects an `.osgjs` file larger than 5 MB. Such files often take a long time to parse, larger files can sometimes take hours or even days, so the user is now given an option to skip that model. It can then be converted at a later date using the "Import model(s)" function.
- Fixed an issue introduced in v1.8.2 by the `IndexError: list index out of range` fix where the tool would look for an FBX file even when the output format was set to OBJ, and a `System.IO.FileNotFoundException` would be thrown.
- Improved some error messages.
- Process exit codes are now used to determine when a process crashes or is manually terminated. Rather than continue with missing or corrupted files, the tool now skips conversion.

### Version 1.9.1 ###
- Packaged files are now split into 500 MB parts to enable larger ZippyShare uploads.

### Version 1.9.0 ###
- Added an option to automatically upload packaged files to ZippyShare. Links are saved to `zippyshareLinks.txt`.
- AR data is now downloaded for compatible Sketchfab models, this includes USDZ (iOS) and GLTF (Android) files. Software such as Blender natively supports GLTF. Unlike the files produced by the automated Blender conversion scripts, the AR data contains original, unaltered mesh/bone data and vertex/material colours. Note that very few Sketchfab models support this feature, and during testing I was only able to find a single model which made use of it.
- Modified some error messages.
- Rather than download files and remove them later, the "Delete unnecessary files" option now skips these files, allowing for faster downloads.
- Thumbnails are no longer deleted when the "Delete unnecessary files" option is enabled.

### Version 1.8.3 ###
- Fixed an issue where the Sketchfab API could return incorrect search results and the tool would download from the wrong artist.

### Version 1.8.2 ###
- Improved duplicate texture detection. Textures are now hashed and compared against two lists - if both lists contain a match, the file is deleted.
- The `IndexError: list index out of range` issue which prevented certain Sketchfab models from converting properly and generated empty model files has been fixed. Most, if not all Sketchfab models should now convert without issues.
- The main Blender scripts are now generated and written at runtime to reduce clutter in the "tools" folder, and to allow for easier configuration.

### Version 1.8.1 ###
- Added an alternative Marmoset Viewer texture extractor, which should be more stable than the old Python-based tool.
- Added an option to change how filename conflicts are handled.
- Fixed an issue where the "Import model(s)" function would fail to convert models which had been downloaded using the "Animated" conversion mode.
- Fixed an issue where the latest version's release notes would not be shown in the redesigned update window.

### Version 1.8.0 ###
- Added an additional step to Marmoset Viewer conversion which converts the `.dat` files in each model's folder to OBJ. These can be used when the FBX file is corrupted, but will need smooth shading applied.
- Added an option to disable sending models to their start pose. This fixes some bone-related issues where parts of models would be rotated incorrectly. Disabling this is only recommended when necessary, since issues may arise with other models.
- Added an option to sort packaged models by artist.
- Added support for Sketchfab/ArtStation embed links.
- ArtStation thumbnails are now downloaded, and copied to the `_packaged` folder if the Auto-package option is enabled.
- Fixed an issue caused by ArtStation projects with multiple Marmoset Viewer files, where the `.mview` files would be overwritten if they shared the same name. These files now have a number appended to their name.
- Fixed an issue introduced in 1.7.5 where the `textures` folder would not be deleted before redownloading an existing model, and duplicate files would be created.
- Fixed an issue where the Auto-package option would not delete existing `.zip` files before compressing, and would add files to the existing archive instead of creating a new one.
- Fixed an issue where the tool would hang when an invalid Sketchfab artist URL was entered.
- Redesigned the update window to match the rest of the tool's UI.
- The Auto-package option now copies the model's thumbnail to the `_packaged` folder along with the `.zip` file, making it easier to find specific models without needing to extract each archive.
- The update window now shows all changes between the current and latest version.
- To help avoid confusion, ASCII FBX files are now automatically deleted when FBX (Binary) is selected as the output format, and the `*.binary.fbx` files are renamed to `*.fbx`.
- Updated the "Delete unnecessary files" option, it now removes everything but the model files and `textures` folder.
- Updated the FAQ.
- Updated the options window to prevent selecting incompatible conversion mode/output format combinations, such as "Animated" and "OBJ".

### Version 1.7.5 ###
- Attempted to reduce the number of false positives caused by Updater.exe and other programs used by the tool.
- Fixed an issue where `DumpModelResources.exe` would skip textures which had the same filename but different contents. Such files now have a number appended to the filename.
- Fixed an issue where the auto-update function would show that there was an update available even if the latest version was installed.
- Updated the FAQ.

### Version 1.7.4 ###
- Fixed an issue where the tool would fail to download models containing special characters in their title (such as quotation marks).

### Version 1.7.3 ###
- FBX materials are no longer assigned random colours.
- Fixed an issue where ArtStation models would be converted regardless of the "Enable conversion" option.
- Fixed some issues caused by the recent changes in `tools\DumpModelResources.exe`.
- Fixed a minor UI issue in the options window.

### Version 1.7.2 ###
- Added an "About" tab in the options window.
- Fixed an issue where Marmoset Viewer textures were not exporting properly.
- Fixed an issue which broke Sketchfab artist downloads.
- `tools\DumpModelResources.exe` can now be run as a standalone application.

### Version 1.7.1 ###
- Added an option to import and reconvert existing Sketchfab/ArtStation models.
- Fixed the OBJ output option.

### Version 1.7.0 ###
- Added the ability to download environment data from Sketchfab models.
- Fixed an issue where restricted Sketchfab models would not download in artist mode.
- Rewrote large portions of the tool's code to improve stability.

### Version 1.6.2 ###
- Fixed an issue which broke Sketchfab artist downloading.

### Version 1.6.1 ###
- Added a new output format, "FBX (Binary)".
- Added support for ArtStation links containing Sketchfab embeds.
- Fixed an issue where some ArtStation models would take a long time to export by redirecting console output to `log-noesis.txt`.
- Fixed the Auto-package option and added batch modes for ArtStation links.

### Version 1.6.0 ###
- Added experimental ArtStation support. Animations and rigs not supported.

### Version 1.5.1 ###
- Added the ability to download scene sounds.
- Automatically fall back to Rigged mode if animations are not present.
- Updated the FAQ.

### Version 1.5.0 ###
- Added experimental animation support.
- Updated the FAQ.

### Version 1.4.4 ###
- Added support for links using the `sketchfab.com/models` format.
- Fixed an issue where the model thumbnail would turn blank when reusing the same link.
- Fixed a rare issue which occurred while decompressing `file.osgjs.gz`.
- Fixed some issues related to links which only contain the model's ID.

### Version 1.4.3 ###
- Added an option to pin the window on top.

### Version 1.4.2 ###
- Added an option to remove unnecessary `.bin` and `.osgjs` files after conversion.

### Version 1.4.1 ###
- Fixed an issue related to missing `.bin.gz` files which affected some models.

### Version 1.4.0 ###
- Added an experimental auto-update feature.
- Environment tests are now only run on the first launch or whenever new tests are added.

### Version 1.3.4 ###
- Automatically run some environment tests on startup to detect common issues.
- Disabled the UI while parsing and downloading models.
- Various UI updates to make the tool feel more responsive.

### Version 1.3.3 ###
- Added an option to skip all existing models in the current queue.
- Fixed an issue in v1.3.2 which broke artist downloading.
- Fixed an issue where models with names consisting entirely of special characters would fail to download in artist mode.

### Version 1.3.2 ###
- Added an option to retry failed model downloads.
- Model JSON data is now properly formatted.
- Updated some logging code.

### Version 1.3.1 ###
- Added a one-time startup notice.
- Disabled rigging by default for new users.
- Fixed an issue related to `.gz` decompression.
- Fixed an issue that caused artist pages to download twice.
- Fixed a number of issues related to the new model dumper.
- Updated the FAQ.

### Version 1.3.0 ###
- Added `GenerateErrorReport.exe` - generates `logs.zip`, which can assist in resolving issues.
- Fixed an issue caused by the Sketchfab API returning invalid texture sizes.
- Fixed an issue that prevented models without a name in the URL from downloading.
- Removed `dump_sketchfab_model.exe` and `dump_sketchfab_model_unique.exe`, replaced with a self-made tool.
- Renamed `README.txt` to `FAQ.txt`.
- Updated the FAQ.

### Version 1.2.0 ###
- Added an option to save the model as a .blend file.
- Added an option to append a unique ID to folder names, to avoid filename conflicts.
- Fixed special Unicode characters not displaying properly in the model preview.

### Version 1.1.0 ###
- Fixed an issue that would prevent some models from converting.
- Added `README.txt` and a log file generator.
- Minor bugfixes.

### Version 1.0.0 ###
- Initial release.
