In Python 3.8.1, `domaın.tld` **will match** `'domain.tld$', re.IGNORECASE`. ſ **will match** s and K (Kelvin sign) **will match** k
In Ruby 2.7.0, `domaın.tld` **will NOT match** `/domain.tld$/i`. However, ſ **will match** s and K (Kelvin sign) will match k.
In Golang 1.13.8, `domaın.tld` **will NOT match** `'(?i)domain.tld$'`. However, ſ **will match** s and K (Kelvin sign) **will match** k.
In node 13.8.0, `domaın.tld` **will NOT match** `/domain.tld$/i`, ſ **will not match** s and K (Kelvin sign) **will not match** k.