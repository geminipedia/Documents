---
title: Pollux API Default Error Code Comparison Table
tags: Gemini Project, Pollux
---

# Pollux API Default Error Code Comparison Table

## Syntax

**`ERR_`** + **EVENT_SOURCE_PREFIX** + **EVENT_DESCRIPTION**

:::info
example

**`ERR_U000`** $\to$ **`U`**: User, **`000`**: already existed
so error code `ERR_U000` presents **User already existed**

:::

## Event Source Prefix

A: Admin
B: Site
C: Page
D: Theme
E: Entity
F: General
G: Group
H: File
I: Item
J: Image
K: i18n
L: Log
M: Post
N: News
O: Note
P: Property
Q: Quote
R: Reply
S: Statement
T: Tag
U: User
X: Lang

## Event Description

000: already existed
001: does not exist
00F: authorization failed
0FF: invalid token
F00: permission deny
FFF: unexpected error