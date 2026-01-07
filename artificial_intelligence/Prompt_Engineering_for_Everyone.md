
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

## Module 3: The Chain-of-Thought Approach

The Chain-of-Thought (CoT) methodology significantly bolsters the cognitive performance of AI models by segmenting complex tasks into more manageable steps. By adopting this prompting strategy, AI models can demonstrate heightened cognitive abilities and offer a deeper understanding of their reasoning processes.

This approach is an example of prompt-based learning, and it requires feeding the model with questions and their corresponding solutions before posing related subsequent questions to it. In other words, our CoT prompt teaches the model to reason about the problem and mimic the same reasoning to respond to further queries correctly.

### Zero-Shot Chain-of-Thought Prompting

There are a few words that, when added to the prompt, are likely to solicit better answers since they invite the AI to do step-by-step reasoning, much like a human would when trying to come to a resolution.

According to researchers, two effective phrases are:

    Let's think step by step.

And:

    Let's work this out in a step by step way to be sure we have the right answer.

### Chain-of-Thought to explore subjects


Chain-of-Thought can be used in various ways to improve the chatbot's reasoning, especially in areas where it's feeble. However, a more valuable use is when it comes to exploring subjects more in-depth.

Instead of asking a generic question, we can break it down into steps we want the model to consider to develop a much richer and valuable answer.

#### Exemple


    What is space exploration?

#### Chain-of-Thought approach


Prompt Instructions

    Consider and include the following elements in your answer:
    
    - Historical Space Missions
    - Moon landing and Human Achievement
    - Moon landing and impact on the Cold War
    - Satellite technology and its impact on humanity
    - Mars colonization possibilities
    - Search for extraterrestrial life
    - Space tourism prospects
    - Space debris and environmental impact
    - International Space Station collaboration
    - Advancements in rocket technology
    - Interstellar travel challenges
    - Private companies and Billionaires involvement controversy
    
    Let us think step by step.

Prompt : 

    What is space exploration?

#### Difference

The downside is that we had to develop a list requiring knowledge of the subject or at least research into it, and this is time-consuming.

On the plus side, we didn't have to retrain the model, which would be truly time-consuming and potentially expensive. Instead, the prompt split the "problem" into smaller steps worth exploring and leveraged the existing model training to compute a reply.

Moreover, these starting points can lead to various interconnected thoughts and ideas from the model. The beauty of a Chain-of-Thought is that it can branch out in different directions, exploring numerous aspects and perspectives related to the initial topic.

We can ask specific questions at any time after the model has already shown us a broader understanding of the topic.

## Module 4: Advanced Techniques



    
