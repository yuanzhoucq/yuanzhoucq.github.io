---
title: 为什么我在 Tab Space 存储的标签页消失了？
tags: [Tab Space]
---



---

**如果您刚刚发现 Tab Space 保存的所有标签页都消失了，这很可能是 Tab Space 刚刚进行了一次更新，您只需要等待几秒钟，数据就会自动恢复。如果无法恢复，请通过“访达->前往->前往文件夹”进入“~/Library/Containers/cn.joyuer.Tab-Works.ext/Data/Library/Preferences”，打开“cn.joyuer.Tab-Works.ext.plist”文件，将其中Bookmarks的值保存命名为 file.tabspace 文件，然后可以将其重新导入 Tab Space。**

如果仍然无法恢复，请继续往下阅读。

---



亲爱的 Tab Space 的用户,

您好！如果您最近在升级 Tab Space 2.3.2 版本前升级了 Safari 13，您可能发现您之前保存的标签页意外消失了。非常抱歉，以下是关于数据丢失的一点说明。

## 为什么数据会丢失？

最初，Tab Space 把用户数据存储在浏览器内一个名为 `locaStorage` 的地方，它位于 `safari-extension://{tab-space-bundle-id}` 这个域之下。这个存储只能被用户在浏览器中访问。然而，Safari 13 更改了扩展 App 拥有的存储域，它现在变成了 `safari-extension://{some-random-id}`。 因此，Tab Space 在 Safari 13 中不再能访问到原先的存储域，数据在我们看来也就丢失了。

当我在一位用户的帮助下发现这一问题的时候，我重新设计了 Tab Space 的存储机制，把存储位置从 `localStorage` 转移到 Tab Space 程序内部。 这样它就可以不再受 Safari 浏览器变动的影响。随后，我把这一新版本 (2.3.2) 提交到 Mac App Store。正常来讲，24 小时内就会通过审核，然后用户自动更新，没有人会丢失数据，皆大欢喜。然而可惜的是，可能由于最近 macOS 将要升级到 10.15 版本，提交新版本的程序较多，Tab Space 新版本的审核花去了将近一星期的时间。这期间，很多用户的 Mac 已经自动升级了 Safari 13，数据也就丢失了。

## 失去的标签页可以恢复吗？

非常抱歉，由于上述原因，没有办法恢复遗失的数据。 `Safari-extension://{tab-space-bundle-id}` 在 Safari 13 中已经不可被访问到了。非常抱歉，由于在一开始设计程序的时候没有充分考虑到浏览器升级带来的影响，为您带来了麻烦。

## 这种情况还会发生吗？

现在您的数据已经被存储到 Tab Space 程序本身之中了，它将不再受到浏览器本身改动的影响。

再次说明，非常抱歉为您的使用带来了麻烦，感谢您的支持和信任。
