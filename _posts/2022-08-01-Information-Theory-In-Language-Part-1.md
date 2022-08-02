---
layout: post
author: Ryan Llamas
summary: How Information Theory plays a large role in NLP and how Encoding and Decoding Language Findings Work
---

<h1>“Almost every problem that you come across is befuddled with all kinds of 
extraneous data of one sort or another; and if you can bring this problem down into 
the main issues, you can see more clearly what you’re trying to do and perhaps find 
a solution.”
<br />
&#8212; Claude Shannon
</h1>

<h3>Probability In NLP</h3>

By definition, the act of probability is "the extent to which something is probable; 
the likelihood of something happening or being the case." But how does one end up
measuring something that could likely happen. It all starts to man's basic ability, 
counting. The most basic device to see how probability is measured is with a coin. 
Given a coin has heads and tails, you could keep flipping it to find a relatively 
even distribution of heads and tails. You could then make the argument that you have a "fair" coin.

![quarter.png](/assets/post3/quarter.png)

But what about language? Language is after all much more chaotic and free vs. the limitations
of simply flipping a coin. There are more variables to consider, such as how often: a word is
used with another, a word used in a particular section of time or place,
a collocation or phrase is uttered at a given event, etc. The list could go on and on
if you put your mind to it, and you'll find the use case that is aimed to be measured
can yield interesting findings when examining language regarding similar topics.

To draw these associations between one event with another, you need to count distributions
of data and track when one event overlaps with another. For example, lets say I started to
track how often band members are mentioned in two entertainment articles. Let's say the band
is Red Hot Chili Peppers to throw some fun into the problem. In the articles, I find:

**Article#1** mentioned band member:

- Anthony Kiedis 7 times
- Chad Smith 0 times
- John Frusciante 2 times
- Flea (Michael Balzary) 5 times

**Article#2** mentioned band member:

- Anthony Kiedis 4 times
- Chad Smith 1 times
- John Frusciante 0 times
- Flea (Michael Balzary) 7 times

By simply counting the names of these band members in the article, I could then map out
a probability space and find associations between the band members in these two articles. 
In this case, I want to find the probability of finding Anthony Kiedis
if I were to try and find a random band member's name in both articles. 

The probability of me finding Anthony in **Article#1** comes up as $$ \frac{1}{2} $$ while for
**Article#2** I find Anthony $$ \frac{1}{3} $$ of the time. To find the probability of finding Anthony
in both articles out of all names requires us to find the _joint probability_. This is defined as:

$$ p(x, y) = p(x) \times p(y) $$

In our case, finding Anthony in both articles by choosing a random band member name
is:

$$ p(x,y) = \frac{1}{2} \times \frac{1}{3} = \frac{1}{6} $$

(Start then on conditional probability here)

<h3>Information Theory in Language</h3>

<h3>Encoding and Decoding Information to Bits</h3>

<h3>Entropy and Hoffman Encoding Challenge</h3>

<h3>Coding Solution</h3>

<h3>Checkpoint</h3>

<h3>References</h3>

<cite>Foundations of Statistical Natural Language Processing, 1st Edition</cite>

[]()

More coding references are provided in README.md in git repo [Here]()
