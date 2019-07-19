class: center, middle, inverse
# Finding UAC and COM bypasses
[Fun with SysInternals!]
.footnote[View source on [GitHub](https://github.com/audibleblink/com-and-uac)]

---
layout: false
class: center, middle

# UAC is not a security boundart ¯\_(ツ)_/¯
.footnote[ -- Microsoft ]

---
class: inverse

.left-column[
# [Agenda](#)
]

.right-column[

  .right[

# Auto-Elevating Executables
# Procmon
# Registry Hives
# Finding Vulnerable EXEs
# DEMO!
  ]
]

???

---
class: center, middle, inverse
# Auto-Elevating Executables
### [[What](#) are they?]

---

.left-column[
# What Are They
]

.right-column[
# EXEs That Enter into A High Integrity Context
.paragraph[
EXEs have manifests in them that describe properties and behaviors

If run by a local admin, the UAC prompt is bypassed

These are signed by Microsoft. Usually located in `C:\Windows`

]
]

---

.left-column[
# Why Is This Interesting?
]

## Some behavior is dependent on user-controllable input
.right-column[

Auto-Elevating executables will often look in predetermined locations for DLLs and helper EXEs

These are mainly in 

.h1[
- DLL Paths
- Registry Keys
- COM objects
- Named Pipes
]
]

---
class: center, middle, inverse
# Process Monitor
### [[aka](#) Procmon]

.footnote[[Get You](https://docs.microsoft.com/en-us/sysinternals/downloads/procmon) One]

---

.left-column[
# Procmon
]

## Windows monitoring tool that shows real-time file system, Registry and process/thread activity.

.right-column[
![](/static/1.png)
]

---
class: center, middle, inverse
# The Registry
### [dun dun [DUNN](#)]

---

.left-column[
# The Registry
]

# Hives

.right-column[

#### `HKEY_CURRENT_USER  [HKCU]`
  Modifiable by the logged in user without additional authentication

#### `HKEY_LOCAL_MACHINE [HKLM]`
  Contains configurations for the whole machine

#### `HKEY_CLASSES_ROOT [HKCR]`
  Merging of `HKLM:\Software\Classes` and `HKCU:\Software\Classes`


You can read more about HKCR and why the HKLM and HKCU hives are merged here.

https://msdn.microsoft.com/en-us/library/windows/desktop/ms724475(v=vs.85).aspx

]

---
class: center, middle, inverse
# Finding Vulnerable EXEs

---

.left-column[
# autoElevate
]

.right-column[
# Powershell can help

```
Get-Children -Recurse -Path *.exe | Select-String -Pattern autoElevate | Select Path
```

![](/static/2.png)

]

---
class: center, middle, inverse
# Demo
### [[Practical](#) Application]

---
class: center, middle, inverse
# What's Next
### [[Practical](#) Application]
