# Redis Actions

**Set Key-Value:**
```bash
set tech redis
```

**Fetch Value:**
```bash
get tech
```

**Delete Key:**
```bash
del tech

# Also supports multiple keys
del tech framework
```

`(integer) 1` this integer refers to the key deletion count. If delete same key, result will be 0 as key is already deleted (or does not exist).

**Check Key Exists:**
```bash
exists tech

# Also supports multiple keys
exists tech framework
```
Out put is same as delete

**Key Expiration:**
```bash
# ex set expiry to seconds
set framework flsk ex 10

# px set expiry to miliseconds
set framework flsk px 10000
```

**Remove Expiration:**
```bash
persist framework
```
 Output is 1 if key is set to be expired or output is 0.

**Key Spaces:**
```bash
# Default is 0.
select 1
```
 Keys in different spaces are separated.

**Key Search Pattern:**
```bash
# Sample keys
set user:101:name Ritwik
# OK
set user:102:name John
# OK
set user:101:location Kolkata
# OK
set user:102:location "New York"
# OK

# Get all keys
keys *

# Search keys that has 101
keys *101*

# ? pattern matches exactly one value
keys user:10?:location

# [] matches specific values
keys user:10[1-9]:location
```

**Save Information:**
```bash
shutdown save

# Opposite is 
shutdown nosave
```

**Rename a Key:**
```bash
# Existing key-value is name => Ritwik, first_name => ritwik
rename name first_name

# Overwrites first_name key and set value Ritwik

# Rename a key but do not over-write if exists
renamenx name first_name
```

**Delete Key Asynchronously:**
```bash
# keys are deleted in parallel. Useful to delete large number of keys
unlink name first_name
```

**Check Type of Key:**
```bash
type name
# string
```

# String Data Type

**Set String Value:**
```bash
set name
```

**Append String:**
```bash
append name " Math"

get name
# => "Ritwik Math"
```

**Set Multiple:**
```bash
mset name Ritiwk surname Math age 31
```

**Get Multiple:**
```bash
mget name surname age
```

**Set Multiple with Caution:**
```bash
# set values if none of the keys already exists
msetnx name Ritwik profession Salaried

# works
msetnx profession Salaried location Kolkata
```

**Numeric Operations**
```bash
# Set integer value as string
set value 0

# Increaase integer value by 1
incr value

# Decreaase integer value by 1
decr value

# Increaase integer value by specific value
incrby value 10

# Decreaase integer value by specific value
decrby value 10

# Set floating point number
set float 2.5

# Increaase floating point value by specific value
incrbyfloat value 1

# Decreaase floating point value by specific value
incrbyfloat value -1
```

To decrease floating point number use negative value with `incrbyfloat`.

**Getset:**
```bash
# Get old value and then reset the key
getset value 0

# Outut => 8. 8 is the old value
```

Getset can be used for atomic reset.
```bash
# Set a integer value
set atomic 10

# Do dome increase/decrease operations
incr atomic
incr atomic
incr atomic

# Reset the value
getset atomic 10
# Output => 13
```

**String length:**
```bash
strlen website
```

**Set String with Caution:**
```bash
# Set a key
set value 0

# Set key only if it does not exist
setnx value 10
```

**Sub-string:**
```bash
# Set a value
set website https://www.udemy.com

# Unlike python the end character is also returned
getrange website 0 10
# Output => "https://www"
```
Position starts from 0. From last count starts from -1. The start index should always be less than end index or it will return empty string.

**Update String:**
```bash
# String characters will be updated starting from mentioned offset
setrange website 12 "idemi"
```
If the strlen of value > (strlen of key - offset), then value will replace all the characters from offset and new string will be greater in length. Otherwise, value will replace all the characters that is positioned in range of offset, offset + strlen of value.

**String Encoding Types:**
```bashh
set et 1

object encoding et
# Output => int

# String length less than 39
set et "Hello developers!"
object encoding et
# Output => embstr

# String length greater than 39
set et "Hello developers! I am a software developer. I love coding."
object encoding et
# Output => raw
```

**Store JSON:**
```bash
set json '{"name": "Ritwik Math", "age": 32}'

# Output => "{\"name\": \"Ritwik Math\", \"age\": 32}"
```

# Redis Lists

**Create a List:**
```bash
# Create a list with passed elements
lpush nums 1

# With multiple elements
lpush nums 1 2 3

# Using rpush
rpush nums 1
```

**Delete a List**
```bash
del nums
```

**Insert Element at Start:**
```bash
# Create a list called nums using lpush or rpush
lpush nums 0
```

**Insert Element at End:**
```bash
# Create a list called nums using lpush or rpush
rpush nums 2
```

**Insert after Specific Element:**
```bash
# Contents of nums 0, 1, 2
# after or before the existing element
linsert nums after 2 3
# Updated contents of nums 0, 1, 2, 3
linsert nums before 3 4
# Updated contents of nums 0, 1, 2, 4, 3
```

**Fetch Contents of Lists:**
```bash
# To get all elements use 0 as start and -1 as end
lrange nums 0 -1
```

**Fetch Element from Index:**
```bash
lindex nums 2
# Output => 2
```

**Remove Element from List:**
```bash
# From start
lpop nums
# Updated contents of nums 1, 2, 4, 3

# From end
rpop nums
# Updated contents of nums 1, 2, 4

# With count
rpop nums 2
# Updated contents of nums 1
```
