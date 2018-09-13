Lights out

Description :

Help! We're scared of the dark!

https://static.icec.tf/lights_out/index.html

Resolution

We have to play with the css parameters in the firefox inspector: 

body 
{
background-color : white
}

delete node <div class="alert alert-danger">Who turned out the lights?!?!</div>


article, aside, details, figcaption, figure, footer, header, hgroup, main, menu, nav, section, summary{
display:true;
}

We can see now the flag :

IceCTF{styles_turned_the_lights}