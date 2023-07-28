---
title: The programmers brain
description: Some of the influential parts from the books that I have read.
summary: "Updated by Fatma, Jul 04, 2023."
date: 04-07-2023
categories:
  - "blog_posts"
tags:
  - "post"
  - "reading"
comments: true
---
## [The programmers brain](https://www.manning.com/books/the-programmers-brain)

### 1 Cognitive processes in programming

- Confusion is acceptable for a while when you start to work in a new domain. Not knowing the meaning of a concept and trying to read complex code are distinct ways of confusion. Each relates to a different cognitive process.
- Three ways of confusion:
  - __A lack of knowledge:=__ issue in long-term memory (LTM)
    - e.g., not knowing the meaning of an operator.
    - The relevant facts are insufficient in your LTM.
  - __Lack of information:=__ issue in short-term memory (STM)
    - e.g., not knowing the inner workings of a function.
    - STM stores information temporarily.
  - __Lack of processing power:=__ issue in working memory
    - You cannot process the entire execution despite an educated guess.

![memory.png](/img/memory.png)

- Three cognitive processes:
  - __Long-term memory:=__ a computer's hard drive
    - LTM is involved in everything we do.
    - e.g., writing binary search requires you to remember
      - the abstract algorithm
      - the syntax of the programming language (PL)
      - how to type on a keyboard
  - __Short_term memory:__ a computer's RAM or cache
    - e.g., keywords, variable names, and data structures when reading a program.
    - The estimated size of an STM is not more than a dozen of items.
    - STM is emptied when you solve the problem.
  - __Working memory:__ a computer's processor
    - You do tracing and other cognitively complex tasks here.
      - _Tracing_ is the mental compiling and executing of code.
    - You form new thoughts, ideas, and solutions here.

### 2 Read code quickly and get a sense of its workings

- STM and LTM
  - Information passes through sensory memory before it reaches STM.
    - Each of the five senses has its cache in the sensory memory.
    - _iconic memory_ is for the sense of sight
      - You can remember more information about code than you can process in your STM. _Code at a glance_ exercise will help you gain an initial image of the code.
        - Look at the code for a few seconds, then remove it from sight and try to answer the following questions:
          - What is the structure of the code?
            - Is the code nested deeply, or is it flat?
            - Are there any lines that stand out?
          - How is whitespace used to structure the code?
            - Are there gaps in the code?
            - Are there large blobs of code?
  - STM first stores information when you read code.
    - The time and size (2-6 things) limit STM to remember the information. You can use chunking for more, such as design patterns.
      - STM and LTM collaborate to overcome STM's size limitation.
  - LTM
    - syntactic knowledge of PL
    - know the algorithm before
  - Lack of practice makes code reading harder.

- Code reading
  - We often read code to
    - add a feature
      - the right location to implement
    - find a bug, and
      - the location of a specific bug where you last edited the code
      - how a certain method is implemented
    - build an understanding of a large system.

- Chunking
  - When you read new information, your brain tries to divide the information into recognizable parts called chunks.
  - If you want to write code that is easy to chunk, make use of design patterns.
  - To deliberately practice chunking, actively try to remember code. Ask yourself:
    - Which parts did you produce correctly with ease?
    - Are there any parts of the code that you reproduced partly?
    - Are there parts of the code that you missed entirely?
    - Do you understand why you missed the lines that you did?
    - Do the lines of code that you missed contain programming concepts that are unfamiliar to you?
    - Do the lines of code that you missed contain domain concepts that are unfamiliar to you?

- Comments
  - Add comments for your junior developers. Beginners focus more on comments.

- Beacons
  - They are parts of a program that help a programmer understand what the code does.
    - _Simple beacons_ are self-explaining syntactic code elements, such as meaningful variable names.
    - _Compound beacons_ do not offer much insight into the code, but together they do. For instance, a for-loop can be a compound beacon because it contains the variable, the initial assignment, and the increment and the boundary values.
  - Ask yourself:
    - What beacons have you collected?
    - Are these code elements or natural language information?
    - What knowledge do they represent?
    - Do they represent knowledge about the domain of the code?
    - Do they represent knowledge about the functionality of the code?

### 3 Learn programming syntax and concepts

