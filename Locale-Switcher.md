---
layout: page
title: Locale Switcher 
subtitle: for Safari
---

Locale Switcher helps you to easily switch between website's versions of different languages.

For details please refer to [Mac App Store](https://apps.apple.com/app/locale-switcher/id1501719622?mt=12).

Or you can drag this bookmarklet <a href="javascript:(function(){ let pairs=[['en-us', 'zh-cn'], ['en-US', 'zh-CN']]; pairs.forEach(pair => pair.forEach((locale, id) => {if (location.href.includes(locale)) {location.href = location.href.replace(locale, pair[1-id])} }))})()">Locale Switcher</a> to your bookmark bar. It offers the simplest function of switching between `zh-CN` and `en-US`.
