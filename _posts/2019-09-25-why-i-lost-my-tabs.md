---
title: Why I lost my tabs in Tab Space?
tags: [Tab Space]
---



---

Updated 04/18/2020:

**If you noticed that all your saved sessions disappeared, that is mostly because Tab Space had just upgraded. Just wait for a few minutes and refresh the page, your data will be restored automatically. If not, you can use Finder -> Go to -> Go to Folder -> "~/Library/Containers/cn.joyuer.Tab-Works.ext/Data/Library/SyncedPreferences", and open "cn.joyuer.Tab-Works.ext.plist”, copy the Value of Bookmarks (`[[...]]`), then save the content as a file named “file.tabspace”. Then you will be able to import it from Tab Space.**

---
Updated 09/25/2019:


Dear Tab Space users,

If you recently upgraded Safari 13 before upgrading Tab Space to version 2.3.2, you may found that your saved tabs disappeared. I am deeply sorry for this situation and here's why.

## Why would this happen?

Initially, Tab Space saves your data somewhere named `locaStorage` in Safari. It is under a domain of Tab Space application which is prefixed by `safari-extension://{tab-space-bundle-id}`. It is very private that only you can access it in Safari. However, Safari 13 changes the domain owned by its extensions, now it is prefixed by `safari-extension://{some-random-id}`. Thus, Tab Space will no longer be able to fetch these data back and display them to you.

When I found this problem with some help of a user, I changed the storage of Tab Space from `localStorage` to some container inside Tab Space. This would make your data better persist and be independent of Safari's change. I submitted this new version (2.3.2) to Mac App Store. Normally it will be approved by Apple within 24 hours. And then everyone gets an upgrade, nobody loses his data. Just perfect! However, maybe these days many developers submit their new versions to Apple since macOS is about to upgrade to version 10.15. It took me about one week to pass the App Store review for Tab Space. Unfortunately, many of you have upgraded to Safari 13. Your data are gone.

## Can I restore the tabs?

Sorry, I didn't find a way to restore them. `Safari-extension://{tab-space-bundle-id}` has become inaccessible since Safari 13. I am so sorry, that I didn't anticipate the influence of Safari's upgrade in the beginning, causing these trouble to you. 

## Will this happen again?

Now your data are stored inside Tab Space app, it will not be influenced by browser's change any more. So this will not happen again.

Again, I am deeply sorry for this situation and thanks for your support.
