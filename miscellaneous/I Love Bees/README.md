I Love Bees

Description

I stumbled on to this strange website. It seems like a website made by a flower enthusiast, but it appears to have been taken over by someone... or something.

Can you figure out what it's trying to tell us?

https://static.icec.tf/iloveflowers/


Resolution

We have a favicon.gif in the head

So let's try to analyse that.

You can use convert tools for extract png from gif .


convert favicon.gif output.png

We search now the pattern of the flag in the gif's fames

strings *.png | grep Ice

IceCTF{MY_FAVORITE_ICON}
IceCTF{MY_FAVORITE_ICON}
IceCTF{MY_FAVORITE_ICON}
IceCTF{MY_FAVORITE_ICON}
IceCTF{MY_FAVORITE_ICON}
IceCTF{MY_FAVORITE_ICON}
IceCTF{MY_FAVORITE_ICON}
IceCTF{MY_FAVORITE_ICON}
IceCTF{MY_FAVORITE_ICON}
IceCTF{MY_FAVORITE_ICON}
IceCTF{MY_FAVORITE_ICON}
IceCTF{MY_FAVORITE_ICON}
IceCTF{MY_FAVORITE_ICON}
IceCTF{MY_FAVORITE_ICON}
IceCTF{MY_FAVORITE_ICON}
IceCTF{MY_FAVORITE_ICON}


So validate the chall with the flag IceCTF{MY_FAVORITE_ICON}