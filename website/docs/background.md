---
title: History
sidebar_position: 6
---

> The story behind how `journal-cli` came to be.

Sometime late in 2017, I found myself flipping through really old entries in my Google Calendar. Turns out I had entries in there dating back to 2001. It was interesting taking a stroll down memory lane and seeing everything from the mundane ("Dentist Appt") to the exciting ("Date with Austin chick")\*. It got me thinking that I should make an effort to write down the highlights of my day _every day_ because future-me might be interested in knowing what I did on, say, December 13th, 2018. ("Started developing `journal-cli`.") So I made the decision to start keeping a daily journal. 

Over the following year I used a variety of note-taking applications to jot down my life's events, despite my unease at spelling out such personal details in cloud-based tools that didn't offer client-side encryption. Then, in June of 2018, Typeform - a surveying app I've used - suffered a breach and some of my data was stolen. Luckily, the data taken from my account wasn't sensitive. But the incident cemented my fears that _nothing is safe in the cloud_. I resolved to find another, safer tool to use for journaling. 

However, every application I tried suffered from one or more serious flaws. They were either insecure, too complicated, too constraining, or offered a poor writing experience. I really wanted to use [Typora](https://typora.io/) - hands-down the best markdown editor available - but it lacked one key feature: It offered no built-in mechanism for tagging files. Tags are essential for me because they basically constitute my journal's index.  

Finally, I had a realization. *Typora supports yaml front matter. I can use front matter to add tags to each file and create a command line tool to parse the tags from each journal file!* Thus, `journal-cli` was born.

\- Nick Spreitzer ([@Refactorsaurusrex](https://github.com/refactorsaurusrex))

---

\* These days I generally refer to that "chick from Austin" as "wife".