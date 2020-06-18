---
author: "Me"
date: 2020-06-09
title: "How to completely disable history in Chrome/Chromium"
best: false
---

You need system admin access.

1. Access Windows registry editor with regedit.exe

2. Go to HKLM\SOFTWARE\Policies\Google\Chrome

3. Add this element: SavingBrowserHistoryDisabled - DWORD - 1

4. Done!

![image](/img/cromi1.JPG)

This is the policy we manage:

![image](/img/cromi2.JPG)



