---
up:
  - "[[Shell MOC]]"
related:
  - "[[Sh ps command]]"
  - "[[Sh pkill command]]"
  - "[[Sh Process]]"
created: 2024-04-29
tags:
  - note/develop🍃
Link: https://linuxize.com/post/pgrep-command-in-linux/
---

- It allows you to find the [[Sh Process]] IDs of a running program based on given criteria.
- It can be a full or partial process name
## Syntax
```sh
pgrep [OPTIONs] <PATTERN>
```
- `<PATTERN>` is specified using extended regular expressions.
- If you want to send signals to the matched processes use [[Sh kill command]] . This command is a wrapper around the `pkill`, and uses same options and pattern matching.

| **Command**                                | **Output**                                                                                                                                                                        |
| ------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `pgrep [pro_name]`                         | displays the PIDs of all running programs that match with the given name.                                                                                                         |
| `pgrep -d <delim>`                         | The `-d` option allows you to specify a different delimiter.<br>`pgrep` prints each matched process ID on a newline.                                                              |
| `pgrep ssh -l`                             | show the process name along with its ID                                                                                                                                           |
| `pgrep -f ssh`                             | When `-f` option is used the command matches against full argument lists.<br>By default, `pgrep` matches only against the process name                                            |
| `pgrep -u root`                            | display processes being run by a given user                                                                                                                                       |
| `pgrep -u root,mark`                       | To specify multiple users, separate their names with commas                                                                                                                       |
| `pgrep -l -u mark gnome`                   | You can also combine options and search patterns.<br>Print all processes and their names that run under user “mark” and contains “gnome” in their names you would type            |
| `-n` (for newest) or the `-o` (for oldest) | To display only the least recently (oldest) or the most recently (newest) started processes                                                                                       |
| `pgrep -v -u mark`                         | To reverse the matching, i.e. to show only processes that do not match the given criteria<br>The following command will print all processes that are not being run by user “mark” |
| `pgrep -c -u mark`                         | print only the count of the matching processes                                                                                                                                    |
| `pgrep '^s' -l`                            | Up arrow = line start with s                                                                                                                                                      |
| `pgrep 's$' -l`                            | $ end with                                                                                                                                                                        |
| `pgrep '^ssh$' -l`                         | If you want to match only the processes which names are exactly as the search pattern                                                                                             |
>[!info]
>The command returns `0` when at least one running process matches the requested name. Otherwise, the [exit code](https://linuxize.com/post/bash-exit/) is `1`. This can be useful when writing [[Shell MOC]].

>[!tldr]
>The caret (`^`) character matches at the beginning of the string, and the dollar `$` at the end.
