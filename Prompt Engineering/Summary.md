# Prompt Engineering
## LLM Types
* Base LLM: In this the model will try to predict the next word using the data its trained on.
* Instruction LLM: This will try to predict the answer or follow the instruction.

Prompt engineering is based on Instruction LLM.

## Two Major principles of Prompt Engineering 
* Write clear and specific instructions "clear != short"
* Give the model time to think

## Principle 1: Write clear and specific instructions
### Tactic 1: Use delimiteres
```
Triple quotes: """
Triple backticks: ```
Triple dashes: ---
Angle Brackets: <>
XML tags: <tag> </tag>
```

e.g. Prompt: Summarize the text delimited by triple backtikcs. Into a single sentence. {Provide the text enclosed in ```}

### Tactic 2: Ask for structured outputs
```
HTML, JSON

e.g. Generate a list of three made-up book titles along with their authors. Provide them in JSON format with the following keys: book_id, title_author
```

### Tactic 3: Check whether conditions are satisfied, Check assumptions required to do the task
e.g. You will be provided with text delimited by triple quotes. If it contains a sequence of instructions, re-write those instructions in the following format: <br />
```
    Step 1: ... <br />
    Step 2: ... <br />
    ... <br />
    Step N: .... <br />

If the text doesn't contain a sequence of instructions, then simply write "No Steps Provided"
```

### Tactic 4: Few-shot prompting
Give successful examples of completing tasks. Then ask model to perform the task

e.g. Your task is to answer in the consistent style <br />
```
<child>: Teach me about Patience.

<grandparent>: The river that carves the deepest valley flows from a modes spring; the grandest symphony originates from a single note; the most beautiful of poems is an amalgamation of words; and the most enduring of structures is built one brick at a time. Patience is the key to success.

<child:> Teach me about resilience.
```

``This will be the generated answer``<br />
`<grandparent>: Resilience is like a tree that bends in the wind. After the storm passes, it springs back upright. Resilience is the ability to bounce back from adversity. It is the ability to adapt to difficult situations. It is the ability to overcome challenges. It is the ability to grow from hardship. Resilience is the key to success.`

## Principle 2: Give the model time to think
### Tactic 1: Specify the steps required to complete a task
    Step 1: ... <br />
    Step 2: ... <br />
    ... <br />
    Step N: .... <br />

Example 1:  """
In a charming village, siblings Jack and Jill set out on \ 
a quest to fetch water from a hilltop \ 
well. As they climbed, singing joyfully, misfortune \ 
struck—Jack tripped on a stone and tumbled \ 
down the hill, with Jill following suit. \ 
Though slightly  battered, the pair returned home to \ 
comforting embraces. Despite the mishap, \ 
their adventurous spirits remained undimmed, and they \ 
continued exploring with delight.
"""

Perform the following actions: 
1 - Summarize the following text delimited by triple \
backticks with 1 sentence.
2 - Translate the summary into French.
3 - List each name in the French summary.
4 - Output a json object that contains the following \
keys: french_summary, num_names.

Separate your answers with line breaks.

Example 2: <br />
Your task is to perform the following actions: 
1 - Summarize the following text delimited by 
  <> with 1 sentence.
2 - Translate the summary into French.
3 - List each name in the French summary.
4 - Output a json object that contains the 
  following keys: french_summary, num_names.

Use the following format:
Text: `<text to summarize>`<br />
Summary: `<summary>` <br />
Translation: `<summary translation>` <br />
Names: `<list of names in Italian summary>` <br />
Output JSON: `<json with summary and num_names>` <br /> 

### Tactic 2: Instruct the model to work out its own solution before rushing to consclusions

Example 1: <br />
Your task is to determine if the student's solution \
is correct or not.
To solve the problem do the following:
- First, work out your own solution to the problem. 
- Then compare your solution to the student's solution \ 
and evaluate if the student's solution is correct or not. 
Don't decide if the student's solution is correct until 
you have done the problem yourself.

Use the following format:
Question:
```
question here
```
Student's solution:
```
student's solution here
```
Actual solution:
```
steps to work out the solution and your solution here
```
Is the student's solution the same as actual solution \
just calculated:
```
yes or no
```
Student grade:
```
correct or incorrect
```

Question:
```
I'm building a solar power installation and I need help \
working out the financials. 
- Land costs $100 / square foot
- I can buy solar panels for $250 / square foot
- I negotiated a contract for maintenance that will cost \
me a flat $100k per year, and an additional $10 / square \
foot
What is the total cost for the first year of operations \
as a function of the number of square feet.
``` 
Student's solution:
```
Let x be the size of the installation in square feet.
Costs:
1. Land cost: 100x
2. Solar panel cost: 250x
3. Maintenance cost: 100,000 + 100x
Total cost: 100x + 250x + 100,000 + 100x = 450x + 100,000
```

### Model Limitations
Hallucination: Makes statements that sounds plausible but are not true. <br />

