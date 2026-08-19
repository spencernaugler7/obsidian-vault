---
title: "Recursive Middle Manager Hell"
source: "https://www.lesswrong.com/posts/pHfPvb4JMhGDr4B7n/recursive-middle-manager-hellI"
author:
  - "[[Raemon]]"
published: 2022-12-31
created: 2026-08-19
description: "I think Zvi's Immoral Mazes sequence is really important, but comes with more worldview-assumptions than are necessary to make the points actionable.…"
tags:
  - "clippings"
---
I think Zvi's [Immoral Mazes](https://www.lesswrong.com/sequences/kNANcHLNtJt5qeuSS) sequence is really important, but comes with more worldview-assumptions than are necessary to make the points actionable. I conceptualize Zvi as arguing for multiple hypotheses. In this post I want to articulate one sub-hypothesis, which I call "Recursive Middle Manager Hell". I'm deliberately not covering some other components of his model [^1].

**tl;dr:**

Something weird and kinda horrifying happens when you add layers of middle-management. This has ramifications on when/how to scale organizations, and where you might want to work, and maybe general models of what's going on in the world.

You could summarize the effect as "the org gets more deceptive, less connected to its original goals, more focused on office politics, less able to communicate clearly within itself, and selected for more for sociopathy in upper management."

You might read that list of things and say "sure, seems a bit true", but one of the main points here is "Actually, this happens in a deeper and more insidious way than you're probably realizing, with much higher costs than you're acknowledging. If you're scaling your organization, this should be one of your primary worries."

## The Core Model

Say you have a two-layer company, a CEO and a widgetmaker. The CEO is directly in contact with reality – his company either is profitable or not. He can make choices about high-level-widgetmaking strategy, and see those choices play out in customers that buy his product.

The widgetmaker is also in direct contact with reality – he's got widgets to make. He can see them getting built. He can run into problems with widget-production, see that widgets are no longer getting made, or getting made worse. And then he can fix those problems.

Add one middle manager into the mix.

The middle manager is neither directly involved with widget-production, or the direct consequences of high-level widget strategy. Their feedback loop with reality is weaker. But, they do directly interact with the CEO, and the widgetmakers. So they get exposed to the object level problems of widget-making and company-profit-maximizing.

Hire a lot of widgetmakers, such that you need two middle managers. Now, the middle managers start talking to each other, and forming their own culture.

Scale the company enough that you need two *layers* of middle-managers. Now there's an upper layer who reports to the CEO, but the things they reports about are "what did the lower-middle-managers tell me?". The lower layer talks directly to the widgetmakers, and reports down what they hear about high level strategy from upper management.

Lower middle management wants promotions and raises. Upper management isn't directly involved with the process of widgetmaking, so they only have rough proxies to go on. Management begins constructing a culture about *legible signals of progress,*which begin to get [goodharted in various ways](https://www.lesswrong.com/posts/EbFABnst8LsidYs5Y/goodhart-taxonomy).

Then, scale the company enough that you have *three* layers of middle management.

Now, in the center of the hierarchy are people who *never* talk to someone who's directly engaged with a real-world problem. And there are multiple levels, which create a ladder for career advancement. Middle management culture develops which is *about* career advancement – people rise through the ranks of that culture if they prioritize career advancement as their goal, trading off against other things. Those people end up in charge of how career advancement happens, and they tend to promote people who are like them.

You can fudge numbers to make yourself look good, and because nobody is in direct contact with the reality, it's hard to tell when the numbers are bullshit. It's really hard to evaluate middle managers, and even if you could, evaluation is expensive. If you're the CEO, you have a million other tasks to do and fires to fight. So even if you're trying hard to prevent this from happening, if you're scaling the company, it's likely happening anyway, outside the places you're trying to evaluate.

(Now, imagine that instead of inventing widgets, you're trying to ensure that the EA community has a positive impact, or that AI Alignment gets solved, or some other vague goal with terrible feedback loops instead of physical widgets that clearly either work or don't work, and are either selling or not selling).

See Zvi's [The Road to Mazedom](https://www.lesswrong.com/posts/KLdqetnxgprifo9BP/the-road-to-mazedom) for a more detailed review of what this might look like.

## Examples

Things are only just starting to get weird, but let's pause here for some illustrative anonymized anecdotes:

**1\. Alice, and manager encouraging "legible" achievements.**

A friend of mine ("Alice") worked at Google. In a meeting with her manager, he said "This new project you're working on will be good for you. It's very concrete and will look good for your career." He was treating this as a favor he was offering her, that he expected her to appreciate. He thought part of his job was helping his employees advance. And, notably, there wasn't any focus on "and this project is actually valuable, or the research is actually interesting." The focus was on legible currency.

Alice felt like whole company seemed to be pressuring her into becoming the sort of person who cared about those legible achievements.

