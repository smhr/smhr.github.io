---
title: 'Simple script for login to the FUM hotspot.'
subtitle: 'Simple script for login to the FUM hotspot.'
summary: Simple script for login to the FUM hotspot.
authors:
- admin
tags:
- Academic
- Gnu/Linux
- Bash
- FUM
categories:
- scripts
date: "2019-04-17T00:00:00Z"
lastmod: "2019-04-17T00:00:00Z"
featured: false
draft: false
---
If you want to simply login to the [FUM](http://um.ac.ir/) hotspot, do the followings:

At first you must compute the MD5 hash of your password:

```bash
echo -n "Password" | md5sum | awk '{print $1}'
```

Please replace the Password with yours.

Then create a simple bash script:

```bash
#!/bin/bash
while true; do
    curl --data "username=Username&password=HashedPass" https://hotspot.um.ac.ir/login > /dev/null
    sleep 100
done
```

You should replase the Username with your FUM one and the HashedPass with the output of the above command.

You can make this script executable and put it in your binary PATHs (for example ~/bin) for easier life.

To logout simply create another script like below:

```bash
#!/bin/bash
curl --data "username=Username&password=HashedPass" https://hotspot.um.ac.ir/logout > /dev/null
```
