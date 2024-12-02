---
layout: home
description: Welcome to my Reinforcement Learning blog where I explore RL concepts, projects, and insights to connect with top RL labs in London.
---

<style>
/* Add the CSS for the typing animation */
@keyframes typing {
    from { width: 0; }
    to { width: 100%; }
}

@keyframes blink-caret {
    from, to { border-color: transparent; }
    50% { border-color: black; }
}

.typing-animation {
    font-size: 24px;
    white-space: nowrap;
    overflow: hidden;
    border-right: 3px solid;
    width: 0;
    animation: typing 6s steps(50, end), blink-caret .75s step-end infinite;
    animation-fill-mode: forwards; /* Ensure the animation stays at the end state */
    margin: 20px auto;
    display: inline-block;
}
</style>
<div class="typing-animation" id="typing-text"></div> <!-- Add the typing animation -->
<script>
    // JavaScript to set the text content
    var text = "welcome to my journal...some thoughts, some projects";
    document.getElementById("typing-text").textContent = text;
    // Stop the caret blinking after the typing animation completes
    setTimeout(function() {
        document.querySelector('.typing-animation').style.borderRight = 'none';
    }, 4000); // Match the duration of the typing animation
</script>




### currently contributing to:

- [The Three Climate Experiment](https://github.com/itsnemoooo/three-climate-experiment) - Agentic building management systems with PyTorch.
- [Sold by RL](projects/sold-by-RL) - Optimising pricing strategies based on customer and competitor behaviour.

### publications 
```
- TODO
```