Example 1: <br />
Tell me about AeroGlide UltraSlim Smart Toothbrush by Boie USA. <br />
```
AeroGlide UltraSlim Smart Toothbrush by Boie USA is a smart toothbrush that is designed to be used with the Boie app. It is a smart toothbrush that is designed to be used with the Boie app. It is a smart toothbrush that is designed to be used with the Boie app. It is a smart toothbrush that is designed to be used with the Boie app. It is a smart toothbrush that is designed to be used with the Boie app. It is a smart toothbrush that is designed to be used with the Boie app. It is a smart toothbrush that is designed to be used with the Boie app. It is a smart toothbrush that is designed to be used with the Boie app. It is a smart toothbrush that is designed to be used with the Boie app.
```
##### _Note: that the Product here is a made up Name and not a real one._
 <br />
#### Reducing Hallucination: <br />
First find relevant information and then generate the answer based on relevant information. 
<br />
<br />


# Iterative Prompting
### Prompt Guidelines
* Be clear and specific
* Analyze why result doesn't give desired output
* Refine the idea and the prompt
* Repeat

### Iterative Process 
* Try something
* Analyze where the result is going wrong
* Clarify instructions and give more time to think
* Refine prompt with a batch of examples

# Summarizing Text

Example 1: <br />
""" 
Got this panda plush toy for my daughter's birthday, \
who loves it and takes it everywhere. It's soft and \ 
super cute, and its face has a friendly look. It's \ 
a bit small for what I paid though. I think there \ 
might be other options that are bigger for the \ 
same price. It arrived a day earlier than expected, \ 
so I got to play with it myself before I gave it \ 
to her.
"""
<br />
Prompt
```
Your task is to generate a short summary of a product \
review from an ecommerce site to give feedback to the \
pricing deparmtment, responsible for determining the \
price of the product.  

Summarize the review below, delimited by triple 
backticks, in at most 30 words, and focusing on any aspects \
that are relevant to the price and perceived value. 
```
_Note that you can also `extract` rather than `summarize` the text. Which will extract the information_

# Inffering

### Inference
* Inference is the process of drawing conclusions from evidence and reasoning.
Example 1: <br />
```
Needed a nice lamp for my bedroom, and this one had \
additional storage and not too high of a price point. \
Got it fast.  The string to our lamp broke during the \
transit and the company happily sent over a new one. \
Came within a few days as well. It was easy to put \
together.  I had a missing part, so I contacted their \
support and they very quickly got me the missing piece! \
Lumina seems to me to be a great company that cares \
about their customers and products!!
```
Prompt
```
What is the sentiment of the following product review, 
which is delimited with triple backticks?

Give your answer as a single word, either "positive" \
or "negative".
```
### We can also identify the number of emptions in the text. <br />
Prompt
```
Identify a list of emotions that the writer of the \
following review is expressing. Include no more than \
five items in the list. Format your answer as a list of \
lower-case words separated by commas.
```

### Identifying Anger <br />
Prompt
```
Is the writer of the following review expressing anger?\
The review is delimited with triple backticks. \
Give your answer as either yes or no.
```

### Extract information from the text and do mulitple tasks <br />
Prompt
```
Identify the following items from the review text: 
- Sentiment (positive or negative)
- Is the reviewer expressing anger? (true or false)
- Item purchased by reviewer
- Company that made the item

The review is delimited with triple backticks. \
Format your response as a JSON object with \
"Sentiment", "Anger", "Item" and "Brand" as the keys.
If the information isn't present, use "unknown" \
as the value.
Make your response as short as possible.
Format the Anger value as a boolean.
```

### Infer topics from the text <br />
Prompt
```
Determine five topics that are being discussed in the \
following text, which is delimited by triple backticks.

Make each item one or two words long. 

Format your response as a list of items separated by commas.
```
# Transforming

```
Translate the following English text to Spanish: \ 
```Hi, I would like to order a blender```
```

### Tone transformation
```
Translate the following from slang to a business letter: 
'Dude, This is Joe, check out this spec on this standing lamp.
```

### Format Conversion
```
Translate the following python dictionary from JSON to an HTML \
table with column headers and title:
```
### Spell Check and Grammar Correction
```
```The girl with the black and white puppies have a ball.```
Proofread and correct the following text and rewrite the corrected version. If you don't find and errors, just say "No errors found". Don't use any punctuation around the text
```

```
proofread and correct this review. Make it more compelling. 
Ensure it follows APA style guide and targets an advanced reader. 
Output in markdown format.
```
# Expand
```
You are a customer service AI assistant.
Your task is to send an email reply to a valued customer.
Given the customer email delimited by ```, \
Generate a reply to thank the customer for their review.
If the sentiment is positive or neutral, thank them for \
their review.
If the sentiment is negative, apologize and suggest that \
they can reach out to customer service. 
Make sure to use specific details from the review.
Write in a concise and professional tone.
Sign the email as `AI customer agent`.
Customer review: ```{review}```
```

# Summary
* Principles
  * Write clear and specific prompts
  * Give model time to think
* Iterative Prompting
  * Try something
  * Analyze where the result is going wrong
  * Clarify instructions and give more time to think
  * Refine prompt with a batch of examples