- Knowing more syntax by heart eases chunking and avoids interrupting your work.
- Regular practices fight memory decay.
- Flashcards help to practice and remember the new syntax.
- Retrieval practice, trying to remember information before looking it up, is the best way.
- Spreading the practices maximize remembering.
- LTM stores information as a connected network of related facts.
- Engaging in the active processing of new information enhances the interconnectedness of memories, facilitating their retrieval and strengthening the memory network.

### 4 Read complex code

- Working memory is like the brain's processor. It processes `1+2+3=`.
- Cognitive load is the capacity to process two to six things at once. If the code is difficult to comprehend and you want to take notes or carefully track each step of execution, you may be facing a significant cognitive burden.
- Working memory overloads when too many elements cannot be divided efficiently into chunks.

- Types of cognitive load as they relate to programming
  - __Intrinsic load__ means how complex the problem is inside (inherent complexity).
  - __Extraneous load__ is what outside distractions add to the problem. It often occurs by accident.

- Techniques to reduce load
  
  - __Refactoring__ eases the maintenance and makes the code more readable.
  
    - __Inlining__ is to take a method and copy the body directly at the call site. It is a clear choice when it has a vague name.
    - Putting a method definition close to its first call reduces extraneous cognitive load.
  
  - __Replacing unfamiliar language constructs__, such as list comprehensions, lambdas and ternary operators.
  
  - __Code synonyms are great additions to a flashcard deck.__

- Memory aids to use when your working memory is overloaded:

  - __Creating a dependency graph__ helps you understand an interconnected code.
  
    1. Circle all the variables.
    2. Link similar variables.
    3. Circle all method/function calls in a different colour.
    4. Link methods/functions to their definitions.
    5. Circle all instances of classes in a third colour.
    6. Draw a link between classes and their instances.

  - __Creating a state table__ containing the intermediate values of variables for code with complex calculations may be util.
  
    1. Make a list of all the variables.
    2. Create a table and give each variable its column.
    3. Add one row to the table for each distinct part of the execution of the code.
    4. Execute each part of the code and write down the value of each variable in its cell.
  
  - __Combining dependency graphs and state tables__

### 5 Reaching a deeper understanding of code

- Figure out what roles the variables play when reading an unfamiliar code
  - There are eleven roles to cover almost all variables:
    1. __Fixed value__ is initialized once and never change, such as _pi_.
    2. __Stepper__ can be predicted as soon as the succession starts. It always iterates over a list of values that are known beforehand. It can be an integer.
    3. __Flag__ indicates that something happened or is the case.
    4. __Walker__ traverses a data structure like a stepper. It traverses a data structure unknown before the loop starts. It might be a pointer or integer index.
    5. __Most recent holder__ holds the latest value encountered in going through a series of values.
    6. __Most wanted holder__ holds the variable searched for a value.
    7. __Gatherer__ collects and aggregates data into one value.
    8. __Follower__ keeps track of a previous or subsequent value. It is always coupled to another variable. e.g., previous element in a linked list when traversing the list.
    9. __Container__ is a data structure holding multiple elements that can be added and removed. e.g., lists, arrays, stacks, and trees.
    10. __Organizer__ is only used for rearranging or storing values differently.
    11. __Temporary__ is used only briefly. It can be to swap data or store the result of a computation used multiple times in a method.

- A group of roles often characterizes a type of program. e.g. a program with a stepper and a most wanted holder value is a search program.

- Text structure vs plan knowledge
  - Text structure knowledge is to know the syntactic concepts.
  - Plan knowledge is to understand the intentions of the code's creator. It is to learn what parts of the code relate to other parts and how.
    1. Find a focal point. e.g. `main()` in Java. You need to understand how the framework links code together to know where to start.
    2. Expand knowledge from the focal point. Look for relationships in the code.
    3. Understand a concept from a set of related entities. You can check call patterns. For example, is there a method called in several places? It might be critical in the codebase.
    4. Understand concepts across multiple entities. Check for the operations applied to the data structures and the constraints on them.

- Your ability to learn a natural language can predict your ability to learn to program.

- There are different strategies to gain a deeper understanding of code, such as visualizing and summarizing.
- Programmers first scan the code. Novices read more linearly, whereas experts mostly follow the call stack.

