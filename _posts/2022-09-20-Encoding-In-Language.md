---
layout: post
author: Ryan Llamas
summary: How Information Theory plays a large role in NLP and How To Encode Language
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
could be shown too, as he would make many fun contraptions at Bell Labs like juggling 
machines and robotic turtles. But this playful nature did not sidetrack him from
main problems he was aiming to solve. His 
collages referred to him as someone who takes on the hard problems because they were hard
by nature. I think we can all learn a thing from Shannon in the perseverance of seeking knowledge
when the road is wrapped in a veil.

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
surprise of a symbol? With $$ -\log_{2}p(x) $$, we are able to determine how much
surprise we expect for one given symbol with a base 2 with translates to the size of 
a bit (0 or 1). For example, consider a fair coin is flipped. The amount of bits 
represented for heads being up translates as:

$$
-\log_{2}p(1/2) = 1 \text{ bit}
$$

Multiplying $$ p(x) $$ allows us to see the probability of this bit appearing. If we
were to apply this back to the previous example, we would find:

$$
1/2\times-\log_{2}p(1/2) = 1/2
$$

This means heads alone would take up half a bit, such as only being 0 or 1 in this case.
By taking the sum ($$ \sum $$), then we are able to determine the average amount of bits 
for a coin flip, which becomes our entropy value.
Such that:

$$
H(X) = - \sum_{x \in X} p(x) \log_{2}p(x) 
\implies p(1/2)\log_{2}p(1/2)+p(1/2)\log_{2}p(1/2)
\\
\implies \text{Average of 1 Bit for a coin flip}
$$

We can say now an average of 1 bit is expected for a coin flip. This is a telling sign
that there will be little surprise and information when encoding this. As the probability of
a set of outcomes becomes more sparse and even, more information can be expected. Consider
the scenario of a local town having ten events, each having a 10% chance of occurring 
each year. Calculating the entropy for those events yield:

$$
H(X) = - \sum_{x \in X} p(x) \log_{2}p(x)
\implies 10 \times (p(1/10)\log_{2}p(1/10))
\\
\implies \text{Average of 3.321928094887362 Bits for an event}
$$

Considering each event has an equal probability of occurring in great numbers, 
the amount of information expected increases as well! 

Now, how can this be applied to
language? When applied to language, you can determine the amount of information
for a single word or collocation. This also means you can reduce the amount of information
needed to communicate the proper intention. 

For example, lets say I was a explorer and
wanted to let people know what city I am in. There are a tons of cities in the world, 
each with a vibrant name. I could be in Chicago, New York, or Krungthepmahanakhon Amonrattanakosin 
Mahintharayutthaya Mahadilokphop Noppharatratchathaniburirom Udomratchaniwetmahasathan 
Amonphimanawatansathit Sakkathattiyawitsanukamprasit (Yes is a real city name!). 

![city_of_bangkok.png](/assets/post3/city_of_bangkok.png)

<cite>Also referred to as the city of Bangkok!</cite>

But when
I factor in the probability of me being in a city and apply bits in my communication, 
then I can reduce this information
dramatically. Krungthepmahanakhon Amonrattanakosin... (you get the point) now becomes a collection of 0's and
1's to effectively communicate where I am. This could do wonders in saving performance in
systems that handle large amounts of text that have recurring themes. It can also define
the amount of information associated with a city for the given use case, defining the
amount of surprise when a city is listed.

But how is language effectively translated to 0's and 1's? While entropy can certainly
be a useful method to evaluate surprise, it would be hard to ignore just how it is translated
to 0's and 1's. This is where encoding comes into play.

<h3>Encoding and Decoding Information to Bits</h3>

While reading <cite>Foundations of Statistical Natural Language Processing, 
1st Edition</cite>, my eyes were caught by very bottom highlighted section below:

![nlp_page_62.png](/assets/post3/nlp_page_62.png)

"What!? Why wouldn't we explore how these codes are generated!" I exclaimed after
seeing this sentence. This is such a cool tool that can't possibly be ignored, and I
had to explore it. You could say I went on a tangent with information theory and
language, as I was shying away from entropy and digging into encoding algorithms. 

Nonetheless, entropy and the encodings do have some correlation, as mentioned in
the passage shared. When entropy is evaluated, the average amount of bits needed becomes
apparent as well when encoding the symbols. This can be an indicator on how much
information will be generated when compressing this info. 