**2\. Beth, and managers outright lying.**

Another friend ("Beth") worked at 500-ish employee company. Once, she had a good manager ("Bob") who had a clear understanding of strategy, cared about the product and the company vision, etc. Then, he got promoted, and she got a new manager ("Barnum") who was clearly a careerist. Barnum would *actively distort* the numbers about how their team was doing, framing things misleading and sometimes actively lying.

Beth tried to bring this up in her periodic skip-level meetings with original manager Bob. But it was awkward to say explicitly "Yo, my manager seems to be outright lying sometimes?" – it'll likely become a protracted conflict that made her life much worse. I don't remember the exact details of how this played out but I think she waited months to bring it up, brought it up sort of gingerly at first, and even when she was more concrete, Bob was basically too busy to take action on it.

**3\. Charlie, and** ***more*** **managers being deceptive.**

I know of an EA-org that once hired a mid-level person ("Charlie") to manage office stuff, who I ended up collaborating with on joint-projects sometimes. Occasionally there'd be a logistical problem we were running into, that I'd want to talk about in the general project slack-channel. Charlie would message me in DMs asking to not talk about it public channels, because it'd look bad to Charlie's higher-level manager that we weren't on top of things.

Some other colleagues and I had similar experiences with Charlie. Eventually someone talked to Charlie's managers about it. Eventually, several months later, they let Charlie go. But the whole thing took several months to play out.

Note that both this and the previous anecdote involve "It's pretty effortful to deal with conflict in an org, which means cultural problems can sit around, unsolved, for a long while." If you're scaling fast, and it takes you 5 months to resolve a problem (either by firing someone, or iterating on intense feedback and figuring out how to resolve it), and there are multiple such problems, they might create bad cultural effects that propagate faster than you can deal with them.

**4\. David, and a culture of not-especially-truthseeking**

David was an AI alignment researcher. After getting used to "rationalist" culture where it's highly encouraged to ask people to be more specific, or ask questions like "why do you believe that?", they joined a new org where that came across as kinda aggressive. It was hard to get clarity on what people were actually talking about, and figure out when their ideas made sense or not.

There was also a general sense that workplace conversations had more of an undercurrent of "we're playing some kind of status game", and they felt more need to be strategic about what they said.

I don't think this was necessarily a middle-management driven problem – this is just how a lot of human cultures are, by default. But I bring it up here to highlight the *base* level of obfuscation you can expect in an organizational culture, before middle management goodharting starts to warp it further.

**5\. Me, and organizational spaghetti code**

When I worked at Spotify, I was hired to help build a tool to automate the process wherein new employees got all the correct permissions, software, hardware, and other onboarding. There were finicky details that made this hard – it never quite reached a point where it worked 100% reliably enough that the IT department could switch to using it without checking everything by hand.

Meanwhile, in another Spotify office, *another* IT department was working an a project that was trying to solve a different problem, but also needed to control whether employees had the correct permissions for our Enterprise Google Drive setup, which was kinda redundant.

Both of us had incentive to grow our project over time to encompass more things. i.e. once you'd built a bunch of basic infrastructure, it felt kinda silly not to use it to solve more problems that benefited from a single source of truth.

*Also* if we grew the scope of our respective projects, we each looked/felt more important, and got to claim more credit for a bigger company impact.

Eventually we both bumped into each other and noticed we were doing duplicate work, and were faced with some options:

- Just do the duplicate work
- Try to merge our projects
- Have one of us stop our project

And, like, guys I'm a rationalist and I try to be a good, practical person. But it was amazing a) how triggered I felt about the other guy who was 'enroaching on my turf', b) how easily justifications came to me that my project should be the one to survive and was better than his, and why *my* excuses for why it was taking forever were more justifiable than *his* excuses for why his was taking forever.

I think we both went on building our tools for another year, and somehow they never quite reached fruition.

## Deepening over time

So, to recap here, we have a few things happening:

- Managers are hard to evaluate.
- Managers are comparatively incentivized to spend much of their time thinking about the social/political world of the internal company.
- If you have hierarchy in a company, regardless of whether people are "middle managers" per se, there's a tendency for people to come to care about advancing in the hierarchy. It's a natural thing to want to do.
- Most people aren't doing that good a job tracking reality or having coherent goals in the first place.
- Managers start to goodhart on their objectives – some by accident, some deceiving themselves, some actively lying.
- Managers who prioritize advancing in the company tend to get promoted, and then hire more people like themselves – people who are either willing to lie, or are likely to self-deceive into confusedly goodharting.

On top of all that, we have the usual run-of-the-mill "Principal-Agent problems", where it's hard to hire someone to go off and strategically do complicated stuff on your behalf.

The Recursive Middle Manager Hell hypothesis doesn't merely say "hire too many middle managers and your company starts to goodhart/lose-purpose/become-deceptive." It *starts* with that, but then the problem doubles in on itself, recursively creating a company where these problems compound, worse than the sum of their parts.

