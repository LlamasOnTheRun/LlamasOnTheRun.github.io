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

While you could argue that language is something that that can't be
conjured the same way we produce words, through probability, one could measure
relationships of words, sentences, paragraphs, articles, books, etc and aim to get as
close as possible to human speech and measure predictability in a word set.

But how is probability used in language? 
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
can yield interesting findings when examining language.

To draw these associations between one event with another, you need to count distributions
of data and track when one event overlaps with another. For example, lets say I started to
track how often band members are mentioned in two entertainment articles. Let's say the band
is Red Hot Chili Peppers to throw some fun into the problem. 

![red_hot_chili_peppers.png](/assets/post3/red_hot_chili_peppers.png)

In the articles, I find:

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

By simply counting the names of these band members in both articles, I could then map out
a probability space and find associations between the band members. 
In this case, I want to find the probability of finding Anthony Kiedis in both articles
if I were to try and find a random band member's name. 

The probability of me finding Anthony in **Article#1** comes up as $$ \frac{1}{2} $$ while for
**Article#2** I find Anthony $$ \frac{1}{3} $$ of the time. To find the probability of finding Anthony
in both articles out of all names requires us to find the _joint distribution_. This is defined as:

$$ p(x, y) = p(x) \times p(y) $$

In our case, the probability of finding Anthony in both articles by choosing the first random band member name
I find is:

