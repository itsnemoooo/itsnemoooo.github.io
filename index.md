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
    font-size: 30px;
    white-space: nowrap;
    overflow: hidden;
    border-right: 3px solid;
    width: 0;
    animation: typing 4s steps(40, end), blink-caret .75s step-end infinite;
    animation-fill-mode: forwards; /* Ensure the animation stays at the end state */
    margin: 20px auto;
    display: inline-block;
}
</style>
<div class="typing-animation" id="typing-text"></div> <!-- Add the typing animation -->
<script>
    // JavaScript to set the text content
    var text = "welcome to my journal";
    document.getElementById("typing-text").textContent = text;
    // Stop the caret blinking after the typing animation completes
    setTimeout(function() {
        document.querySelector('.typing-animation').style.borderRight = 'none';
    }, 4000); // Match the duration of the typing animation
</script>

<video width="100%" height="auto" controls autoplay loop muted>
    <source src="https://itsnemoooo.github.io/assets/vids/welcome_animation.mp4" type="video/mp4">
    Your browser does not support the video tag.
</video>
### current projects

- [The Three Climate Experiment](projects/three_climate_experiment) - Agentic building management systems. DDQN with experiments in Experience Replay buffers.
- [Sold by RL](projects/sold-by-RL) - Developed a Deep Deterministic Policy Gradient-based pricing agent to navigate complex ecommerce data.

### publications
- TODO

<!-- - [Lessons from my startup](blog/cofounder-story)

- [What I learned in filters](blog/what-I-learned-in-filters) -->
