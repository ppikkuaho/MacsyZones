# Pietari's MacsyZones build

Fork of [rohanrhu/MacsyZones](https://github.com/rohanrhu/MacsyZones) (GPL-3.0), kept at github.com/ppikkuaho/MacsyZones for our own changes. Branch `pietari` = tag `v3.1.1` plus our commits (`git log v3.1.1..pietari`). The first: the app no longer downloads and installs updates when it starts (upstream has no off switch, issue #91). Remotes: `origin` is the fork, `upstream` is rohanrhu. No pull requests or comments upstream without Pietari's approval.

## Build and install

```
cd ~/Documents/macsyzones
xcodebuild -project MacsyZones.xcodeproj -scheme MacsyZones -configuration Release \
  -derivedDataPath /tmp/mz-build DEVELOPMENT_TEAM=YKHK786JZ3 CODE_SIGN_STYLE=Automatic \
  -allowProvisioningUpdates build
osascript -e 'quit app "MacsyZones"'
rm -rf /Applications/MacsyZones.app
ditto /tmp/mz-build/Build/Products/Release/MacsyZones.app /Applications/MacsyZones.app
open -a MacsyZones
```

The same signing team keeps the Accessibility grant across rebuilds. The "Check for Updates" button would still replace this build with upstream's, so do not use it.

## Settings

`~/Library/Application Support/MacsyZones/AppSettings.json`. Starting values (2026-11-05): snap key Control, modifier key None, and these off: shake to snap, snap with right click, layout switcher, Quick Snapper shortcut, window cycling shortcuts (upstream's Command+[ and Command+] would take over those keys in every app).

## Update deliberately

`git fetch upstream --tags`, `git rebase --onto <new-tag> v3.1.1 pietari`, build and install as above, update this file, `git push --force-with-lease origin pietari`.
