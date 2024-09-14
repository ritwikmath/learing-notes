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

**Key Expiration :**
```bash
# ex set expiry to seconds
set framework flsk ex 10

# px set expiry to miliseconds
set framework flsk px 10000
```

**Remove Expiration :**
```bash
persist framework
```
 Output is 1 if key is set to be expired or output is 0.

**Key Spaces :**
```bash
# Default is 0.
select 1
```
 Keys in different spaces are separated.

**Key Search Pattern :**
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

**Save Information :**
```bash
shutdown save

# Opposite is 
shutdown nosave
```

**Rename a Key :**
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

