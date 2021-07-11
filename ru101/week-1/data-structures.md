# Data Structures

- [Data Structures](#data-structures)
  - [Data Types Overview](#data-types-overview)
  - [Keys & Expiration](#keys--expiration)
    - [Key attributes](#key-attributes)
    - [Key Spaces](#key-spaces)
    - [Key Name Examples](#key-name-examples)
    - [Key Commands](#key-commands)
    - [Key Expiration](#key-expiration)
  - [Strings](#strings)
  - [Hashes](#hashes)
  - [Lists](#lists)
  - [Sets](#sets)
  - [Sorted Sets](#sorted-sets)

---

## Data Types Overview

[Data Types](https://redis.io/topics/data-types)

---

## Keys & Expiration

- Keys are the primary way to access data values within redis.
  
### Key attributes

- Unique by definition
- Can be composed of ANY sequence of bytes
- Binary Safe
  - "Foo", 42, 3.1415, 0xff
- Key names can be up to 512MB in size
- Keys should favor readability over length

### Key Spaces

- Logical Databases
  - Database Zero
  - Provides separation of key-names
  - Useful when needing multiple key-spaces for one application
- Flat key space
- No automatic name-spacing
- Developer must use good name-spacing

### Key Name Examples

- Key-names are case sensitive.
- Redis server does a binary comparison on key-names
  - exp: `registeredusers:1000:followers` != `RegisteredUsers:1000:followers`

- Parts of a key name
  - `user:id:followers`
    - `user:1000:followers`
      - user: object name
      - 1000: unique identifier for the instance
      - followers: composed object

### Key Commands

- `SET key value [EX seconds] [PX milliseconds] [NX|XX]`
  - Check for nonexistence with `NX` or existence with `XX`
    - example: `SET customer:1000 fred NX` >> `OK`
- `GET key`
  - example: `GET customer:1000` >> `fred`
- `KEYS pattern`
  - Blocks until complete
  - Never use in production
  - Useful for debugging
    - example: *Get all customers who has an ID beginning with '1'*
      - `KEYS customer:1*`
- `SCAN slot [MATCH pattern] [COUNT count]`
  - Iterates using a cursor
  - Only iterates over a handful at a time
  - Returns a slot reference
  - May return 0 or more keys per call
  - Safe for production
    - example: `SCAN 0 MATCH customer:1* COUNT 1000`
- `DEL key [key...]`
  - Remove the key and memory associated with the key
  - This is a blocking operation
    - example: `DEL customer:1000`
- `UNLINK key [key...]`
  - Key is unlinked, memory associated is reclaimed by async process
  - Non blocking
    - example: `UNLINK customer:1000`
- `EXISTS key [key...]`
  - Returns `1` if key exists and `0` if it does not
    - example: `EXISTS customer:1000`

### Key Expiration

---

## Strings

---

## Hashes

---

## Lists

---

## Sets

---

## Sorted Sets
