
# Lessons from failures: #001 Whose IP is it anyway?

### London, UK - September, 2024 

I was wrapping up my Masters in AI for Sustainable Development at University College London. Working in the AI centre with friends, running reinforcement learning experiments, I was finally applying what I had learned over the course.

I managed to achieve some breakthrough results on my project, having spent the summer focused on creating better control solutions for buildings to manage their energy when impacted by extreme climates. 

This is a topic I am passionate about, and the 55 percentage point improvement over baseline for energy savings was quite exciting.

Not only that, I was staring down the precipice of valuable research in reinforcement learning for building management, something I came to London to try my hand at.

However, what was valuable for research could also be valuable for industry. 

### An opportunity arises

A company reached out regarding the results from my paper. They were interested in forming an incubator inside of a monolithic American-based company, and they decided my results were good enough to commercialise. 

Let's call them "PILL Inc". They had been working with my university for quite some time to try and get some venture programs up and running and this looked like the opportunity. They offered to fund me and instructed me to form a founding team, enlisting the help of a colleague from the AI centre who they were already in contact with through her PhD funding. 

She can be called "Elizabeth".

From early October, Elizabeth and I were pitching PILL Inc. We were aiming for £125k angel funding from their new incubator. Together with the VC team, and some executive support from PILL Inc, we had been vetted and were on a promising path. 

We navigated initial rounds of due diligence and pushed toward our goals. To formalize the venture, Elizabeth and I founded the company and assigned shares. Things were moving fast; we even brought in her family’s lawyer and accountant for some free support until we got funding.

As a foreigner, it was encouraging to know that the legal aspects of the venture were taken care of by Elizabeth, a British National. So there we were: me the CTO, responsible for product and technical details, and her the CEO, with the network, the business know-how, and the backing of PILL Inc.

I had some doubts in her helpfulness or technical ability to deliver any part of the MVP, but that is the beauty of funding. We were asking for £125k for 10%, and after salaries it should be enough to pay for some consultants on the building and product side. 

### The Strain Begins

3 weeks out from the IC (investment committee), it's getting real.

As PILL Inc was a new incubator, they offloaded most of the due diligence back onto us. Unfortunately, internally our deadlines kept stretching out, and cracks in our workflow began to show. I grew increasingly skeptical about Elizabeth’s contribution, especially when she’d often resort to generating content that was inconsistent or, frankly, untrue. She had a glaring habit of offloading critical thinking to language models, which when you are trying to be concise and convincing in an investment pitch, is a non-starter (at least at the time of writing this).

Simple tasks, like finalizing a slide deck, were marred by her insistence on changing templates or revising facts. 

Over one weekend, I took the initiative to send some slides to the VC team for feedback. Elizabeth erupted when she found out, accusing me of undermining her role as CEO. After a heated one-hour call where I mostly listened, I apologized, suggesting we work together in person to prevent miscommunication. She agreed—until later that night, when she messaged at 11:30 p.m. to cancel tomorrow's work session, citing “more important things.”

### Communication Breakdown

The following Tuesday, we planned to attend an accelerator’s demo day in person. Unfortunately, we had to switch to virtual attendance, as space was limited. I went in person anyway, hoping to make the most of it. They let me in and I spent the day networking, and crafting notes on pitch decks- what works, what doesn't. Exhausted but motivated, I reached out to Elizabeth around 3 p.m., asking if we could finally meet to sync up on the slides. Silence.

By Wednesday morning, I was met with a barrage of texts from Elizabeth, critiquing my work and telling me to refocus on competitor analysis. Our planned in-person meeting was abruptly canceled, and despite my frustration, I continued to try reaching her for clarity. Finally, at 2 p.m., she responded with another request—she needed me to sign documents that evening. Confused, I asked if we could meet to go over the feedback she had on our work.

### We meet

At 5:40 p.m., we met in person at the AI Centre in Holborn. Elizabeth began the conversation by asserting that the intellectual property (IP) was hers and that she’d pursue legal action if I didn’t agree. She then spiraled into a monologue, seeking validation for her “contribution” to the invention. I realized then that she had not only claimed ownership of the idea but was also ready to remove me from the company if I didn’t concede. 

Things were getting messy. 

I was confused. This innovative step, anything remotely patentable in my Thesis, had been developed entirely without her. Instead, I had opted to discuss with a colleague at DeepMind as their research in RL is best-in-class. She had helped me focus on applying RL to buildings, yes, but my research was independent and my development efforts were even more so. 

Against my better judgment, I quizzed her on specifics: What type of reinforcement learning had we implemented? Was it model-free or model-based? She had no answers. It was apparent she’d been preparing for a legal battle rather than working to understand our product's unique selling point (USP). 

