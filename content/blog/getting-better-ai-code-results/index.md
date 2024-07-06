+++
title = 'Getting better AI code results'
date = 2024-07-05T15:04:58-06:00
tags = ["artificial intelligence", "productivity"]
draft = false
+++

If you have used AI to generate code for any remotely niche technology, you must have quickly realized that AI is not magic, and it does not possess the answer to every problem.

As an example, in the past couple of weeks I had been using AI to help me automate some repetitive tasks in AutoCAD. AutoCAD uses its own programming language derived from Lisp called [AutoLisp](https://en.wikipedia.org/wiki/AutoLISP) which you can use to create custom commands.

Since I just wanted to streamline my workflow, it didn't make sense for me to "learn" AutoLisp. Instead, I used ChatGPT to make the custom command for me.

## The problem

As soon as I started prompting the AI, I found myself trapped following this faulty set of instructions:

1. Provide ChatGPT with context and express in detail the desired result. The AI will generate an initial code. Go to Step 2.

1. Try the code / run the command. If there is an error, go to Step 3.
1. Copy the error obtained (usually word for word) and inform ChatGPT about it. The AI will change the part of the code where it thinks the problem is. Go to Step 2.

You can spend hours trying to get ChatGPT to fix the problem. You may never be able to get out of this loop. The truth is that if ChatGPT knew how to solve the problem, it would've given you the solution since the beginning.

The issue is that we tend to believe that AI chatbots are _intelligent_, and that they will eventually understand why their code is not working. We also tend to believe that the AI is aware of all the possible ways of solving the problem, and knowledge of all the available built-in functions. But they do not.

## The solution

Once the AI is stuck in a way of "thinking", you will need to "feed it" new ideas to break the pattern. You must give the AI examples of solutions to similar problems.

You will need to search for these examples in forums, you may need to read the documentation. You might even find the solution to your problem in the documentation and realize that it was way simpler than what the AI was trying.

## Conclusion

AI is a great tool, but it is not _actually_ intelligent. If you want good results and want to avoid terrible code, you should have a basic understanding of how the solution might look like.
