# My Metal Model of Software Development

A while ago, I started to look for a new job, which means I've been interviewed quite an amount of times recently. During tech interviews, devs tend to ask more or less same questions. But there is one, which although been asked several times still was causing me trouble every single time: *"What constitutes a good code for you?"*

Every time I tried to answer it, I was somehow disappointed with the answer. Whenever I went into describing specific code qualities like readability, modularity, testability, extensibility, etc I've always felt like something important is left behind. Something, that should precede all these qualities and be a source behind such principles as SOLID, DRY, YAGNI, KISS, DAFAQ, name it. 

So, I was thinking about that and I believe I've come up with a nice answer. At least, I like it myself.

## Model

To answer the question, I'm going to introduce a tiny model of the software development process, based on a notion of two discrete sequences: a sequence of requirements and a sequence of code states.

**Requirements.** There are always two parties involved in software development, even when they are sitting inside a single human head. One needs software to be built, and another builds it. The former is the source of the flow of changing requirements. We can represent this flow as a function of time:

```r_t = requirements(t)``` 

**State.** From a code perspective, any system we are building is a series of states of its codebase. Once again, let's think of it, as a function of time: 

```s_t = state(t)```

**Requirements mismatch.** Given requirements and a state, we can introduce requirements mismatch as a higher-order function taking `requirements` function, `state` function and time as its arguments: 

```m_t = mismatch(requirements, state, t)``` 

## The Answer

The best system in term of code quality is the one, for which the result of the integration of function `mismatch` over the interval of the system's lifetime is as small as possible.

## Let's make it a bit more complicated. 

Given model is just enough to give the smarty-pants answer to *"what is a good code?"* question I gave in a previous section. But once I started to bother with model building it would be nice to use the model for the reason smart folks do that, namely use it as a foundation of for some speculation about the real world.  To do so, I have to introduce some more complexity to it.
 
**Requirements depend on the current State.** Stakeholders producing requirements often realize their original requirements have to be adjusted when they start to use software built based on their previous requirements: 

```r_t = requirements(state, t)```

In other words, due to our limited mental capabilities, it's hard for us humans to say if we satisfied with something before we use it. The lack of recognition of that fact is the main oversight of classical waterfall-like approaches to building software.  

**In turn, the state change is based on requirements.** We are building software, because someone needs it, so we always satisfying some requirements:

```s_t = state(requirements, t)```

It looks too obvious to even mention it.  But if we'll pay attention to the fact that `requirements` is itself a function of time, we can understand one of the main flaws of modern Agile sprint-based methodologies (at least in the way they are being adopted by companies). They just tend not to respect the long-term nature of incoming requirements, and instead focus on several up-coming sprints only.  In other words, agile methodologies are like greedy algorithms, and we as programmers know that greedy for a wide range of problems, greedy algorithms fail to provide an optimal solution.

**State change is limited by the effort we put in.** Each state transformation takes some effort from programmers building the system:

```s_t = state(requirements, effort, t)```

It doesn't really matter if we'll represent effort as a function of time (we are dropping more developers into a team when needed) or a constant value (in case of a stable team working on a project in fixed lengthed iterations). What's matter is that it should be clear that we can't go from any s1 to any s2. Withing given time frame, we can change the system only that much. 

And this last point brings lots of excitement to my daily life! If you ever participated in one of these popular programming challenges, where you have to program simulated Moon landing unit, you know that it has the same core problem. You can't arbitrarily change landing unit velocity and position, because it's limited by a maximum torque you can apply. 

In other words, if you'll try to see this big picture of software development. And think about this analogy between spacecraft landing problem and any long-term software project, you can see that no matter how big, how legacy and how boring the system you are working on is, it's, in fact, a rocket science! The only shameful difference is that we as an industry are used to happily smashing our "spacecrafts" into Moon surface and starting over while giving this process fancy names like *"legacy system decommissioning"*. 
