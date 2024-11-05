---
layout: home
title: Home
description: Welcome to my Reinforcement Learning blog where I explore RL concepts, projects, and insights to connect with top RL labs in London.
---
## Hello internet,

I’m Nathan, an American engineer based in London. Here are my insights, projects, and research. All opinions are my own.

## Latest Blog Posts

{% for post in site.posts limit:3 %}
- [{{ post.title }}]({{ post.url }}) - {{ post.date | date: "%B %d, %Y" }}
{% endfor %}

## Featured Projects

- [GridWorld RL Agent](projects/gridworld) - Implemented a Q-Learning agent to navigate a GridWorld environment.
- [RL Stock Trading Bot](projects/stock-trading-bot) - Developed an RL-based trading bot for stock market predictions.

## Connect with Me

- [LinkedIn](https://www.linkedin.com/in/yourprofile)
- [GitHub](https://github.com/itsnemoooo)
- [Twitter](https://twitter.com/yourusername)