---
sidebar_position: 2
title: Listing
---

# Listing, Indexing, and Searching

There are three different commands that list your journal entries. Let's look at them one by one.

## Get-JournalEntries

The `Get-JournalEntries` command, or `gje` for short, returns a list of your entries in chronological order. This can be in ascending or descending order and filtered by date ranges or by tags. You can show all your "readme" entries that have expired or even those which have not yet expired. You can also open an entry randomly selected from your entire journal, or from a collection of entries based on any of the filtering criteria mentioned above. Here are a few examples of this command. 

```powershell
# Returns the last 30 journal entries in descending order.
Get-JournalEntries

# Returns the last 30 journal entries tagged 
# 'running' OR 'shopping' in descending order.
Get-JournalEntries -Tags running,shopping

# Returns the last 30 journal entries tagged both
# 'running' AND 'shopping' in ascending order.
gje -Tags running,shopping -TagOperator All -Direction Ascending

# Returns up to 100 journal entries from the last year.
gje -Limit 100 -From "1 year ago"

# Returns 10 journal entries written between 1 year ago
# and 6 months ago.
gje -Limit 100 -From "1 year ago" -To "6 months ago"

# Returns up to 30 entries from January 1st 2020 
# to February 28th 2020.
gje -From "1/1/2020" -To "2/28/2020"

# Returns all expired readme entries
Get-JournalEntries -ShowReadMeEntries

# Returns all expired readmes written in the last year.
Get-JournalEntries -ShowReadMeEntries -From "1 year ago"

# Returns all expired and all future readme entries.
gje -ShowReadMeEntries -IncludeFutureReadMeEntries
```

You should be able to mix and match the available parameters to return the exact set of entries you want to review. 

:::tip Hot Tip!

As was mentioned in the [article on writing](/docs/basics/writing), you can use tab-completion to retrieve tag names that have previously been used in your journal. This is true of all tag parameters across journal-cli.

:::

## Get-JournalIndex

While `Get-JournalEntries` returns a list of individual entries, `Get-JournalIndex` - or `gji` - groups all your journal entries by tag. This command shares many parameters with `Get-JournalEntries`. Therefore, as you might expect, you can filter the results by one or more tags and/or by date range. The only parameter that's different is called `-ShowCollateralTags`. The easiest way to explain the utility of this parameter is with an example.

```powershell
# Returns an index of entries that contain BOTH 
# "running" and "work".
PS> Get-JournalIndex -Tags running,work -TagOperator All

Tag     Count Entries
---     ----- -------
running     1 {2021.06.29}
work        1 {2021.06.29}
```

The first thing you might notice is that the two results are for the same entry. That might be confusing at first, but it's by design. The command requested all entries that are tagged both "running" and "work" - and in this case there is only one such entry - but `Get-JournalIndex` is intended to break down the result set *by tag* and there are *two tags* here. Therefore, we correctly have *two results*, both of which point to the same entry. 

Let's see what happens when we add `-ShowCollateralTags`.

```powershell
PS> gji -Tags running,work -TagOperator All -ShowCollateralTags

Tag         Count Entries
---         ----- -------
photography     1 {2021.06.29}
gear            1 {2021.06.29}
journal-cli     1 {2021.06.29}
running         1 {2021.06.29}
work            1 {2021.06.29}
```

Now we have five results, all of which point back to the same journal entry. That's because that one entry contains all five of those tags. Here's the explanation: By default, when `-TagOperator` is set to `All`, the results will only reflect the tags *you specifically requested*. However, you may also be interested in seeing all the collateral tags included on the matched journal entries but which go beyond the specific tags requested.

## Get-JournalFiles

In contrast with `Get-JournalEntries` and `Get-JournalIndex`, both of which return custom objects, `Get-JournalFiles` returns native PowerShell objects representing the underlying journal entry files. The allows manipulation of journal files using native PowerShell commands such as `Select-String`, which enables full text searching, and `Remove-Item` which can be used to permanently delete unwanted journal entries from disk. 

`Get-JournalFiles` allows you to select files by tag, date range, or by entry names. Most of these parameters are the same as what's described above for `Get-JournalEntries` and `Get-JournalIndex`. The only exception is `-EntryNames`, which takes an array of journal entry file names in the format of `YYYY.MM.DD`. For example, `2021.06.29` references the journal entry file for June 29th, 2021. This is helpful any time you want to manipulate journal entries returned from either `Get-JournalEntries` or `Get-JournalIndex` using native PowerShell commands. As indicated above, the primary use cases here are performing full text search and entry deletion. 
