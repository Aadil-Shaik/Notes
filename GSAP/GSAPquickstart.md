# GSAP

credit : Web Dev Simplified, GreenSock Learning(GSAP official youtube channel), Sheryians Coding School

```bash
    gsap.from(' //selector_name ' , { //properties , //properties, //properties } )
```

```bash
    gsap.to(' //selector_name ' , { //properties , //properties, //properties } )
```

```bash
    gsap.fromTo( ' //selector_name ' , { //from } , { //to } )
```

- duration : time to execute the animation
- initial condition : axis or opacity
- delay : delay before execution starts
- stagger : time before consecutive elements of same name execute same animation
- ease : the speed curve of animation. go onnn website and copy premade

  eg. 'bounce' , 'power2.in'

eg.

```bash
    gsap.from('.right', {duration:2, x: '-100vw', delay: 1, ease: 'power2.in'})
    gsap.from('.left' , {duration:1, x: '-100%', delay:2 })

    gsap.from('.link' , {duration:1, opacity:0, delay:1, stagger: .5})
    gsap.to('.footer', {duration:1, y:0, ease:'elastic', delay:2.5 })

    gsap.fromTo('.button' , { opacity:0, scale:0, rotation: 720 }, { duration:1, delay: 3.5, opacity:1, scale:1, rotation: 0 } )
```

**See the updates**

```bash
    const obj = { x: 0 }
    gsap.to( obj, { duration: 2, x: 100, onUpdate: () => console.log( obj.x ) } )
```

**Using Timeline**

```bash
    const timeline = gsap.timeline({ defaults:{ duration: 1 } })

    timeline        //chaining all the from's
        .from('.header', { y: '-100%', ease: 'bounce' })
        .from('.link', { opacity: 0, stagger: .5 })
        .from('.right', { x: '-100vw', ease: 'power2.in' }, 1)      //delay inside is relative delay and delay outside is absolute delay
        .from('.left', { x: '-100%' }, '<.5' )      // < indicates when previous starts and the .5 here is time
        .to( '.footer', { y: 0, ease: 'elastic' })
        .fromTo( '.button', { opacity: 0, scale: 0, rotation: 720 }, { opacity:1, scale: 1, rotation: 0 })

        //To reverse it

        coooonnnst button = document.querySelector('.button')
        button.addEventListener('click', ()=> {
            timeline.timeScale(3)       //3 times faster
            timeline.reverse()
        })
```

**Multiple elemts**

```bash
    .from( ["#id1", "#id2"], {
        x: -60,
        scale: 1.6,
        opacity: 0,
        duration: 1
     } )                        //for a 100px image this appears to drop from top with right side as fixed origin
```

**Looping and yoyo**

```bash
    to.("#arrow", {
        y:20,
        yoyo:true,             //does forward animation aswell as backward animation with smoothening at end
        repeat:-1              //Loop stuck indefinitely
    })
```

### Functions in gsap

onStart and onUpdate

```bash
    gsap.from("#element", {
        onStart: function(){
            --x--
        }
    })
```

## Scroll Trigger

needs js cdn from gsap website

```bash
    gsap.registerPlugin(ScrollTrigger);

    gsap.to(".c" , {
      scrollTrigger: ".c",      //as soon as .c hits viewport at the very bottom, animation starts
      x : 400,
      rotation: 360,
      duration: 3
    })
```

**Toggle Actions**

- inside scrollTrigger object put `markers: true` to get a visual indicator which help in development

configure scroll trigger as an object

Syntax:

- toggleActions: " a b c d "

a - when screen enters element

b - when screen exits element downwards

c - when screen reenters element from downwards

d - when we scroll back all the way back up

x <= play pause resume reverse restart reset complete none

- start : " //part of element //part of screen/viewport ", default: top bottom

use keywords like top, center, bottom or

for element use pixels

for screen use % or vise versa

- end : " //part of element //part of screen/viewport ", default: bottom top

make end relative to start `end: "+-300", // add px or no. ur wish`

- to start ro end : make relative additions by using functions to apply it with respect to the element's size `end: () => "+-" + document.querySelector(".c").offsetWidth, `

you can animate different elements with different element's start condition and different element's end condition