The second generation of the company is built on a culture where "advance in the hierarchy" (rather than focus on the "core goals of the company") is implicitly the main thing to be doing. "Do stuff that seems legibly valuable" becomes the main currency, rather than "do stuff that is *actually* valuable." (And where "begin to goodhart, confusing yourself about whether you're actually doing something valuable" begins becoming an implicit part of the culture).

The third generation takes it a step further. Now that "Do stuff that is legibly good" is the story people are explicitly telling each other, it becomes the substrate of a culture where " *pretend* to do stuff that is legibly good" is what people are actually doing. Eventually, many people pick up on the fact that "pretend to do legible good" is the real game, and they start making choices that assume other managers are also pretending.

And finally you might reach a generation where "pretend to produce legible good" is just a piece in a game that is essentially disconnected from reality. People don't even think of it as "pretending" anymore, it's just what people in-the-know do. The upper management who control most of the company structure build an ecosystem based around loyalty and trading favors, but which uses "make powerpoints describing the results of your projects" as a sort of token to be manipulated. The company continues to produce value incidentally through inertia, but it's now much harder to steer, and there is a lot of inefficiency and waste. If the world changes significantly it'll have a harder time pivoting. If it does successfully pivot, it'll probably be executed through a small department that works more independently, in spite of company culture.

