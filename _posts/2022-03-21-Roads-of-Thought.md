---
layout: post
author: Ryan Llamas
summary: Our first topic discusses strategies a NLP practitioner may take when building solutions. Also, will look at an implementation for Context Free Grammars using Python Package NLTK to make a Yoda Text Generator.
---

<h1>“Language is the most massive and inclusive art we know, a mountainous and anonymous work of unconscious generations.”

&#8212; Edward Sapir
</h1>

<h3>The Foundation I Take Notes From</h3>

As I was reading Foundations of Statistical Natural Language Processing, I couldn’t help but stop to look up each individual 
who made a major contribution to the field of NLP. Learning about these individuals and understanding their givings to 
the field taught me much about how our current NLP algorithms and structures came to fruition.

For example, learning about Ludwig Wittgenstein's idea of the use of a word in everyday life playing a role in language. 
Or Edward Sapir’s contributions to the study Native American language, finding how cultural patterns shape a society and language. 
It is all too fascinating to ignore!

![NLP Contributors](/assets/post2/nlp_contributors.PNG)

At the beginning of the book, the main person it likes to point out is Noam Chomsky and his ideas. He contributed to NLP 
by creating a method to say whether a sentence is a “grammatical” or an “ungrammatical” one using a defined rule set purposed 
for the English language. He also believed everyone internally has a common set of rules for language and goes about proving 
these ideas showing how similar different languages are.

Funny enough, the book seems to argue against these ideas and models when it comes to crafting meaningful sentences and 
building practical applications. After all, it makes sense for a book focused on the statistics of NLP rather than the 
groupings of words and their pairings. It begs for opinionated structure and meaning, and Noam Chomskey offers quite the opposite.

The points presented are fair when it comes to making sentences of note rather than ambiguity. For example, Noam Chomsky 
believes the sentence “Colorless green ideas sleep furiously” is a grammatically correct sentence, but in truth, doesn’t 
seem practical in reality. With this, we travel into the approaches a NLP researcher takes.

<h3>Two Roads of Thought</h3>

The book argues there are two roads of thought when approaching a NLP problem. One approach is the Rationalist approach, 
where certain knowledge of a language's structure is innate, even coining the term people have an innate language faculty. 
Noam Chomsky is a strong supporter of this approach, stating if an advanced alien martian were to arrive at earth, he would 
deduce there is only one language with local variants depending where you are. 

Then there is the Empiricist approach, by applying a language model/structure, then analyzing it with statistical methods 
to influence its output. This approach does not support the idea that there is an declared set of rules, but language itself 
adapts based on its present use.

![NLP Contributors](/assets/post2/rationalist_vs_empiricist.png)

You can see how Chomskey’s ideas sponsor the categorical approach of saying there are grammatical and ungrammatical sentences 
due to the declared definitive structure rationalists apply to language. However, Empiricists do not accept the notion of 
whether a sentence is grammatical, but that its use is clearly expressed in a meaningful way.

For example, take a look at a Rationalist approach for crafting grammatical sentences. The below diagram used a Context 
Free Grammar approach (CFG for short) to craft grammatical sentences. Using a set of lexical rules, it defines what types of 
words go with its Part of Speech, such as a “Determiner” with a “Noun” is considered a “NP”. You can see how static this makes 
sentence generation and how it can end up making cryptic sentences. We will dig into this more later…

![NLP Contributors](/assets/post2/CFG_with_NLP_example.png)

<h3>Are These Two Mindsets Widely and Only Accepted Today</h3>

Here is the point where I believe we dive into opinion, as no clear answer could be produced after looking into this delicate 
question. The Empirest approach declares the answer is in the data while the Rationalist approach says the answer is universally 
defined in nature. But my belief is there are not only two practical approaches, and one should explore the possibility of combining 
these approaches to produce more fantastic methods and results for future NLP problems.

To look into this question, I was heavily influenced by Kenneth Church and Mark Liberman’s latest paper The Future of Computational 
Linguistics: On Beyond Alchemy. The paper points out other approaches as well such as Associationism (the frequency of X and 
Y will influence the use of X and Y more in the future) and Connectionism (the modeling of neural networks to produce intellectual 
responses) and points out how approaches rise and fall based on the latest discoveries/leaders in the industry. If one were to 
see the connections that could be drawn between these approaches, I truly believe there are hidden developments waiting to be discovered.

