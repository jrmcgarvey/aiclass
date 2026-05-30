## Slide 1

TECHNICAL FOUNDATIONS

How LLMs Work

Part 1: Architecture

From raw text to a thinking machine --- step by step

Tokens  ·  Embeddings  ·  Position  ·  Attention  ·  Neurons & Layers

## Slide 2

SESSION OVERVIEW

Artificial Intelligence for Lay People  ·  Week N

What we will cover today

1

Tokens

How text is broken into manageable pieces

2

Embeddings

Giving words a location in meaning-space

3

Position

Why word order matters, and how it is encoded

4

Attention

How words notice and influence each other

5

Neurons & Layers

The neural network machinery underneath

## Slide 3

TOKENS

Artificial Intelligence for Lay People  ·  Week N

The Goldilocks Problem

Whole Words

Too many

Hundreds of thousands of words in English alone --- plus slang, technical terms, new coinages. An unmanageably large dictionary.

Tokens

Just right

50,000--100,000 chunks covering virtually any text. Common words get one token. Rare words split into meaningful pieces.

Single Letters

Too few

Letters carry almost no meaning alone. The letter \'b\' tells you nothing. Processing letter-by-letter loses all structure.

## Slide 4

TOKENS

Artificial Intelligence for Lay People  ·  Week N

What tokens look like --- and a surprising side effect

Sample tokens from a typical model

the

cat

sat

on

un

believ

able

ing

pre

John

!

2024

■  Whole words    ■  Sub-word fragments    ■  Names    ■  Other

A surprising side effect

How many r\'s in  strawberry ?

The model never sees individual letters. It sees tokens: 

straw

berry

To count letters, the model must reason about what is inside each token --- indirectly. It often gets it wrong.

Each token is assigned a unique ID number. From here on, the model works entirely with numbers.

## Slide 5

EMBEDDINGS

Artificial Intelligence for Lay People  ·  Week N

Giving words a location in meaning-space

The idea

Each token is placed at a location in a mathematical space --- like a map.

Words with similar meanings end up near each other:

cat  and  kitten  are neighbors.

king  and  queen  are neighbors.

cat  and  nuclear reactor  are far apart.

meaning →

cat

kitten

dog

puppy

king

queen

prince

car

truck

## Slide 6

EMBEDDINGS

Artificial Intelligence for Lay People  ·  Week N

The map starts random --- training makes it meaningful

Random initialization

At the start of training, every token is placed at a random location --- drawn from a bell-curve distribution centered on zero.

At this point,  cat  and  nuclear reactor  are equally likely to be neighbors. Pure chance.

Training on trillions of words gradually moves every token to where it belongs --- until the geometry of the space reflects the structure of language.

Initial value distribution

0

most starting values

cluster near zero

## Slide 7

EMBEDDINGS

Artificial Intelligence for Lay People  ·  Week N

From two dimensions to thousands

A real map has 2 dimensions. An embedding space has thousands.

Each additional dimension is another axis along which tokens can be similar or different --- capturing grammar, formality, emotional tone, subject matter, and properties we don\'t even have names for.

768

dimensions

Small model

1,536

dimensions

Medium model

4,096+

dimensions

Large model

Key insight

Each token\'s location is stored as a list of numbers --- one per dimension.

A large model might store each token as a list of 4,096 numbers.

This list is called the token\'s  embedding vector.

By the end of training, the geometry of this space encodes a remarkable amount of human knowledge about language and meaning.

## Slide 8

POSITION

Artificial Intelligence for Lay People  ·  Week N

Word order matters --- and the model needs to be told

The problem: the model processes all tokens simultaneously --- it has no built-in sense of order.

The dog chased the boy.

The boy chased the dog.

Same tokens. Completely different meaning.

The solution

Each token gets a second vector --- a position tag --- added to its embedding. Position 1\'s tag is always the same regardless of which word sits there. The combined vector carries both what the word means and where it sits in the sentence.

## Slide 9

POSITION

Artificial Intelligence for Lay People  ·  Week N

Meaning + position = a unique combined vector

The

\+

Pos 1

Combined

vector

dog

\+

Pos 2

Combined

vector

chased

\+

Pos 3

Combined

vector

the

\+

Pos 4

Combined

vector

boy

\+

Pos 5

Combined

vector

Note:  the two instances of  \"the\"  now have  different  combined vectors --- because they sit in different positions. The model can tell them apart.

## Slide 10

ATTENTION

Artificial Intelligence for Lay People  ·  Week N

Every word gets to ask: how relevant are you to me?

How attention works

Every token looks at every other token in the sentence and asks:  how relevant are you to me? 

The answers are collected and used to build a richer, context-aware representation of each token.

Example:  \"The bank of the river was steep.\"

The word  bank  looks across the sentence and finds  river  highly relevant. This shifts its meaning away from finance and toward geography.

The

bank

of

the

river

was

steep

Thick line = strong attention    Thin line = weak attention

\"bank\" pays strong attention to \"river\" --- resolving the ambiguity

## Slide 11

ATTENTION

Artificial Intelligence for Lay People  ·  Week N

Multiple attention heads --- looking for different relationships

Head 1

Grammatical relationships

Which word is the subject? Which is the object? How do verb tenses relate?

Head 2

Semantic relationships

Which words share a topic or domain? What is this passage about?

Head 3

Reference tracking

When the text says \"it\" --- what does it refer to? Connecting pronouns to nouns.

Combined: rich, context-aware token vector

## Slide 12

NEURONS & LAYERS

Artificial Intelligence for Lay People  ·  Week N

The neural network machinery

What is a neuron?

A neuron is a very simple computing unit:

1.  Receives numbers as input

2.  Multiplies each by a  weight  --- its importance score

3.  Adds the results together

4.  Passes the sum through an  activation function  --- enabling complex pattern learning

The connections between neurons are the weights --- the parameters adjusted during training.

x₁

w₁

x₂

w₂

x₃

w₃

Σ

f(x)

activation

function

output

A single neuron

## Slide 13

NEURONS & LAYERS

Artificial Intelligence for Lay People  ·  Week N

Layers of processing --- stacked deep

Attention

Feed-Forward

Layer 96

Attention

Feed-Forward

Layer 95

· · ·

Attention

Feed-Forward

Layer 2

Attention

Feed-Forward

Layer 1

Inside each layer

Every layer contains two steps in sequence:

1. Attention --- tokens look at each other

2. Feed-Forward Network --- each token is processed individually

Between steps, Layer Normalization keeps the numbers stable.

How deep?

Large models have 96 or more layers. Each layer adds another round of refinement. By the final layer, each token\'s vector carries a remarkably rich representation of its meaning in context.

## Slide 14

SUMMARY

Artificial Intelligence for Lay People  ·  Week N

What we have built --- and what comes next

Text

Raw input

Tokens

Numbered chunks

Embeddings

Meaning-space vectors

Position

Order encoded

Attention

Context gathered

Layers

Deep refinement

The machine now exists --- but it is full of random numbers and cannot do anything useful yet.

Next session: How the model learns

Training  ·  Gradient Descent  ·  Fine-Tuning  ·  Inference  ·  Capabilities & Limitations

We have built the machine. Next time we fill it with knowledge.

## Slide 15

See you next session.

Next time: Training, Gradient Descent, Fine-Tuning, and Inference

How does the machine learn? How does it generate a response?

We will find out.

Artificial Intelligence for Lay People  ·  Week N