In practice these generations don't come in discrete stages. But I find it helpful for thinking about how generations of company hiring and cultural accumulation might layer on top of each other. (Side note: these stages roughly correspond to the levels in Baudrillard's [Simulacra and Subjectivity](https://www.lesswrong.com/posts/fEX7G2N7CtmZQ3eB5/simulacra-and-subjectivity), which some have found useful for modeling how language is used. See [Simulacra Levels and their Interactions](https://www.lesswrong.com/posts/qDmnyEMtJkE9Wrpau/simulacra-levels-and-their-interactions) and [Simulacrum 3 As Stag-Hunt Strategy](https://www.lesswrong.com/posts/tF8z9HBoBn783Cirz/simulacrum-3-as-stag-hunt-strategy) for further detail)

I'll flag that each generation here is essentially an additional sub-hypothesis, which you can accept or reject independently. I personally think it's pretty likely that all four layers happen at least sometimes. I also think, whether or not the generations progress in the same way, the notion that a company culture will undergo *some* kind of phases, where each generation of hiring attracts and builds on the culture that the previous generation established (and gets harder to steer), seems likely true, independent of exactly how it plays out.

**Hard to reverse, and hard to talk about**

Zvi calls the progress down this path "raising maze levels", inspired by the book Moral Mazes, which explores a few case studies of companies with many layers of middle management, where these pathologies got very extreme.

Say you're a CEO, or otherwise in company leadership trying to ensure your company can communicate clearly, focus on producing object-level value, etc. It's much easier to *stop* the culture from progressing down this path, than to reverse the culture once it's taken root. This is for a few reasons:

1. The more people are at your company, the more people you either have to change the behavior of, or fire/replace. So more people straightforwardly equals "more work."
2. If upper management is actively benefiting from the new culture and in fact helped create it, then you don't just have to do the linear work of changing habits or firing people. You need to fight an entrenched power structure that will actively oppose you.
3. By default, people are just pretty crap at telling the difference between "actually working on a problem for real" and "confabulating reasons why their pretend work is useful." They may literally not know the difference. So if you talk to people about how you need to fix the company culture, and not exaggerate/lie/goodhart on objectives, they may nod sagely... and then go back to doing pretty much what they were doing before, and not notice the difference.
4. Once the maze culture takes root, people become *even more* crap at noticing when they're confabulating, deceiving or goodharting. They're incentivized not to notice, they're incentivized not to care if they do, and they're incentivized to look the other way if others are.
5. The entrenched power structures that benefit from higher maze levels will take advantage of #3 and #4, equivocating between different claims in a way that is plausibly deniable and hard to pin down.

## Implications for EA and AI

There are many more details here, but I want to keep this reasonably short while emphasizing my key takeaways.

I think it is sometimes appropriate to build large organizations, when you're trying to do a reasonably simple thing at scale.

I think most effective altruist and AI alignment organizations cannot afford to become mazes. Our key value propositions are navigating a confusing world where we don't really know what to do, and our feedback loops are incredibly poor. We're not sure what counts as alignment progress, many things that *might* help with alignment also help with AI capabilities and push us closer to either hard takeoff or a slow rolling unstoppable apocalypse.

Each stage of organizational growth triggers a bit less contact with reality, a bit more incentive to frame things so they look good.

I keep talking to people who think "Obviously, the thing we need to do is hire more. We're struggling to get stuff done, we need more people." And yes, you are struggling to get stuff done. But I think growing your org will diminish your ability to *think*, which is one of your rarest and most precious resources.

Look at the 5 example anecdotes I give, and imagine what happens, not when they are happening individually, but *all at once*, reinforcing each other. When managers are encouraging their researchers to think in terms of legible accomplishments. When managers are encouraging their researchers or programmers to lie. When projects acquire inertia and never stop even if they're pointless, or actively harmful – because they look good and even a dedicated rationalist feels immense pressure to make up reasons his project is worthwhile.

Imagine if my silly IT project had been a tool or research program that turned out to be AI capabilities accelerating, and then the entire company culture converged to make that difficult to stop, or talk plainly about, or even avoid actively lying about it.

What exactly do we do about this is a bigger post. But for now: If your instinct is to *grow –* grow your org, or grow the effective altruism or AI safety network, think seriously about the costs of scale.

I recommend Zvi's [Protecting Large Projects Against Mazedom](https://www.lesswrong.com/posts/4inoCWnKrpHt4gCx9/protecting-large-projects-against-mazedom) for concrete advice here. (In general I recommend reading the whole sequence, although it starts off a couple posts that make less obvious claims about superperfect competition, which I'm less confident in and don't think it is necessary to get the rest of the model)

I'll end by summarizing the highlights from Protecting Large Projects:

1. [Do less things and be smaller](https://www.lesswrong.com/s/kNANcHLNtJt5qeuSS/p/4inoCWnKrpHt4gCx9#Solution_1__Do_Less_Things_and_Be_Smaller)
2. [Minimize levels of hierarchy](https://www.lesswrong.com/s/kNANcHLNtJt5qeuSS/p/4inoCWnKrpHt4gCx9#Solution_2__Minimize_Levels_of_Hierarchy)
3. [Skin in the game](https://www.lesswrong.com/s/kNANcHLNtJt5qeuSS/p/4inoCWnKrpHt4gCx9#Solution_2__Minimize_Levels_of_Hierarchy)
4. [Soul in the game](https://www.lesswrong.com/s/kNANcHLNtJt5qeuSS/p/4inoCWnKrpHt4gCx9#Solution_2__Minimize_Levels_of_Hierarchy)
5. [Hire and Fire Carefully](https://www.lesswrong.com/s/kNANcHLNtJt5qeuSS/p/4inoCWnKrpHt4gCx9#Solution_5__Hire_and_Fire_Carefully)
6. [Promote, Reward and Evaluate Carefully](https://www.lesswrong.com/s/kNANcHLNtJt5qeuSS/p/4inoCWnKrpHt4gCx9#Solution_6__Promote__Reward_and_Evaluate_Carefully)
7. [Fight for Culture](https://www.lesswrong.com/s/kNANcHLNtJt5qeuSS/p/4inoCWnKrpHt4gCx9#Solution_7__Fight_for_Culture)
8. [Avoid Other Mazes](https://www.lesswrong.com/s/kNANcHLNtJt5qeuSS/p/4inoCWnKrpHt4gCx9#Solution_8__Avoid_Other_Mazes)
9. [If necessary, Start Again](https://www.lesswrong.com/s/kNANcHLNtJt5qeuSS/p/4inoCWnKrpHt4gCx9#Solution_9__Start_Again)

## Future work?

A thing on my mind is, I expect a lot of people to have taken at least a brief look at these arguments, and been like "I dunno, maybe, but scaling organizations still seems really useful/important, and I don't know that I buy the effects here are strong enough to outweigh that."

And... that's super fair! The arguments here are pretty abstract and handwavy. I think the arguments here are good enough to promote this as a serious hypothesis. But I think it's kinda reasonable for most people's actual guesses about the world to be informed more by their broader experience of what orgs tend to be like.

I think it'd be fair ask "okay, cool, but can you go do some real empirical work here to see how reliably Moral Maze problems tend to come up, and how strong the effect size is?". I think this is maybe a thing worth putting some serious research time on. But, in order for that to be useful, there needs to be a real person with some real cruxes, and the data-gathering needs to actually address those cruxes.

So, if you are someone running a company, or hiring, and you could be persuaded of the Recursive Middle Manager Hell Hypotheses but want to see some kind of data... I'm interested in what sort of evidence you'd actually find compelling.

[^1]: Zvi had at few more major components/hypotheses in his Immoral Maze models, not covered here, which include:

- "superperfect competition and the elimination of slack"
- "moral mazes being particularly soulsucking and destructive of human value"
- "motive ambiguity as a tool for upper management to test loyalty."

I found them all at least somewhat plausible, but harder to argue for, and wanted to keep the post short.

[^2]: "superperfect competition and the elimination of slack"

[^3]: "moral mazes being particularly soulsucking and destructive of human value"

[^4]: "motive ambiguity as a tool for upper management to test loyalty."