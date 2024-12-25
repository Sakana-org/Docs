---
title: Switch files | Sakana Docs
description: How switch files work
---

# NSP / Nintendo Submission Package (PFS0)
Main file games are distributed in. It contains multiple files inside (mainly nca).

## Structure
| Offset                    | Value               | Type      |
| ------------------------- | ------------------- | --------- |
| 0 to 3                    | Magic Number (PFS0) | UInt8     |
| 4                         | File Number         | UInt32 LE |
| 8                         | String Table Size   | UInt32 LE |
| 16 + (24 * File Number)   | String Table Start  | UInt8     |
| String Table Start + Size | Data Offset         | Nca       |

The String Table is a list of file names separated by NULL (U+0000).\
The Data section has multiple Nca files, each file can be found at offset `16 + fileN * 24` where fileN is the number of the file (EX: 3) starting at 0.

# NCA / Nintendo Content Archive
These files contain code, assets and other, the contents are encrypted mainly with AES-128-XTS (Variant of ECB) and AES-128-CTR.

## Structure
| Offset               | Value            | Type         |
| -------------------- | ---------------- | ------------ |
| 16 + fileN * 24      | Body offset      | BigUInt64 LE |
| 16 + fileN * 24 + 8  | File size        | BigUInt64 LE |
| 16 + fileN * 24 + 16 | File name offset | UInt32 LE    |

Note: The 16 in front is the `Header offset` which always is 16 but is kept separate incase of future modification.

The File Name Offset is the offset for the string table.\
The file contents are found at offset `Body offset + Data Offset`.