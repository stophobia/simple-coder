# MoleculAI: Amplifying LLM Code Generation Performance

## It does not chat. It writes code.

As any respectable scientist will tell you: the proof of the pudding is in the eating!

Since this is a code generating agent, we will focus on tests specifically for programming, namely HumanEval.

Using the SimpleCoder class, it is possible to achieve the following performance gains using OpenAI and GPT:
- GPT-4: **from 67% to 83%**
- GPT-3.5: **from 48% to 69%**

[ for test methods see `book.4_test.ipynb`]

### HumanEval Leaderboard
[Code Generation on HumanEval](https://paperswithcode.com/sota/code-generation-on-humaneval)

| Rank | Model                   | pass@1 | Paper Title                                                     | Year |
|------|-------------------------|-------|-----------------------------------------------------------------|------|
| 1    | Reflexion (GPT-4)       | 91.0  | Reflexion: Language Agents with Verbal Reinforcement Learning   | 2023 |
| 2    | Parsel (GPT-4 + CodeT) | 85.1  | Parsel: Algorithmic Reasoning with Language Models by Composing Decompositions | 2023 |
| ***   | SimpleCoder (GPT-4)    | 83 | <--- this repo  | July, 2023 |
| ***   | SimpleCoder (GPT-3.5)  | 69 | <--- this repo  | July, 2023 |
| 3    | GPT-4 (zero-shot)       | 67.0  | GPT-4 Technical Report                                          | 2023 |
| ... |
| 8    | GPT-3.5                  | 48.1  |  | 2023 |

# SimpleCoder vs Reflexion
[Reflexion: Language Agents with Verbal Reinforcement Learning; arXiv:2303.11366 [cs.AI]](https://arxiv.org/pdf/2303.11366v3.pdf)

The difference: *simplicity*

While both approaches have a similar iterative loop structure, the Reflexion approach utilizes three distinct models for generation, evaluation, and self-reflection. This is a very robust approach, but it can be challenging to understand and implement.

SimpleCoder uses a minimized architecture, with a single agent that iterates over it's own output until it determines that the solution is adequate, at which point it outputs a stop code.

We provide a simplified interface for running this architecture over your own files, which you can find in one of our included Jupyter notebooks.

# FEATURES
* Runs on your local machine
* Can write output files directly to disk
* Can read your existing code or text, and use it for reference
* Can refactor existing files or create new ones
* Hooked up to OpenAI chat completion by default, but can be changed to open source LLM

# How are you doing this?!
## What are Agents?

An LLM Agent is a piece of code managing the message state between you and the LLM. While most people experience AI interactions through simple chat bots (basic UI elements linked to a chat completion endpoint), such agents do not enhance the quality or capabilities of the AI output.

Other agents are very advanced and can allow the AI to use tools, or construct and manage task lists that can be chained and executed. These agents are very powerful, but can be extremely difficult to understand, customize, and implement into your code. 

## Enter SimpleCoder: A Minimized Code-Generating Agent

SimpleCoder is a minimized code generating and editing Agent. It implements self-reflection, similar to Reflexion ([github](https://github.com/noahshinn024/reflexion)), to allow the bot to improve on it's own output.


The following is a simplified version of a loop that SimpleCoder runs. It runs this loop until it determines that it is done with the problem.

```
compose_message_log()

response = generate_response()

process_response(response)

store_code_file()

```
[ you can find this in `moleculai/simple_coder.py > SimpleCoder.work()` ]


# Getting started
Check out the following Jupyter notebooks with samples that will illustrate various use cases:
* `book.1_simple_coder.ipynb`
    * Basic use - generate a new file
    * Generate with reference to another file
* `book.2_refactor.ipynb`
    * Refactor an existing file
* `book.3_project.ipynb`
    * Generate a multi-file project
    * Consistent cross-file references
    * Create documentation