$$ p(\text{Anthony In Article#1, Anthony in Article#2}) = 
\frac{1}{2} \times \frac{1}{3} = \frac{1}{6} = 16.6667\% $$

But let's say I wanted to know the relationship between band members in these articles,
such that I wanted to see **how often** a band member's name occurred **given**
another band member is mentioned. A use case for this is possibly to see how often
a pair of band members is considered a good pair by the media. In this case, 
I would be calculating the _conditional distribution_. This is defined as:

$$ p(x\mid y) = \frac{p(x,y)}{ p_{Y}(y) } $$

Another way of looking at $$ p(x\mid y) $$ is **what is the probability of x given y is
already known**. But wait, what is then $$ p_{Y}(y) $$? This is called the _marginal distribution_.
This is defined as:

$$ p_{Y}(y) = \sum_{x} p(x,y) $$

Think of this as totalling up the probabilities of the event y happening with each event x.
After all, to truly know the relationship of these two values, we have to know how y 
behaves for every instance of x, to truly understand how much of a dependence it has on x.
You could also apply the opposite logic to x with $$ p_{X}(x) $$.

<!--TODO Add equation for marginal distribution here-->

Now, back to our example. One thing to note about conditional distributions, they
work best when a set of events **are neither independent nor mutually exclusive**. I couldn't
for example, try to find the probability of finding Anthony's name in both articles given
I know the probability of finding Flea's name is in both articles. Both are 
independent events because one as no influence over the other, and vice versa. Such
that:

$$ p(\text{Anthony In Article#1&2}\mid \text{Flea In Article#1&2}) 
= p(\text{Anthony In Article#1&2}) $$

$$ p(\text{Flea In Article#1&2}\mid \text{Anthony In Article#1&2}) 
= p(\text{Flea In Article#1&2}) $$

Another puzzling piece, I need to find a way to group these events with a limited subset
of data. I couldn't group it by article because I am currently guaranteed to find
Anthony and Flea mentioned in both articles, such that:

$$ p(\text{Anthony In an Article}\mid \text{Flea In an Article}) = 1 $$

$$ p(\text{Flea In an Article}\mid \text{Anthony In an Article}) = 1 $$

Maybe if I had 100 or 1000 articles, I am bound to find some that mention only Flea and some
that only mention Anthony. But even then, am I truly solving the problem of finding relations
between band members? What if Flea was only mentioned once when Anthony was mentioned
several times in a given article? It wouldn't be fair to say then that the article identifies
Flea and Anthony as having a relation. In this case, it's a matter of grouping your
data in such a way that allows you to still solve the problem. So, lets group the
data from articles to sentences. Such that:

**Article #1&2** sentences with mentioned band member:

- Anthony and Chad mentioned in a sentence: 2
- Anthony and John mentioned in a sentence: 0
- Anthony and Flea mentioned in a sentence: 3
- Chad and John mentioned in a sentence: 0
- Chad and Flea mentioned in a sentence: 0
- John and Flea mentioned in a sentence: 1

Now we're talking. By grouping the data to lower groupings, we can now start to see
relationships form in the text. We could even go further with these groupings by splitting
words into grouping of 5 and counting the times we see these two events. But for the sake of
a simple (as it can be) example, lets see what the conditional distributions are:

$$ = p(\text{Anthony is in the sentence}\mid \text{Flea is in the sentence}) 
\\
\implies\frac{\text{Probability of Anthony and Flea mentioned in a sentence}}
{\text{Marginal Distribution of Flea with each band member}} 
\\
\implies\frac{3}{4} = 75\%
$$

And

$$ = p(\text{Flea is in the sentence}\mid \text{Anthony is in the sentence})
\\
\implies\frac{\text{Probability of Anthony and Flea mentioned in a sentence}}
{\text{Marginal Distribution of Anthony with each band member}}
\\
\implies\frac{3}{5} = 60\%
$$

With this information, I can then say that Flea has a strong dependence with Anthony,
while Anthony can be paired with other band members and still have a relevant presence.
This sort of information can tell a lot given the proper use case, and can even be used
to build complex algorithms to estimate surprise and compress information. This is where
information theory comes into play.

<h3>Information Theory in Language</h3>

Information Theory is the ability to communicate information from one source to another
with minimal interruption and loss of information given noise (the interference between 
the source and destination) 
is present in your process. We can thank the work of Claude Shannon for this field, as
his original paper <cite>A Mathematical Theory of Communication</cite> gave rise to many 
methods of estimation and NLP models that persist to this day. I couldn't help but take time
to read a good portion of this paper, as I wanted to see the root of the foundations that
created an entirely new field during his time.

![claude_the_juggler.png](/assets/post3/claude_the_juggler.png)

<cite>Picture of Claude Shannon Juggling</cite>

Claude Shannon is an individual that couldn't possibly be ignored. He was a student of
MIT contributing to many fields such as Boolean algebra and Cryptography. His playful nature
could be shown too as he would many fun contraptions at Bell Labs like juggling 
machines and robotic turtles. But this playful nature did not sidetrack him from
main problems he was aiming to solve and sharing the knowledge he has gained. His 
collages referred to him as someone who takes on the hard problems because they were hard
by nature. I think we can all learn a thing from Shannon in the perseverance of seeking knowledge
when the road is wrapped in a veil.

- Discuss Claude Shannon's Discovers in paper

But what did Claude Shannon discover in his paper? His findings showed that you could make
a model that could minimize the loss of information and estimate the amount of surprise
for a given set of symbols. He also coined the term "bit" in this paper, as he would
convert his symbols into 0's and 1's based on their predictability. But just how is
the value of surprise defined for a given set of symbols? 
This is through **entropy**, which is defined as:

$$ 
H(X) = - \sum_{x \in X} p(x) \log_{2}p(x)
$$

Shannon defines entropy in the paper as "playing a central role in information theory 
as measures of information, choice, and uncertainty". But how does this evaluate
surprise of a symbol?

- Talk about Entropy and its uses

Information Theory has a role to play when using statistical methods
for a set of events.

- Discuss importance of Shannon's Noisy Channel Model in NLP

<h3>Encoding and Decoding Information to Bits</h3>

<h3>Entropy and Hoffman Encoding Challenge</h3>

<h3>Coding Solution</h3>

<h3>Checkpoint</h3>

<h3>References</h3>

<cite>Foundations of Statistical Natural Language Processing, 1st Edition</cite>

[Investopedia Conditional Probability Example](https://www.investopedia.com/terms/c/conditional_probability.asp)

[Conditional Distribution Info](https://corporatefinanceinstitute.com/resources/knowledge/other/conditional-probability/)

[Contributions Made by Claude Shannon](https://www.quantamagazine.org/how-claude-shannons-information-theory-invented-the-future-20201222/)

[Brief Explanation of Claude Shannon's Findings In Communication Theory](https://www.exploratorium.edu/complexity/CompLexicon/Shannon.html)

<cite>Claude Shannon, A mathematical theory of communication, Bell System Technical Journal, Vol. 27, 1948</cite>

More coding references are provided in README.md in git repo [Here]()
