---
layout: post
title:  "file descriptor"
categories: os
date:  2022-12-07 12:53:58 +0900
---


![](https://www.computerhope.com/jargon/f/file-descriptor-illustration.jpg)

A **file descriptor** is a number that uniquely identifies an open file in a computer's operating system. It describes a data resource, and how that resource may be accessed.


When a program asks to open a file — or another data resource, like a **network socket** — the **kernel**:

1. Grants access.
2. Creates an entry in the global file table.
3. Provides the software with the location of that entry.

The descriptor is identified by a unique **non-negative integer**, such as 0, 12, or 567. At least one file descriptor exists for every open file on the system.

File descriptors were first used in Unix, and are used by modern operating systems including Linux, macOS, and BSD. In Microsoft Windows, file descriptors are known as file handles.

<br/>

- [Overview](#overview)
- [Stdin, stdout, and stderr](#stdin-stdout-and-stderr)

<br/>
## Overview

When a **process** makes a successful request to open a file, the **kernel** returns a file descriptor which points to an entry in the kernel's global **file table**. The file table entry contains information such as the inode of the file, byte offset, and the access restrictions for that data stream (read-only, write-only, etc.).

<br/>
## Stdin, stdout, and stderr

On a Unix-like operating system, the first three file descriptors, by default, are **STDIN** (standard input), **STDOUT** (standard output), and **STDERR** (standard error).


<table class="mtable3 tab">
<tbody>
<tr class="tcw">
<th style="width:155px">Name</th>
<th>File descriptor</th>
<th>Description</th>
<th>Abbreviation</th>
</tr>
<tr class="tcw">
<td>Standard input</td>
<td style="text-align:center"><b>0</b></td>
<td>The default data stream for input, for example in a command pipeline. In the terminal, this defaults to keyboard input from the user.</td>
<td><b>stdin</b></td>
</tr>
<tr class="tcw">
<td>Standard output</td>
<td style="text-align:center"><b>1</b></td>
<td>The default data stream for output, for example when a command prints text. In the terminal, this defaults to the user's screen.</td>
<td><b>stdout</b></td>
</tr>
<tr class="tcw">
<td>Standard error</td>
<td style="text-align:center"><b>2</b></td>
<td>The default data stream for output that relates to an error occurring. In the terminal, this defaults to the user's screen.</td>
<td><b>stderr</b></td>
</tr>
</tbody>
</table>





<br/>
<br/>
References

- [https://www.computerhope.com/jargon/f/file-descriptor.htm#overview](https://www.computerhope.com/jargon/f/file-descriptor.htm#overview)