Strategies for reading comprehension:

  1. __Activating__ is actively thinking of related things to activate prior knowledge. Giving yourself a fixed amount of time to study code and get a sense of what it's about activates prior knowledge. Questions:
     1. What was the first element that caught your eye? Why? ...
     2. Are these related?
     3. What concepts (syntactic or domain) are present? Do you know all?
  2. __Monitoring__ is keeping track of your understanding of a text. Mark the lines that you understand and make you confused. In your second time, you can focus on the confusing lines.
  3. __Determining importance__ is deciding what parts of a text are most relevant. Put an exclamation mark on the lines that look important. Questions:
     1. Why did you choose them?
     2. What role do those lines have?
     3. How are they connected to the overall?
  4. __Inferring__ is filling in facts that are not explicitly given in the text. Questions:
     1. What is the domain or topic?
     2. What concepts are used?
     3. What can you learn from them?
     4. Which names are related to each other?
     5. Are there ambiguous names when looked at without context?
     6. What meaning could ambiguous names have?
  5. __Visualizing__ is drawing diagrams of the read text to deepen understanding.
  6. __Questioning__ is asking questions about the text at hand. Questions:
     1. What are the five most central concepts?
     2. What strategies did you use to identify the central concepts?
     3. What are the five most central computer science concepts?
     4. What can you determine about the decisions made bythe creator(s)?
     5. What assumptions do decisions rely on?
     6. What are the benefits of these decisions?
     7. What are some potential downsides of these decisions?
     8. Can you think of alternative solutions?
  7. __Summarizing__ is creating a short summary of a text.

### 6 Solve programming problems better

- Models help communicate information about programs and solve problems.
- The following subsections explains how to make decisions about different software designs

#### 6.1 The mental model is created by the brain while programming

- It creates an abstraction in your working memory that you can use to reason about the problem at hand.

- Creating mental models of source code __in the working memory__
  1. Begin by creating local models
  2. List all relevant objects in the codebase and the relationship between them
  3. Answer questions about the system and use the answers to refine your model
     1. What are the most important elements? Are they present in the model?
     2. What are the relationships between these important elements?
     3. What are the main goals of the program?
     4. How does the goal relate to the core elements and their relationships?
     5. What is a typical use case? Is it covered in the model?

#### 6.2 How we think about computers when solving problems

- Notional machines are abstract versions of how a real computer functions that are used when explaining programming concepts and reasoning about programming. They help us understand programming because they enable us to apply existing schemata to programming. Different notional machines sometimes nicely complement each other but may also create conflicting mental models.

- Analyzing to scope problems correctly by abstracting irrelevant details and including important ones

### 7 Misconceptions: Bugs in thinking

- __Positive transfer__ helps you learn faster and perform tasks better by getting knowledge from your LTM and transfering to new situations. You can actively search for related information in your LTM to use it.
- The factors effecting how much transfer takes place:
  1. __Mastery__ How well you’ve mastered the task for which knowledge is already stored in your LTM.
  2. __Similarity__ Commonalities between the two tasks.
  3. __Context__ How similar the environments are.
  4. __Critical attributes__ How clear it is to you what knowledge may be beneficial.
  5. __Association__ How strongly you feel that the tasks are similar.
  6. __Emotions__ How you feel about the task.

- __Negative transfer__ happens when existing knowledge interferes with learning new things or executing new tasks. You may hold misconceptions when you assure that you are right, but you are wrong. To fix misconceptions, you need a new mental model to replace the wrong model. Even if you have learned a correct model, there is always the risk you will fall back to using the misconception. Use tests and documentation within a codebase to help prevent misconceptions.

- __High-road transfer__ is of more complex task.
- __Low-road transfer__ is of automatized skills.

- __Near transfer__ happens when the transfer is between close domains.
- __Far transfer__ happens when the transfer is between distant domains.

- For a belief to be a misconception, it must be faulty, be held consistently, across different situations, and be held with confidence.

### 8 How to get better at naming things

- Naming matters for four reasons:
  - Names make up a large part of code.
  - Names play a role in code reviews.
  - Names are the most accessible form of documentation.
  - Names can serve as beacons.

