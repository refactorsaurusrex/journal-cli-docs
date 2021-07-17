---
sidebar_position: 1
title: Writing
---

# Writing Entries

:::tip Hot Tip!

You can generate a list of all journal-cli commands at any time by running `Get-Command -Module JournalCli`. Run `help {command}` to display documentation for a specific command. 

:::

## Using a text editor

### Tags

To create a new journal entry and edit it using your default markdown file editor, run `New-JournalEntry`. You can also use its built-in alias `nj`. Without any parameters, this will create a new, untagged entry for the current date. You can always add or remove tags later from the entry's yaml front matter, which looks like this:

```yaml
tags:
  - running
  - work
  - coding
```

To add tags directly from the command line, use the `-Tags` parameter, which accepts an array of string values. 

```powershell
# Examples of valid tag arguments.
New-JournalEntry -Tags running,work,coding
New-JournalEntry -Tags cooking
```

:::tip Hot Tip!

You can use "tab completion" to automatically populate tag names, based on the tags you've previously used in your journal. For example, if I type `-Tags run` followed by the tab key, "running" will be automatically suggested because I've previously used "running" as a tag. The wildcard characters `*` and `?` can be used as well, so typing `-Tags *ing` followed by the tab key would cycle through all previously used tags that end with the letters "ing" in alphabetical order, such as "running", "cycling", and "swimming".

:::

:::warning

When entries are created without any tags, they're assigned the `(untagged)` tag because all entries should have at least one tag. Entries with literally *zero* tags cannot be indexed. (More on indexing in [the next section](/docs/listing).)

:::

### Entry Date

By default, entries are created for the current date. If you want to create an entry for a different date, use the `-Date` parameter. This parameter accepts a wide variety of inputs from natural language statements such as "yesterday", "tomorrow", "last month", or "1 year ago". You can also use more standard date formats such as "7/3/2021" or "June 12, 2019". Just be sure to enclose your date value in quotes if it includes spaces. 

```powershell
# Examples.
New-JournalEntry -Date "7/3/2021"
New-JournalEntry -Date yesterday
New-JournalEntry -Date "1 year ago"
New-JournalEntry -Date "last month"
```

### Readme Dates

The final parameter available for the `New-JournalEntry` command is `-ReadMe`. This parameter is somewhat special. It represents some point in the future when you'd like to revisit a particular journal entry. You can either pass in a specific date, such as `"10/3/2033"`, or one of several valid expressions of time. These are written in the format of `"{integer} {years|months|weeks|days}"`, so `"1 year"`, `"15 months"`, `"6 weeks"`, and `"1024 days"` are all valid expressions. Durations are evaluated based on the date of the journal entry they are applied to. A journal entry dated January 1, 2021 with a readme of "1 year" will have a "readme expiration date" of January 1, 2022. 

How do you view readme entries? Check out the articles on [listing](/docs/basics/listing) and [reading](/docs/basics/reading) entries to learn more!

## Using the terminal

:::warning 

By default, every command you type is persisted to PowerShell's command history. This may or may not be desirable when it comes to writing journal content. Instructions for omitting journal content from PowerShell history are below.

:::

You can also write journal entries directly from your terminal window with the `Add-JournalEntryContent` command, or `aje` for short. As the name indicates, this command is *purely additive*. Journal entry content cannot be edited or deleted from the terminal. To do that, you'll need to open the entry in an editor. (More on that [here](/docs/basics/reading).) The simplest and most common way to add content to a journal entry is to run something like this:

```powershell
aje "Today I went to the park and it was swell."
```

That will append the specified text to the journal entry for the current date. If the entry doesn't yet exist, it will be created automatically. Here are a few more examples to demonstrate what else can be done.

```powershell
# Add some tags
aje "Journal CLI is neat!" -Tags cli-tools,neat

# Write for a date other than today
aje "Journal CLI is neat!" -Date yesterday 
aje "Journal CLI is neat!" -Date "3 days ago" 
aje "Journal CLI is neat!" -Date "1 week ago" 
aje "Journal CLI is neat!" -Date "6 months ago" 

# Place text under a specific header
aje "Journal CLI is neat!" -Header "## Discoveries"

# Reminder yourself to re-read the entry in the future
aje "Journal CLI is neat!" -Readme "10 years"
aje "Journal CLI is neat!" -Readme "10/1/2033"
```

A few things to keep in mind when writing in your terminal:

- There is an implicit `-Body` parameter used in all the examples above. In general, PowerShell will do a good job figuring out which parameter is intended to be the body text. If it fails to make that determination, you'll get an error saying so. In that case, just explicitly write `-Body "{your text here}"`.
- Duplicate tags are always filtered out. So if an entry is already tagged "fun" and you run `aje "I had fun today" -Tags fun`, the corresponding entry will only be tagged "fun" once.
- If a header is not specified, the body text is appended to the default date-based H1 header that is automatically added to all entries. 
- Headers must be written with between 1 and 6 leading `#` characters, followed by the header text. For example, `-Header "## Fun Day"` is valid. `-Header "Fun Day"` is not, and will result in an error message. 
- To write a multi-line body string, simply press the `Enter` key **before** typing your terminating quotation mark. In other words, if you write `aje "Here is some text"` and then press `Enter`, that entire string will be sent to the journal entry file. However, if you write `aje "Here is some text` (no terminating double quote) then `Enter` PowerShell will see that you're writing a multi-line statement.

### Sensitive Content

By default, every PowerShell command you enter is persisted to history. This may or may not be desirable, depending on the type of content you're writing from the terminal. To exclude all invocations of `Add-JournalEntryContent` from PowerShell history, add the following statement to your PowerShell profile. You can get the path to your profile by typing `$PROFILE` in your terminal. To edit it with VS Code, run `code $PROFILE`. (This assumes you've enabled [running VS code from the command line](https://code.visualstudio.com/docs/editor/command-line#_launching-from-command-line).)

```powershell
Set-PSReadLineOption -AddToHistoryHandler {
  param($line) 
  "Add-JournalEntryContent*","aje*" | ForEach-Object { 
    if ($line -like $_) {
      return $false
    }
  }
}
```