They also reinforce the idea that young researchers who rebel against the precedent to find new practices are the future 
for the industry, but recognize the risks associated with it can lead to pure rejection and wasted time. I feel the risk is 
worth the benefit, as NLP solutions are becoming more and more involved such as achievements like Amazon's Alexa. It is why I 
am so bold to say there must be more than meets the eye.

<h3>Context Free Grammar Challenge</h3>

To show the power of a CFG, I decided to make one using a set of sentences. To further challenge myself, I wanted to make it 
into the Chomsky Normal Form considering we brought up Noam Chomsky’s idea of a “grammatical” sentence. A grammar is considered 
in Chomsky Normal Form if it follows a certain set of rules:

![NLP Contributors](/assets/post2/chomsky_normal_form_rules.png)

What do these symbols mean? Great question, let's break it down. Every grammar must have a starting point to generate a 
sentence. This is what “S” is, our Starting Point. “S” will need to know its options for generating a sentence, so it is 
made up of Nonterminals, aka “A” and “B”. The rule “A->BC” is called a Production, defining what a nonterminal is able to 
produce using other nonterminals. Then there is “a” which is considered a terminal. Terminals in our case are the words we 
will use in a sentence. For example, the word “the” is considered a terminal. The epsilon symbol refers to the fact that S 
(and only S) can produce an empty string if it chooses. As long as your grammar satisfies these rules, it is considered in 
Chomsky Normal Form.

So why are CFGs so powerful and what does having it in Chomsky Normal Form achieve? A CFG without the rule set of Chomsky 
Normal Form can be powerful alone as it can parse and map a set of terminals for computation purposes. Consider the equation 
(2+3)+5: knowing the answer is ten is simple for the human mind, but for a machine, a CFG is essential. This allows the analysis 
of PEMDAS operation rules for more complex equations. See how this maps in a CFG:

![NLP Contributors](/assets/post2/CFG_without_chomsky_example.png)

Note that given a more complex equation, a CFG could be mapped in many different ways. The same thing goes for language as well.

Now what makes Chomsky Normal Form so attractive when making your CFG? It is due to its simplicity of rules to be met, 
attractive existing algorithms such as CYK to identify if a sentence can be made into Chomsky Normal Form in a reasonable time, 
and the multitude of proofs and analysis made with the given rule set. For example, let’s say we have the sentence “Welcome to my home.” 
I can identify that I have five values in this sentence (including the period) and can say if I had a CFG that parsed this 
sentence, I would end up with 9 production rules (A->BC). Later on, you will see how I came to this conclusion, but this 
is one of the few examples on how CFGs are useful in defining computation expectation.

Now, to add some humor to the problem and solution. Considering CFGs often create sentences that provide little meaning 
or seem metaphorical in nature, I decided to use sentences only Yoda from Star Wars would use. It seems appropriate considering 
if you were to try to understand a sentence produced by a CFG, it would come off as a riddle. Hence, I will try to craft a 
yoda test generator using a generated CFG.

![NLP Contributors](/assets/post2/yoda.png){: width="250" }

<cite>“He once said to me, "Size matters not." That's how he talked. He would speak in riddles.” - Luke Skywalker </cite>

<h3>Coding Solution</h3>

I decided to solve this problem in Python using the NLTK package, a popular package for NLP solutions. First, we will need 
data to analyze and feed to our CFG. Scouring the internet, I found a array on github of Yoda sentences to use, and added 
additional ones to cover some edge cases:

![NLP Contributors](/assets/post2/yoda_sentences.png)

One of the few challenges of generating a CFG with a random set of sentences is:
1. Making sure to keep track of all its components, in this case, its nonterminals, productions, and starting points
2. Defining a Algorithm to parse a sentence and create new unique productions
3. Ensuring you have a way to parse a sentence and end up with the same “S”

While there are algorithms to modify an existing CFG to Chomsky Normal Form, it gets more complicated to generate a CFG 
from the ground up while ensuring it meets its rules and satisfies all previous sentences. After googling and realizing there 
is no defined algorithm for this task, I decided to create my own. It follows four steps: Find the POS of a sentence, see if 
it covers existing production rules and “mutate” it, parse the “mutated” sentence with newly created production rules, rinse and
repeat. Lets see this in code:

![NLP Contributors](/assets/post2/main_method.png)