But what entropy encoding algorithms exist to evaluate these group of bits you may ask? There
exist so many! Here are a few examples:

- Huffman Coding
- Unary Coding
- Arithmetic Coding
- Shannon-Fano Coding
- Elias Gamma Coding
- Tunstall Coding

We haven't even listed them all which is the beauty of these algorithms. Each serve a
distinct purpose and use case all because there is not a one-size fits all solution. 
 Instead,
it is a wealth of tools available for use, and knowing which one to use
is half the battle.

For example, take the difference between Shannon-Fano and Huffman
coding (we will mainly be discussing these two algorithms for now in the duration 
of this post). 
Huffman coding can produce variable length encodings such that a set of codes could be
10, 11, 100 with various bit sizes vs. Shannon Fano coding which produces fixed length encodings such as 100,
110, 111 where the bit size is always three. This can greatly effect the length of your
compression depending on the probability set's distribution. 

The reason these algorithms are so important is that it also provides a method 
of avoiding to space out
our information (hence compression). Let's take the above passage from the book as 
an example:

<center style="font-weight: 900;">1000010101111100010101110</center>

<center style="font-weight: 900;">100  00  101  01  111  100  01  01  01  110</center>

<center style="font-weight: 900;">p  t  k  a  u  p  a  a  a  i</center>

Notice how I am able to decipher this set of bits with minimal interruption (other than
me manually eyeing the key and the code to ensure they are correct
for this example). I am able to parse
through these bits and find a set of symbols simply by looking left to right
with the bit stack and splitting when a set is found in the key. That is the benefit of
these algorithms, the ability to encode the keys without hindering the ability to decode
them. Note however these encodings do not work with the presence of noise in your system, 
such that by inserting an extra bit will still generate a valid code:

<center style="font-weight: 900;">100001010111<div style="font-weight: 900; color: red;display: inline-block;">1</div>1100010101110</center>

<center style="font-weight: 900;">100  00  101  01  11<div style="font-weight: 900; color: red;display: inline-block;">1</div>  110  00  101  01  110</center>

<center style="font-weight: 900;">p  t  k  a  u  a  t  k  a  i</center>

Now that we know how to decode a set of bits, your probably wondering how we go
about encoding it. Both Shannon and Hoffman encoding algorithms relies on 
probability. In particular, the individual probability of symbols in a set. With
the probability of each symbol, we can then build a binary tree that maps out our
bits. But how we go about building that tree is what separates these two algorithms.
Let's start with Shannon Fano encoding and use the example in the passage. The 
pseudocode is defined:

1. Organize the probabilities with its associated symbol in sorted descending order
2. Split the symbols down the middle where each sets total probability is close to
one another.
3. Reference back to the total probability 
value of the original list (Should end up to be 100% for the first time around)
4. Perform Step 2-4 again for each set until you end up with leaf nodes that 
contain one value
5. Assign the least probable references with 0 and most probable references with 1
for the entire tree

Let's see this in action. First, the organized probabilities with its symbol in
descending order:

![shannon_fano_encoding_1.png](/assets/post3/shannon_fano_encoding_1.png)

Now we split the array based on how close the probabilities are to one another. In
this case, we get a nice 50-50 split:

![shannon_fano_encoding_2.png](/assets/post3/shannon_fano_encoding_2.png)

And reference it back to its total probability:

![shannon_fano_encoding_3.png](/assets/post3/shannon_fano_encoding_3.png)

Now perform the same steps with each set. It should look like:

![shannon_fano_encoding_4.png](/assets/post3/shannon_fano_encoding_4.png)

![shannon_fano_encoding_5.png](/assets/post3/shannon_fano_encoding_5.png)

Now that we have leaf nodes with one value/symbol, we can then assign bits based on
its probability:

![shannon_fano_encoding_6.png](/assets/post3/shannon_fano_encoding_6.png)

With this tree, by traveling from the root to the leaf node, I am then able to define 
encodings for each symbol. Take the letter "k" as an example. Traveling down the tree
yields the following encoding:

![shannon_fano_encoding_7.png](/assets/post3/shannon_fano_encoding_7.png)

See how traveling down to each node leads to a new encoding. Starting at the root, I am
able to define a unique encoding that can be used to communicate a message. All the
encodings end up being exactly how we found in the passage:

$$
t = 00
\\
a = 01
\\
p = 100
\\
k = 101
\\
i = 110
\\
u = 111
$$

