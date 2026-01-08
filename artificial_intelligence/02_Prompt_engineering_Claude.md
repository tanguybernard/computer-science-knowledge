# Prompt Engeneering with Claude

## Chain of thought prompting

Chain of thought (CoT) prompting, encourages Claude to break down problems step-by-step, leading to more accurate and nuanced outputs.

source : https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/chain-of-thought


## Role prompting

Exemple

    You are the General Counsel of a Fortune 500 tech company. We're considering this software licensing agreement for our core data infrastructure:
    <contract>
    {{CONTRACT}}
    </contract>
    
    Analyze it for potential risks, focusing on indemnification, liability, and IP ownership. Give your professional opinion.
