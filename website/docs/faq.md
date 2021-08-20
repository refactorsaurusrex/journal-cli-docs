---
id: faq
title: FAQ
sidebar_position: 5
---

## Why PowerShell?

Although PowerShell seems to be popular mostly as a punching bag among some developers, it's actually a cool language that has come a long way in the last several years. It can be extremely concise for command line usage, very verbose for scripting purposes, it runs everywhere, has nice built-in functionality for things like progress bars and tabular output, and has lots of other niceties that I can't even think of off the top of my head. But the _main_ reasons I like PowerShell for command line tools are twofold. First, it allows me to write applications using my preferred language, C#. Second, it allows me to publish *once* and distribute everywhere. Once a module has been published to the PowerShell Gallery, installation is _exactly_ the same on every platform. Bottom line: I know PowerShell, I like it, and it does what I need it to do. 

## How can I find all untagged entries?

Like this:

```powershell
Get-JournalEntries | ? {$_.Tags.Count -eq 0}
```

## How can I delete journal entries?

You can always manually delete entries in the same way that you'd delete any other file on your computer. However, if you'd like to delete them with PowerShell, you should use the `Get-JournalFiles` command to select the entries you want to delete, then pipe those items to the `Remove-Item` function. Here's an example:

```powershell
# Deletes entries from yesterday a
Get-JournalFiles -From yesterday -To today | Remove-Item
```