- Some examples from Simon Butler's naming conventions:
  - Identifiers should be composed of between two and four words.
  - Identifiers should not consist of fewer than eight characters, except for c, d, e, g, i, in, inOut, j, k, m, n, o, out, t, x, y, z.
  - Unless there are clear reasons not to do so, enumeration types should be declared in alphabetical order.
  - Identifiers should not begin or end in an underscore.
  - Type information should not be encoded in it.

- Identifiers consisting of full words are easier to understand.
- Not the length of variable names make harder to remember, but the number of syllables the names contain.

- Words are better than letters and abbreviations.

- Camel case variables are more rememberable. Snake case is more recognisable.
- Initial naming practices have a lasting impact.
- Although there is no causation, bad naming code is more prone to bugs.
- There are many different name molds used to shape variable names, but limiting yourself to a smaller number of molds will likely help comprehension.

- Applying Feitelson’s three-step model (what concepts to use in a name, what words to use for those concepts, and how to combine them) leads to higher quality names.

### 9 Code smells and the cognitive principles behind them

- Code smells, such as long methods, indicate structural issues with code. There
are different cognitive reasons why code smells cause a higher cognitive load.
Duplicated code, for example, makes it harder to chunk code properly, while
long parameter lists are heavy on your working memory.
 There are different ways to measure cognitive load, including biometric sensors
like measuring blinking rate or skin temperature. If you want to measure your
own cognitive load, the Paas Scale typically is a reliable instrument.
 Linguistic antipatterns indicate places in a codebase where code does something
different than names involved suggest, leading to a higher cognitive load.
This is likely caused by the fact that your LTM finds wrong facts while trying to
support your thinking. Linguistic antipatterns can also lead to wrong chunking
because your brain assumes a meaning of code that is not actually implemented.

### 10 Advanced techniques to solve complex problems

- While many people in programming argue that problem solving is a generic skill, it is not. Your prior knowledge of programming, coupled with the current problem you are solving, influence how quickly you can solve programming problems. Your LTM stores different types of memories, which all play a different role when solving problems. The two overarching categories of memories are implicit and explicit memories. Implicit memories are "muscle memories", tasks you can execute without thinking about them, like touch typing. Explicit memories are memories you are aware of that you need to actively recall, such as the syntax of a for-loop.
- To strengthen your implicit memories related to programming, it is best to automatize related skills, such as touch typing and memorizing relevant keyboard shortcuts.
- To strengthen your explicit memories related to programming, study existing code, preferably with an explanation about how the code was designed.

### 11 The act of coding and variety of tasks in programming

When you are programming, you perform a combination of different programming
activities: searching, comprehending, transcription, incrementation, and
exploration. Each activity puts pressure on different memory systems. Therefore,
each activity should be supported by different techniques.
 Interruptions while you are programming are not only annoying; they are detrimental
to productivity because it takes time to rebuild your mental model of
the code.
 To better deal with interruptions, offload mental models into notes, documentation,
or comments.
 Deliberately support your prospective memory if you cannot complete a task by
documenting your plans.
 Try to limit interruptions to moments you experience low cognitive load, for
example, through automation using a FlowLight or manually by setting your
status in Slack.

### 12 Improve large code bases

CDN is a framework that helps programmers predict the cognitive effect programming
languages will have on their users.
 CDCB is an extension of CDN that helps programmers understand the impact
their codebases, libraries, and frameworks will have on their users.
 In many cases, trade-offs between different dimensions must be made. Improving
one dimension might decrease another dimension.
 Improving the design of existing codebases according to the notations framework’s
cognitive dimension can be done with a design maneuver.
 Different activities place different demands on the dimensions a codebase
optimizes for.

### 13 Less painful onboarding process of new developers

Experts think and act differently from beginners. Experts can reason abstractly
about code and have the ability to think about it without referring to the code
itself. Beginners tend to focus on details in the code and have a hard time stepping
back from details.
 When midlevel programmers learn new information, they sometimes fall back
to beginner-level thinking.
 People who are learning a new concept need to learn about it in both abstract
terms and in concrete examples.
 People who are learning a new concept also need time to connect a new concept
to prior knowledge.
 When onboarding, limit the programming activities newcomers perform to one
at a time.
 When onboarding, prepare relevant information to support the onboardee’s
long-term, short-term, and working memory.

---

Updated by _Fatma_ on July 04, 2023
