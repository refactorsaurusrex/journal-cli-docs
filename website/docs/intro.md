---
sidebar_position: 1
---

# Quick Start

Let's get started with `journal-cli` **in 5 minutes or less**.

:::info

This documentation is for `journal-cli` v2. Documentation for v1 can be found [here](https://v1.journalcli.app). 

:::

1. Ensure you have a default application set for `.md` files.
2. Install the [latest version of PowerShell](https://github.com/PowerShell/PowerShell/releases/latest) for your system.
3. Install [journal-cli](https://www.powershellgallery.com/packages/JournalCli): `Install-Module JournalCli`.
4. Restart your PowerShell terminal **or** run `Import-Module JournalCli`. (You do not need to do both; `journal-cli` will automatically be imported into new PowerShell sessions after installation.)
5. Run `Set-JournalSettings -Location C:\Path\To\Your\Journal`. Be sure to use a path appropriate for your operating system.
6. Run `New-JournalEntry -Tags something,something-else` and start writing about your day today!

## Next Steps

Now that you've gotten started, I highly recommend that you read the four articles in the "Basic Usage" section. They should be read *in order* since the build on one another. By then you should be ready for the "Advanced Usage" section.  