```bash
    gsap.registerPlugin(ScrollTrigger);

    gsap.to(".b" , {
      scrollTrigger: {
        trigger: ".a",
        start: " top 50px ",
        endTrigger: ".c",
        end: " bottom 80% ",
        markers: true,
        toggleActions: restart pause reverse pause
      },
      x : 400,
      rotation: 360,
      duration: 3
    })
```

**Scrub** : links animation to scroll

    `scrub: true` => default linking

    `scrub: 1` => takes 1 second to catchup and is smooth

- timeline with scroll trigger

```bash
    gsap.registerPlugin(ScrollTrigger);

    let t = gsap.timeline({
        scrollTrigger: {
            trigger: ".c",
            start: "top center",
            end: "top 100px",
            scrub: 3,
            markers: true
        }
    });

    t.to(".c",{
        x: 400,
        rotation: 360,
        ease: none,
        duration: 3
    })
    .to(".c"{
        background-color: purple,
        duration: 1
    })
    .to(".c"{
        x: 0,
        duration: 3
    })
```

**Pinning**

`pin: true` => makes the element stay at the start point on screen until end is triggered

`pinSpacing: false` => disables extra padding that is automatically added if the element falls short of the animation description

here is one of the advance syntax for 4 pannels coming over like a deck of cards showing up one after another from the bottom

````bash
    gsap.registerPlugin(ScrollTrigger);

    gsap.utils.toArray(".panel").forEach((panel, i) => {
        ScrollTrigger.create({
            trigger: panel,
            start: "top top",
            pin: true,
            pinSpacing: false
        });
    });

**Snapping**

    when user leaves the scroll inactive, it brings the scroll to nearest snap zone

    you need to set the snap zones

    the followinnnng exmaple has 'x' number of panels horizontally with overflow hidden. scrolling downwards moves one panel to another smoothly as scrub : 1.

```bash
    gsap.registerPlugin(ScrollTrigger);

    let sections = gsap.utils.toArray(".panel");

    gsap.to(sections, {
        xPercent: -100* (sections.llength -1),
        ease: "none",
        scrollTrigger: {
            trigger: ".container",
            pin: true,
            scrub: 1,
            snap: 1/(section.length-1),     //basically a snap zone is width of container
            end: () => "+-" document.querySelector(".contaner").offsetWidth  //total width of all panels
        }
    })
````

**Callbacks and Custom Options**

write in scrollTrigger function's object

onEnter(): () => console.log( "animation started" ),

onLeave(): () => console.log( "animation reached end" ),

onEnterBack(): () => console.log( "entered the end area again" ),

onLeaveBack(): () => console.log( "leaving from the start point" ),

onUpdate(): (self) => consolge.log( "update", self.progress.toFixed(3) ), //each time scroll trigger is updated upto 3 decimal places

onToggle(): (self) => console.log("toggled", self.isActive), //true or false when active

toggleClass: "active", //set class to active. in css put some property when active

id: "id_name", //outside of scrollTrigger grab it by `let trigger = ScrollTrigger.getById("id_name");`

**Set Defaults**

ScrollTrigger.defaults({
toggleActions: "restart pause resume none",
markers: true
});

By default the scrolling of viewport is considered. If you want to set some other element then

`scroller: "#container",`

BY default ScrollTrigger looks for vertical scrollig

`horizontal: true,`

## Extras

### Textillate.js

import necessary cdns - minified

js: jQuery, lettering.js, css: use animate css cdn codepen

copy syntax from github. copy the one where everything is initialized

use the animmation preview on website to choose 'in' and 'out' animation

- Don't forget to mention the call back function to call 'out' animation

```bash
    gsap.from("#h1_tag_element", {
        onStart: function(){
            $('#h1_tag_element').textillate({
                in:{
                    effect: 'fadeInUp',
                    callback: function(){
                        $('#h1_tag_element').textillate('out')
                    }
                },
                out:{
                    effect: 'fadeOutUp'
                }
            }) ;
        }
    })
```

<!-- ## Examples and usecases

use gsap directly after importing cdn

need to learn
scrolltrigger link to skew of images
pair with css scroll snapping
 -->