1. I keep track of five things in the overall program. Will go into detail for each later
2. Method that returns the Part of Speech(POS) for a sentence
3. Method that returns POS in a modified array with existing productions
4. Method that determines if a S was found as a leaf of a sentence
5. Parses the POS with possible mutations and creates new production rules with a new “S”
6. Clears the POS for the sentence and starts again

Finding this method of approach required some research into existing algorithms to see what I could modify them to fit my use case. 
I used a combination of steps as reference from converting CFG to Chomsky Normal Form algorithm to CYK algorithm. I even performed 
it by hand for a few sentences to ensure it was a feasible approach.

However, it looks simple from this viewpoint, but let’s take a closer look at each method, starting with how I get the POS:

![NLP Contributors](/assets/post2/get_POS_method.png)

1. I track overallProductionsFound and the sentences POS in temp
2. for loop with iterate on each word in the sentence getting its POS
3. Append the POS for the word in temp
4. Create a Production that maps a Nonterminal, in this case the POS, to its given word
5. Will add the Production rule only if it does not already exist in overallProductionsFound

You can see how this method begins to add our initial production rules. In this case, it satisfies the condition A -> a 
if we were to look back on Chomsky Normal Form’s conditions. Lets see how this prints in terminal:

![NLP Contributors](/assets/post2/POS_terminal_output.png)

NLTK is doing its job well providing us the POS for each word in the sentence. In this case:
- The maps to DT which is a determiner
- Different maps to JJ which is a adjective
- I maps to PRP which is a personal pronoun
- Finally the period

This is NLTK tools at work, with tools like word_tokenize() to split the sentence in an array of words/punctuation and pos_tag() 
to determine the POS for each word in the array. We also see the first use of classes Nonterminal and Production, as a production 
is mapped out as A->a or DT->”the”.

Now that we have our POS for the sentence and the initial production rules, we can start parsing this array and create our 
production rules satisfying the condition A -> BC. However, we wouldn’t want to create duplicate productions while parsing 
this array. Hence, we will now mutate this array to match existing production rules:

![NLP Contributors](/assets/post2/mutate_method.png)

1. I keep track if I foundExistingProductions while parsing (Ignore overallStartingNonTerminals as this was a typo)
2. A conditional to find out if we have production rules defined
3. Loop until the index is at the last element of initialNonTerminals
4. Define what is the lhs (Left Hand Side) and rhs (Right Hand Side) of using the current index
5. Loop through every production rule to check if its production.rhs() is equal to the nonterminals we defined in step 4
6. If we found a match: remove both nonterminals with pop() and replace it with production.lhs()
7. Mark that we have found an existing production rule with foundExistingProduction. Also break out of loop because a found production rule should be one of a kind, therefore we won’t find another
8. Move the index over two in index-=2
9. This step is very similar to steps 7 and 8, only difference is we define the lhs and rhs differently to not go over index bound
10. If foundExistingProduction is true, then perform a recursion until we find find no existing production rules

This parsing algorithm was actually defined after I made the algorithm for performRightToLeftProductionCreation(). I realized 
after its creation that I needed to find a way to modify sentences with existing rules to avoid recreating them. I also 
found that if I have a sentence T and a start S: if S->T, then I should have a way to map T->S.

Hence, mutateListWithAlreadyDeclaredProductions() was made to satisfy this need. Consider the sentence “Agree with you, 
the council does.” Let’s say I had the array with two copies of this sentence. I should expect this sentence to map back 
to the same S. Lets see this in action:

![NLP Contributors](/assets/post2/POS_terminal_output.png)

Notice that no new S was added to “Our new starting nonterminals” after coming across the same sentence twice. This is 
mutateListWithAlreadyDeclaredProductions() at work, making sure we map back to our same S, in this case, production rule ”11”.

Now that our mutated sentence is doing its job, we have to consider an edge case. Consider if a subset of S was found to 
be a leaf of a tree. Consider the following graph:

![NLP Contributors](/assets/post2/start_and_leaf_case.png)

If S->2, and 2 was found to be later used in another production set, I would need to keep track of this to avoid overwriting 
it when updating these production rules to S later on.

Hence, determineNonterminalsThatIsChildAndStart() was created to find these. It makes it convenient to do it after 
mutateListWithAlreadyDeclaredProductions() as well, considering if a subset of S was found in this updated array, then 
it will end up being a nonterminal anyway. Here is the code used to accomplish this:

![NLP Contributors](/assets/post2/child_and_start_method.png)

