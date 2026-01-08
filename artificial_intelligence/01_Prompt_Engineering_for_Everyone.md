
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

### Lab 7: The Tree-of-Thought Approach in Prompt Engineering

<img width="840" height="550" alt="tree-of-thought" src="https://github.com/user-attachments/assets/2068e060-627a-4e9b-8f4a-68282623aeb9" />

For example, in the Game of 24, GPT-4 with Chain-of-Thought prompting solved only 4% of tasks. In comparison, their ToT approach achieved a success rate of 74%.

The researchers remarked that the CoT didn't perform as well as it “lacks mechanisms to try different clues, make changes to decisions, or backtrack.”

And that's the main limitation of CoT. When considering a complex problem, humans (well, systematic and logical ones, at least) tend to explore a tree of thoughts, evaluating what works and what doesn't, backtracking if needed, jumping back to a previous “node” in the tree if it was more beneficial or promising for the resolution of the problem.

#### Example of Tree-of-Thought

Tree-of-thought prompting uses a similar approach that not only invites the AI to consider a step-by-step process and to think logically but also makes it consider intermediate thoughts, building upon them and exploring branches that may or may not lead somewhere. This exploration maximizes the use of LLM and its capabilities, leading to drastically more useful results.

Tree-of-Thought (ToT) Prompting is an innovative method that expands upon and refines the existing Chain-of-Thought prompting approach. By incorporating ToT Prompting, LLMs can demonstrate enhanced reasoning skills. Moreover, this technique allows these models to correct their mistakes autonomously and continually build upon their knowledge.

Dave Hulbert suggested a few rather convincing prompts that leverage this approach and yield, anedotically, great results. I particularly like how he incorporates the Persona pattern and recommend you approach ToT prompting using his prompts or similar variations you might develop yourself.


Prompt

    Bob is in the living room.
    He walks to the kitchen, carrying a cup.
    He puts a ball in the cup and carries the cup to the bedroom.
    He turns the cup upside down, then walks to the garden.
    He puts the cup down in the garden, then walks to the garage.
    Where is the ball?


Naive Answer (GPT-4o mini 7 Jan. 2026) :

    The ball is in the garden. When Bob turned the cup upside down in the bedroom, the ball would have fallen out of the cup. Since he then walked to the garden and put the cup down there, the ball would be on the ground in the garden.





Prompt Instructions V1

    Imagine three different experts are answering this question. 
    All experts will write down 1 step of their thinking, then share it 
    with the group. Then all experts will go on to the next step, etc. 
    If any expert realises they're wrong at any point then they leave. 
    Answer the question based on experts' opinion. The question is...



Prompt Instructions V2 :

    Simulate three brilliant, logical experts collaboratively answering a question. Each one verbosely explains their thought process in real-time, considering the prior explanations of others and openly acknowledging mistakes. At each step, whenever possible, each expert refines and builds upon the thoughts of others, acknowledging their contributions. They continue until there is a definitive answer to the question.The question is...


Prompt Instructions V3 :

    Identify and behave as three different experts that are appropriate to answering this question.
    All experts will write down the step and their thinking about the step, then share it with the group.
    Then, all experts will go on to the next step, etc.
    At each step all experts will score their peers response between 1 and 5, 1 meaning it is highly unlikely, and 5 meaning it is highly likely.
    If any expert is judged to be wrong at any point then they leave.
    After all experts have provided their analysis, you then analyze all 3 analyses and provide either the consensus solution or your best guess solution.
    The question is...


Answer with Prompt Instructions V3:

    All experts agree that the ball is not in the cup after Bob turns it upside down in the bedroom. Therefore, the final answer is:

    The ball is in the bedroom (on the floor, as it fell out of the cup).

#### Applying ToT to something more useful

Prompt Instructions :
    
    Imagine three different experts are answering this question.
    All experts will write down 1 step of their thinking,
    then share it with the group.
    Then all experts will go on to the next step, etc.
    If any expert realizes they're wrong at any point then they leave.


### Lab 8: Controlling Verbosity and the Nova System

#### Controlling Verbosity

#### The Nova System: An Advanced Problem-Solving Tool

The Nova System (or Nova Process) is an intelligent way to solve problems using a team of virtual experts powered by an LLM such as GPT-4o.

##### What’s Special About Nova?

Nova uses ChatGPT to create a “team” of experts that discuss and find solutions to tricky problems.
It has a Discussion Continuity Expert (DCE) who keeps the conversation on track.
There’s also a Critical Evaluation Expert (CAE) who checks solutions to make sure they’re good and safe.

##### How Does Nova Work?

Problem Unpacking: It breaks the problem down to understand it fully.
Expertise Assembly: It picks the right experts for the job and gets their initial thoughts.
Collaborative Ideation: The experts brainstorm together. The DCE leads the talk, and the CAE ensures the ideas are good and safe.

##### Key Roles:

- DCE: Keeps the discussion clear and on track.
- CAE: Reviews the ideas and discusses any issues using facts and evidence.

#### The Prompt Index

The Prompt Index is a site boasting a huge AI prompt database. The site doesn’t simply specialize in conversational AI but also includes prompts for other forms of generative AI, such as Midjourney and DALL-E, which enable the generation of images.

### Lab 9: Getting to Know watsonx Prompt Lab

IBM Prompt

