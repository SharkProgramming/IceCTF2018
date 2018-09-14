# Toke relaunch

## Description :

We've relaunched our famous website, Toke! Hopefully no one will hack it again and take it down like the last time.

https://static.icec.tf/toke/

## Resolution

We first try to read the file robots.txt

https://static.icec.tf/toke/robots.txt

Succes ! We a page hidden inside it.

User-agent: *
Disallow: /secret_xhrznylhiubjcdfpzfvejlnth.html

So let's go to this page

https://static.icec.tf/toke/secret_xhrznylhiubjcdfpzfvejlnth.html

We have the flag

IceCTF{what_are_these_robots_doing_here}
