---
layout: post
title:  "Beauty of Recursion"
date:   2018-06-22 01:00:00 +0530
categories: cs
author: "Nilay Shrivastava"
comments: true
---
Is there something visually beautiful that can come out of Recursion? Industry stalwarts hate it (recursion is a big NO in production code!) and undergrads (like me) sweat while doing time complexity analysis for algorithms employing recursion. But whichever side of the spectrum you are in the software world, you would agree that recursion has a charm of its own. During my undergraduate years as I became familiar with the Computer Science world around me, I began to appreciate the inherent idea behind recursion. Moreover I understood that it not just a fancy technique used by clever programmers, but is something that is intrinsic to nature itself. This post is a presentation of __art__ that I learned and then coded during my leisure time. 

In this sense this post is more of a showcase/gallery than an educational blog.


<script src="../../../../js/p5.min.js"></script>
<script src="../../../../js/p5.dom.min.js"></script>
# Fractal Trees
This is the most common example of fractals.Notice how each part of the system is constructed recursively. Use the slider to generate more patters

<center><div id="tree" style="position: relative;"></div></center>

# Making things more natural approach: Stochastic Trees
Although the tree patterns were beautiful, they were too symmetric to be natural. Below is an example of __naturalness__ can be embedded by combining randomness with recursion. The underlying algorithm doesn't traverse all children in the recursion tree everytime, rather it choses the recursion branch randomly.
To make it more natural I also added the effect of __wind__ on our swaying tree.


<center><div id="swayingtree"></div><center>

# A more general approach: Using L-Systems

<center><div id="L1"></div></center>

<script type="text/javascript">
let width = 400;
let height = 400; 

function tree(p) {
    const PI = p.PI;
    const TWO_PI = PI * 2;

    let angle = PI / 4;
    let slider;
    
    var canvas;

    p.setup = () => {
        canvas = p.createCanvas(width, height);
        canvas.parent("tree");

        slider = p.createSlider(0, TWO_PI, TWO_PI);
        //const sliderX = (p.width  - slider.width  >> 1) + canvas.x,
        //  sliderY = (p.height - slider.height >> 1) + canvas.y;
        //slider.position(sliderX, sliderY);
        //slider.position(canvas.x,canvas.y);
        
        slider.position((p.width/2) + 350,p.height+550);

    };

    p.draw = () => {
        p.background(51);
        p.stroke(255);
        angle = slider.value();
        //console.log(angle);
        p.translate(200, p.height);
        p.branch(100);
    };

    p.branch = (len) => {

        p.line(0, 0, 0, -len);
        p.translate(0, -len);

        if (len > 4) {
            p.push();
            p.rotate(angle);
            p.branch(len * 0.67);
            p.pop();
            p.push();
            p.rotate(-angle);
            p.branch(len * 0.67);
            p.pop();
        }
    };

}

const simpleTree = new p5(tree);

function swaying(p) {
    const PI = p.PI;
    
    let yoff = 0.005;
    let seed = 6; //3

    var canvas;
    p.setup = ()=>{
        canvas = p.createCanvas(width, height);
        canvas.parent("swayingtree");
    };

    p.draw = ()=> {
        p.background(51);
        p.fill(255);

        p.stroke(255);
        p.translate(p.width / 2, p.height);
        yoff += 0.005;
        p.randomSeed(seed);
        // Start the recursive branching!
        p.branch(60, 0);
    };


    p.mousePressed = ()=> {
        yoff = p.random(1000);
    };


    p.branch = (h, xoff)=> {
        let sw = p.map(h, 2, 100, 1, 5);
        //let sc = map(h, 2, 100, 200, 255);
        p.strokeWeight(sw);
        p.line(0, 0, 0, -h);
        p.translate(0, -h);
        h *= 0.71;
        xoff += 0.1;

        if (h > 10) {
            let n = p.floor(p.random(0, 5));
            for (let i = 0; i < n; i++) {
                let theta = p.map(p.noise(xoff + i, yoff), 0, 1, -PI / 3, PI / 3);
                if (n % 2 == 0)
                    theta *= -1;
                p.push();
                p.rotate(theta);
                p.branch(h, xoff);
                p.pop();
            }
        }
    };
}
const swayingTree = new p5(swaying);
</script>

{% if page.comments %}
<div id="disqus_thread"></div>
<script>

/**
*  RECOMMENDED CONFIGURATION VARIABLES: EDIT AND UNCOMMENT THE SECTION BELOW TO INSERT DYNAMIC VALUES FROM YOUR PLATFORM OR CMS.
*  LEARN WHY DEFINING THESE VARIABLES IS IMPORTANT: https://disqus.com/admin/universalcode/#configuration-variables*/
/*
var disqus_config = function () {
this.page.url = PAGE_URL;  // Replace PAGE_URL with your page's canonical URL variable
this.page.identifier = PAGE_IDENTIFIER; // Replace PAGE_IDENTIFIER with your page's unique identifier variable
};
*/
(function() { // DON'T EDIT BELOW THIS LINE
var d = document, s = d.createElement('script');
s.src = 'https://euler16.disqus.com/embed.js';
s.setAttribute('data-timestamp', +new Date());
(d.head || d.body).appendChild(s);
})();
</script>
<noscript>Please enable JavaScript to view the <a href="https://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
{% endif %}