I manage to steer the conversation back to action items for the week as we still had the IC pitch coming up, and keep composure the meeting came to an end.

### I take stock

Shaken, I made the march home to Angel with my mind mulling over all our previous interactions throughout the week. I recalled she had for the first time asked me to share the Github repo of my thesis just a few days ago. I thought it strange at the time, but now it made sense. 

I went home and checked Companies House, where the company we founded was listed. There it was! I’d been removed as a company director three days prior, without a single word of notice. This was just a day after she had berated me for supposedly undermining her role as CEO. My head got quite warm, and my brain was having a fight-or-flight response to this news. As this happened I got a text from Elizabeth, the documents were ready to sign- an NDA and IP ownership needed my signature.

I decided to get a second opinion, so I reached out to the VC from PILL Inc, someone who had worked with us directly and had our backs when we were getting started. I wanted to discuss the situation, luckily managing to secure an early morning slot the next day. 

Elizabeth continued texting, insisting I sign the NDA “ASAP.” I sent one text stating that I had received the email, and that I had noticed my removal from the company, asking for clarification from her. She fired off a series of excuses, saying it was sparked from a discussion she had independently with the VC, I needed a different contract, she had only set up the company to get cloud credits, and she suggesting that, as a non-British national, I couldn’t work for the company(not true—I hold a visa). According to her, she was acting in my best interests and I should sign these documents ASAP because the VC team needed them by 8AM sharp. 

She continued texting and attempting to call late into the night.

I was now very thankful I had an opportunity to speak with the VC team myself the following morning.

### Critical team and trust issues

The next morning, after ignoring more calls and texts from Elizabeth, I laid it all out for the VC manager:

- Elizabeth’s sudden IP ownership claims
- My removal from the company on October 27th without notice
- The NDA she sent, demanding immediate signature
- Persistent communication breakdowns and lack of transparency
- An evident deterioration of trust and collaboration

My VC manager responded with empathy. The facts didn't check out from her side- there was no 8AM deadline, no reason to remove me from the company, and the false sense of urgency shed even more light on the situation. 

She suggested I not sign the NDA in its current form and instead gather formal documentation of my contributions. I shared that UCL had previously confirmed my “innovative step” in the project, and I’d developed the code independently. Elizabeth’s sudden request for access to the code further fueled doubts about her understanding of the IP.

The VC manager, however was focused on moving forward. She recommended reviewing our agreements with UCL and PILL Inc regarding student IP and getting clarity on this front.

### I make the call

After the call, I took an hour to reflect. I decided that I wouldn't be signing anything and I couldn’t continue the partnership with Elizabeth. Though I had once been excited to collaborate, this experience revealed an irreversible breach of trust. 

So I called her.

I let Elizabeth know I’d consulted with the VC team and that I would not be signing any documents for a company I was no longer a part of. I also informed her that all future communication should go through email, as I would now be seeking legal advice. 

Her reaction was hostile; she blamed me for “ruining her opportunity” and declared she would move forward on her own. Full stop.

### How to move forward

I've been reflecting on this a lot.

In the words of Steve Jobs on one of the most valuable things he learned at Apple: "I now take a longer term view on people, in other words when I see something not being done right, my first reaction is to not go fix it. It is to say we're building a team here and were gonna do great stuff for the next decade not just the next year and so what do I need to do to help so that the person screwing up learns- veurses, how do I fix the problem."

I shared his opinion going into this project.

At the end of the day, there was a breakdown in communication where Elizabeth didn't feel valued in her contributions to the team. It reached the point where she decided to feel more secure by working with her legal team independently to do everything she could to gain control of the IP and the company.

Even though I feel as though it is partially my fault as I had the say in choosing and sticking with the team. My concerns about the quality of her work or critical thinking did not outweigh my view on her as a colleague and as someone who had a connection to PILL Inc. 

I wanted her on the team to do it simple. I build the product, she manages the funding. The second I realised she wanted more, and she needed the validation, it was too late.

Maybe Steve Jobs did a better job screening candidates and never had to worry about this.

In the short term, I am seeking work in ML/RL engineering in London and clarifying my IP rights. As for Elizabeth, I wish her well but recognize that this experience was a critical lesson in the importance of transparency and trust in any partnership. 

For anyone navigating startup dynamics, remember that IP isn’t just a legal asset—it’s the result of genuine, collaborative work. Trust your instincts, and don’t compromise on transparency, no matter the allure of early-stage funding.

---



This journey has been a whirlwind, but I’m emerging with a clearer vision of my own boundaries and values. Here’s to future ventures, grounded in integrity.

-Nathan