1. I keep track of overallProductionsFound and overallStartingNonTerminals
2. Check if an existing S has been found, for it can’t be a leaf then
3. Will loop through mutatedNonTerminals and overallStartingNonTerminals till it finds a unique match
4. If the conditions are met, add this nonterminal to overallStartingAndLeafNonTerminals and remove it from overallStartingNonTerminals

This scenario is very rare in a small subset of data, but given a large corpus and examining its sentences, overallStartingAndLeafNonTerminals 
could end up being larger. Lets see this method in action when a subset of S is used in a sentence:

![NLP Contributors](/assets/post2/leaf_terminal_output.png)

Here we can see the sentence “No different I.” used, but then “Yes, No Different I.” is checked using a nonterminal identified 
as a S candidate. Consider this visual representation:

2->“No different I.”
Other Production Rules for Sentence…

and

4->”Yes, No Different I.”
4->UH 3
3->, 2
Other Production Rules for Sentence…

When production rule two is used as a subset of S, we will keep track of this, and print it with the statement “Starting and 
Leaf nonterminals: [2]”. We will eventually use this array later on when defining our S candidates, but this is an edge 
case to be made aware of.

Now that we are parsing a sentence with existing production rules and covering its edge cases, it's time to map out new 
production rules all the way to a new S. This is what performRightToLeftProductionCreation() aims to accomplish. You’ll 
find that this method is rather similar in pattern to mutateListWithAlreadyDeclaredProductions(). This is something I wish 
to refactor it in future, as I can merge the two to accomplish both tasks based on a boolean flag. Regardless, let’s see 
this algorithm in action:

![NLP Contributors](/assets/post2/left_to_right_method.png)

1. I keep track a rollingID I increment for each new production rule, overallProductionsFound, and overallStartingNonTerminals
2. Begin the index at the last element and create a array called newNonTerminals to track new productions created from unfoundNonTerminals
3. Loops until the index arrives at the last element. Each iteration will define a new Production rule using its lhs and rhs
4. After creating this new Production rule, I track it in overallProductionsFound and take note of the newNonTerminals
5. Account for the case where we reach the end of our array to define a new Production rule as I have to look at previous rule created
6. If we haven’t found our new S, perform a recursion on the method until we end up with one element in newNonTerminals, else add our new S in overallStartingNonTerminals

This is the final step of our process to take care of creating new production rules and also defining new S candidates.

You can imagine after 20 sentences, the amount of interactions/iterations with elements can be quite large. Not to mention, 
the amount of production rules produced. In fact, we can go ahead and calculate it. Considering there are 10 words in a sentence, 
we end up finding/creating 19 production rules for a given sentence. If N were the amount of words in a sentence, the amount of 
production rules found/produced is 2N-1. This equation is what makes the Chomsky Normal Form so valuable, due to the ability to 
calculate expectations with a defined rule set. Lets see what out final output is after twenty sentences:

![NLP Contributors](/assets/post2/production_rules_output.png)

Wow, this is a lot of production rules! Not to mention, a lot of starting nonterminals identified! I’m sure if we mapped
this entire set into a visible tree, we would not only have a huge tree to look at, but be able to reproduce all sentences 
found in our array by starting with a S!

At this point, I wanted to play around with my new CFG and generate some random sentences. But before I do this, I have to 
define which production rules make up S, use NLTK CFG class to map these rules for further tool use, and then finally generate 
some random yoda sentences! Lets see this final piece in action:

![NLP Contributors](/assets/post2/final_print_method.png)

1. Replace Production elements with a lhs() that is mapped to what we found to be S in overallStartingNonTerminals
2. Append Production elements for S values that are in overallStartingAndLeafNonTerminals (Keeps original S rule intact)
3. Use NLTK CFG class to have a central class that stores our rules
4. Print one-liner print statements for N sentences to demonstrate how sentences are being mapped in our CFG using parser.parse()
5. Commented out for a reason. This two line statement used NLTK tool generate() to craft random sentences based on our CFG

Steps one and two were certainly mistakes made when looking at constructing a CFG class. I assumed CFG constructor needed 
an array of starting Nonterminal(s), but it turns out it needed one as an identifier. Hence, I went ahead and added the 
S in overallProductionsFound through a looping mechanism. I could have added this as a step in previous methods, but avoided 
it to maintain working changes (This is why Test Driven Development is important as it helps drive and maintain your design! I 
intended to add tests before making a solution, but my Hackathon instincts kicked in. Will be more careful next time.)

