---
title: Pollux API Default group permission syntax and default value
tags: Gemini Project, Pollux
---

# Pollux API group permission syntax and default value

## Overview

Each `Group` must bind to one `Permission`, and every subset in `Permission` may have its own `PermissionType`, each `PermissionType` can be divided in to three type (`Read`, `Write`, `Delete`), which present by `Access`.

:::info
Note: Those items below are **not subject to `Read` permission** after its single item being set to **`published: true`**: **`news`, `post`**
:::

:::info
Note: Those items below are **not subject to `Read` permission**: `reply`, `property`
:::

### `Permission`
- news `PermissionType`
- post `PermissionType`
- reply `PermissionType`
- item `PermissionType`
- property `PermissionType`
- user `PermissionType`
- group `PermissionType`
- layout `PermissionType`
- log `PermissionType`
- analytics `PermissionType`
- loginAdmin `Boolean`
- banned `Boolean`

### `PermissionType`
- owner `Access`
- group `Access`
- anyone `Access`

### `Access`
- read `Boolean`
- write `Boolean`
- delete `Boolean`

### Interpretation & Example Format

Like Linux file permission expressed in terms of octal code, the example within this document will follow that but with a little different.

:::info
#### **Linux way**

`R`: `Read` $\to$ Yes: **1** No: **0**
`W`: `Write` $\to$ Yes: **1** No: **0**
`X`: `Execute` $\to$ Yes: **1** No: **0**
<br />
```
User   Group   All 
R W X  R W X  R W X
```

Example: Imaginary a file created in Linux enviroment, and its permission mode had been set to **`750`**: that representative the file’s **owner** can **`Read`, `Write`, `Execute`** it; other users in the **same group as owner** can **`Read`, `Execute`** it but **can't `Write`**, **anyone** apart from this **can’t do anything**.
<br />
```
User   Group   All 
R W X  R W X  R W X
1 1 1  1 0 1  0 0 0
```
$111_{(2)} \to 7_{(8)}, 101_{(2)} \to 5_{(8)}, 000_{(2)} \to 0_{(8)}$

So you got permission code **`750`**
:::

:::info
#### **Pollux Way**

Linux limited the access of every single file with there own permission mode given, but Pollux not go this way; we limited user access things by group permission.

`R`: `Read` $\to$ Yes: **1** No: **0**
`W`: `Write` $\to$ Yes: **1** No: **0**
`D`: `Delete` $\to$ Yes: **1** No: **0**
<br />
```
User   Group   All 
R W D  R W D  R W D
```

> Pollux is a part of Gemini platform service that manage your contents as simple as piss, can you "Execute" your news? Must not, so we replace `Execute` with `Delete`. Having your brave assistant won't delete important things anymore by using our system.
> [name=Aries Cs, Developer of Gemini Project]

Example: Imaginary a user Anne on Gemini want to access some `news`. Anne's user group had had permission mode **`Group.Permission.news`**  **`764`**: that means Anne can **`Read`, `Write`, `Delete`** the `news`es **created by self**; Anne also can **`Read`, `Write` (Edit)** the `news`es created by others in the **same group**, but **can't `Delete`** them; apart from this Anne **can’t do anything**.
<br />
```
User   Group   All 
R W X  R W X  R W X
1 1 1  1 1 0  1 0 0
```
$111_{(2)} \to 7_{(8)}, 110_{(2)} \to 6_{(8)}, 100_{(2)} \to 4_{(8)}$

So you got permission code **`764`**
::::

## Default Permission
The default permissions are service build-in rules, you can edit it or add your own rules. Be care of any action of modify `admin` permission.

### Admin
**`admin`**
| `Permission` | `Access` |
| ------ | ------ |
| `news` | `775` |
| `post` | `775` |
| `reply` | `775` |
| `item` | `777` |
| `property` | `777` |
| `user` | `755` |
| `group` | `777` |
| `layout` | `777` |
| `log` | `444` |
| `analytics` | `444` |
| `loginAdmin` | `true` |
| `banned` | `false` |

### Staff
**`staff`**
| `Permission` | `Access` |
| ------ | ------ |
| `news` | `775` |
| `post` | `775` |
| `reply` | `775` |
| `item` | `766` |
| `property` | `766` |
| `user` | `755` |
| `group` | `444` |
| `layout` | `666` |
| `log` | `444` |
| `analytics` | `444` |
| `loginAdmin` | `true` |
| `banned` | `false` |

### Cooperator
**`cooperator`**
| `Permission` | `Access` |
| ------ | ------ |
| `news` | `774` |
| `post` | `774` |
| `reply` | `774` |
| `item` | `766` |
| `property` | `766` |
| `user` | `754` |
| `group` | `444` |
| `layout` | `664` |
| `log` | `000` |
| `analytics` | `440` |
| `loginAdmin` | `true` |
| `banned` | `false` |

### Contributor
**`contributor`**
| `Permission` | `Access` |
| ------ | ------ |
| `news` | `444` |
| `post` | `744` |
| `reply` | `744` |
| `item` | `766` |
| `property` | `766` |
| `user` | `744` |
| `group` | `000` |
| `layout` | `000` |
| `log` | `000` |
| `analytics` | `000` |
| `loginAdmin` | `false` |
| `banned` | `false` |

### Normal
**`normal`**
| `Permission` | `Access` |
| ------ | ------ |
| `news` | `444` |
| `post` | `744` |
| `reply` | `744` |
| `item` | `444` |
| `property` | `444` |
| `user` | `744` |
| `group` | `000` |
| `layout` | `000` |
| `log` | `000` |
| `analytics` | `000` |
| `loginAdmin` | `false` |
| `banned` | `false` |

### Banned
**`banned`**
| `Permission` | `Access` |
| ------ | ------ |
| `news` | `000` |
| `post` | `000` |
| `reply` | `000` |
| `item` | `000` |
| `property` | `000` |
| `user` | `000` |
| `group` | `000` |
| `layout` | `000` |
| `log` | `000` |
| `analytics` | `000` |
| `loginAdmin` | `false` |
| `banned` | `true` |

:::info
`Banned` Permission is against to the hacker who send lost of bad request to API. 
:::