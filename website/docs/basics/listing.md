---
sidebar_position: 2
title: Listing
---

# Listing Entries

There are three different ways to list your journal entries. Let's look at them one by one.

## By Entries

The `Get-JournalEntries` command - or `gje` for short - returns your entries in chronological order. This can be in ascending or descending order and filtered by date ranges or by tags. You can show all your "readme" entries that have expired or even those which have not yet expired. You can also open an entry randomly selected from your entire journal, or based on any of the filtering criteria already mentioned. Here are a few examples. 

```powershell
# Returns the last 30 journal entries in descending order.
Get-JournalEntries

# Returns the last 30 journal entries tagged 
# 'running' OR 'shopping' in descending order.
Get-JournalEntries -Tags running,shopping

# Returns the last 30 journal entries tagged both
# 'running' AND 'shopping' in ascending order.
gje -Tags running,shopping -TagOperator All -Direction Ascending

# Returns the last 100 journal entries from the last year.
gje -Limit 100 -From "1 year ago"

# Returns 10 journal entries written between 1 year ago
# and 6 months ago.
gje -Limit 100 -From "1 year ago" -To "6 months ago"

# Returns all expired readme entries
Get-JournalEntries -ShowReadMeEntries

# Returns all expired readmes written in the last year.
Get-JournalEntries -ShowReadMeEntries -From "1 year ago"

# Returns all expired and all future readme entries.
Get-JournalEntries -ShowReadMeEntries -IncludeFutureReadMeEntries
```

In short, you should be able to mix and match the available parameters to return the exact set of entries you want to review. As was mentioned in the article on [writing](/docs/basics/writing), you can use tab-completion to auto-populate tag names that have been used in your journal. This is true of all tag parameters across journal-cli.

## By Index

## By Files