Lets see how step four displays our sentences being mapped out by our CFG:

![NLP Contributors](/assets/post2/tree_print_terminal_output.png)

So what are we looking at here? Let's take the sentence “I sense much fear in you.” as an example. It maps out as:
[Tree('S', [Tree('55', [Tree('PRP', ['I']), Tree('VBP', ['sense'])]), Tree('56', [Tree('54', [Tree('JJ', ['much']), Tree('NN', ['fear'])]), 
Tree('53', [Tree('IN', ['in']), Tree('0', [Tree('PRP', ['you']), Tree('.', ['.'])])])])])]

Remember, S is the starting nonterminal and will be mapped out by a set of productions. Here S, envelopes the entire sentence, 
and its production rules eventually map out to its terminals. Lets translate the above now to a diagram:

![NLP Contributors](/assets/post2/sentence_tree_example_visual.png)

That’s right, if we were to perform a Breadth-First search algorithm with this tree, we would be able to reproduce our sentence. 
Notice that the algorithm does its best to evenly distribute productions on the left and right side of S. This is why I 
parsed and produced new Production(s) with a skip over of two elements. I wanted a tree that wasn’t too left oriented nor 
right oriented. Instead, I wanted to make sentences as evenly distributed as possible within the confines of my existing rules.

Now that we know our sentences are being parsed back properly (remember S->T and T->S), let's start generating sentences. 
NLTK provides the tools to generate sentences with your CFG given you provided terminal values or “A->a”. I did some research 
on how to provide random words vs what I provided in a given sentence, but couldn’t come to a reasonable solution (Maybe something 
to explore in the future!) Lets see how step five generates a huge list of random sentences:

![NLP Contributors](/assets/post2/text_from_CFG_output.png)

I had to wrap my generate() loop with a modulus of million to get a clean output as it would generate a multitude of sentences. 
The above shows the structure of the sentence “Always two there are, no more, no less: a master and an apprentice.” often with 
variations often made to the right side. This is due to the multitude of options available within the sentence as we have made 
available multiple terminals/words with multiple POS to cover. The method generate() alone would try to generate every possible 
combination, creating an observable infinite reproduction of sentences.

Not only that, but we can clearly see that these sentences do not make much sense. They truly are riddles, which fits 
the persona of Yoda in the end. If we wanted to see sentences that have more weight and meaning, we would have to dive into 
the statistics of a probable CFG for each route available (Something to explore later on!).

Regardless, we can clearly see the value and problems with a CFG with an Chomsky Normal Form approach. It does a great job 
at defining the structure and rules to reproduce a sentence, but is terrible when it comes to generating sentences based on 
its model. The uses for this could vary from case to case. One possible use is to study unique languages and its POS to help 
identify possible responses. Another is to identify the use of a word based on what POS it is paired with given a data set of 
sentences. Another keynote to take away is this model can be generated dynamically without interference, but has no mechanism 
to learn over time on what an appropriate sentence looks like.

<h3>Checkpoint</h3>

In this post, we went over some great figures in the NLP world, roads of thought for a NLP solution, 
how these roads of thought map to the modern day world, and a coding challenge for CFG for a subset of sentences. 
The coding problem certainly took some time and research, but boy was it worth it. Seeing this tree being used to generate 
random sentences of any caliber is exciting enough, especially researching ways on how it can be improved in all ways, shapes, 
and forms. I definitely want to revisit this code and further improve upon it when the time comes. But for now, I believe 
the point is made. CFGs with no statistics applied to your NLP solutions will produce cryptic messages, but may fit some solutions.

References

Foundations of Statistical Natural Language Processing, 1st Edition

https://blog.christianperone.com/2018/05/nlp-word-representations-and-the-wittgenstein-philosophy-of-language/

https://en.wikipedia.org/wiki/Colorless_green_ideas_sleep_furiously

https://www.montgomeryschoolsmd.org/curriculum/esol/cpd/module2/docs/chomsky.pdf

http://mbenhaddou.com/2017/07/02/text-generation-using-context-free-grammar/

https://www.researchgate.net/figure/Two-general-approaches-to-natural-language-processing-the-differentiation-between_fig2_259501468

https://www.ncbi.nlm.nih.gov/pmc/articles/PMC8089371/

More coding references are provided in README.md in git repo here: https://github.com/LlamasOnTheRun/YodaTextGeneratorWithLexicalRules