Now I can effectively communicate a message with minimal loss of information. But maybe
I don't want to use fixed length encoding, but instead, I wish the length to vary in size.
Better yet, maybe I want to have a coded solution on hand. 
This is where Hoffman Encoding comes into play.

<h3>Entropy and Hoffman Encoding Code Challenge</h3>

For this posts coding challenge, I decided to code a solution for Hoffman Encoding
and calculate the entropy value for what is being analyzed. 
This will involve parsing through a text document,
counting words that are to be measured, encoding the given words with Hoffman, and
then calculating the entropy value for the given set.

Before we do that, lets discuss on how Hoffman encoding works. Unlike Shannon-Fano
encoding, Hoffman encoding used variable length encodings. This means the length encodings
can vary in bit size. Such that a high probability symbol may produce "1", but the
lowest probability symbol could expand out to 100101001... Of course, this depends
on just how many symbols you identified in your data set.

The pseudocode for Hoffman Encoding is as follows:

1. Take the two lowest probabilities in your list
2. Reference back these probabilities to a total sum
3. Remove the two lowest probabilities and push the new total sum to the list
4. Perform Steps 1-3 until you end up with one probability value as the root
5. Assign 0 to the left reference and 1 to the right reference

Let's go through an example. Let's say I was analyzing a book to determine what location
is often used in the text. Let's say this book is The Hobbit by J.R.R. Tolkien.
After performing a count, there are 7 distinct locations used:

- <p><div style="font-weight: 900;display: inline-block;">The Shire(TS)</div>: 24%</p>
- <p><div style="font-weight: 900;display: inline-block;">Goblin Town(GT)</div>: 45%</p>
- <p><div style="font-weight: 900;display: inline-block;">Carrock(C)</div>: 14%</p>
- <p><div style="font-weight: 900;display: inline-block;">Beorn's Hall(BH)</div>: 2%</p>
- <p><div style="font-weight: 900;display: inline-block;">Mirkwood(M)</div>: 2%</p>
- <p><div style="font-weight: 900;display: inline-block;">Long Lake(LL)</div>: 9%</p>
- <p><div style="font-weight: 900;display: inline-block;">Desolation of the Dragon(DD)</div>: 4%</p>

(Note: This is very much dummy data and not measured. Although, I am curious to find
a way to measure where someone is in text based on context clues. Something to look into
in the future)

Now, lets put this pseudocode code in action. First, we need our probability list:



TODO Discuss Use Case Scenario for Code

Deciding on what to use as an effective dataset to measure was certainly a challenge.

<h3>Coding Solution</h3>

<h3>Checkpoint</h3>

<h3>References</h3>

<cite>Foundations of Statistical Natural Language Processing, 1st Edition</cite>

[Investopedia Conditional Probability Example](https://www.investopedia.com/terms/c/conditional_probability.asp)

[Conditional Distribution Info](https://corporatefinanceinstitute.com/resources/knowledge/other/conditional-probability/)

[Contributions Made by Claude Shannon](https://www.quantamagazine.org/how-claude-shannons-information-theory-invented-the-future-20201222/)

[Brief Explanation of Claude Shannon's Findings In Communication Theory](https://www.exploratorium.edu/complexity/CompLexicon/Shannon.html)

[Entropy Wikipedia Page](https://en.wikipedia.org/wiki/Entropy_(information_theory))

[Walkthrough on how Entropy Equation if Formed](https://machinelearningmastery.com/what-is-information-entropy/)

[Summery of all Encoding Techniques with Mention of Entropy](https://www.jncet.org/Manuscripts/Volume-6/Issue-5/Vol-6-issue-5-M-02.pdf)

[Encoding Algorithm Walkthrough for Shannon-Fano](https://www.geeksforgeeks.org/shannon-fano-algorithm-for-data-compression/)

[Difference Between Huffman and Shannon-Fano Codings (NOTE: Encoding for Shannon-Fano 
here is wrong due to more bits being produced for a higher probability!)](https://iq.opengenus.org/huffman-coding-vs-fano-shannon-algorithm/)

[Hoffman Encoding Visual Example](https://www.princeton.edu/~cuff/ele201/kulkarni_text/information.pdf)

<cite>Claude Shannon, A mathematical theory of communication, Bell System Technical Journal, Vol. 27, 1948</cite>

More coding references are provided in README.md in git repo [Here]()
