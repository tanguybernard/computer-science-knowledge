
# IBMSkillsNetwork AI0117EN
# Prompt Engineering for Everyone


## Module 1: Introduction to Prompt Engineering

### Zero-shot, one-shot, and few-shot prompting

In a zero-shot scenario, the model is given a task without any prior examples; it must determine what to do based solely on the prompt and its training.

For example, when we asked, 'What is Prompt Engineering?' we used a zero-shot prompt.

In contrast, a one-shot prompt provides the model with a single example, while a few-shot prompt includes multiple examples to guide its output.

Naive or standard prompts typical don't use few-shots prompting.


## Module 2: Getting Started with Prompt Engineering

### Lab 3

#### The difference between prompt instructions and the prompt
Technically, you could paste in the Prompt Instructions just before your question for the AI. What is the difference between the two approaches?

Aside from appearing much neater visually, splitting the prompt instructions from the prompt allows us to lock the instructions to the whole conversation without repasting it each time we ask a question.

Occasionally, this differs from what we want, so placing such instructions directly in the prompt textbox can be beneficial to limit them to that single question without affecting the rest of the chat.

### Lab 4: The Naive Prompting Approach and the Persona Pattern

#### The Naive Approach

    What's the best way to get fit?


#### The same query, using a persona

    Acting as a fitness expert, tell me the best way to get fit.

#### When the Persona is someone famous


    Acting as marketing expert Seth Godin, give me a list of 10 article 
titles to promote my new book about dog training.


### Lab 5: The Interview Pattern

#### Example :

Prompt Instructions :

    You will act as a fitness expert who is current with the latest research data and provide very detailed step-by-step instructions in reply to my queries. You will interview me, asking me all the relevant questions necessary for you to generate the best possible answer to my queries.


Prompt input box :

    Create a gym workout program to lose weight and build strength.

#### Creating a blog post with the Interview Pattern

Prompt Instructions

    You will act as a SEO and content marketing expert. You will interview me, asking me (one at the time) all the relevant questions necessary for you to generate the best possible answer to my queries. 


Prompt

    Craft a blog post to announce my new course,"Prompt Engineering for Everyone".

    Prompt Instructions aternative

Ask me a series of questions, one by one, to gather all the information you need to give a proper response.

#### Tips

1. Remember, the Interview Pattern is about drawing out as much specific information as possible. Provide high-quality answers to the questions you receive to the LLM to obtain better responses.
2. Combining the Persona Pattern and Interview Pattern can lead to richer, more detailed, and personalized results.
3. Don't hesitate to experiment with different instructions. Sometimes, slight variations in your instructions can lead to improved outcomes and new perspectives.
