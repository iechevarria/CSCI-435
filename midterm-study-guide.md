# CSCI 435 Midterm Study Guide 

## Lecture 1:  Introduction to Software Engineering

- **software engineering:** establishment and use of engineering principles to get software that is reliable and works efficiently; IEEE 610.12 calls it 'application of a systematic, disciplined, quantifiable approach to the development, operation, and maintenance of software'

- these definitions are good, but they don't say *how* to do software engineering, so people understand software engineering differently

- SE often compared to civil engineering; in both,

  - size matters
  - team effort w/ planning
  - tough to change designs 

- civil engineering different b/c:

  - software can't leverage components
  - physics guides civil engineering

- software has axes of variability:

  - size
  - interaction / how people interact with it
  - requirements / stability or knowledge
  - reliability / need for it
  - security / need for it
  - portability
  - cost

- examples:

  |                     | MS word               | space shuttle | eBay                  |
  | ------------------- | --------------------- | ------------- | --------------------- |
  | **size**            | large                 | large         | moderate              |
  | **interactiveness** | high                  | low           | high                  |
  | **requirements**    | frequent new features | stable        | frequent new features |
  | **reliability**     | moderate              | very high     | moderate              |
  | **security**        | low                   | low           | high                  |
  | **portability**     | high                  | low           | low                   |
  | **cost**            | high                  | high          | low                   |

- lines of code:

  - OS X: 86 M
  - Win XP: 40 M
  - Open Office: > 10 M
  - Eclipse: > 10 M

- software gets worse; changes added, environment made change; called "bit-rot"

- things that don't work / are wrong approaches:

  - "books with rules are all we need"
  - "just add more programmers if we're behind"
  - "we can outsource it"
  - "we can refine requirements later"
  - "software can change later easily"
  - "write code now  (without planning)"
  - "can't assess quality until it's done"

- what questions are important? 

  - how will we know the system works?
  - how do we make it efficiently?

- problem 1: how do we know it works?

  - defects are common, more common than other engineering disciplines
    - space disaster ($7 B, 10 years) b/c software bug (64 bit float )
    - at&t long distance broke because of bad break statement in C
    - therac-25 race conditions killed patients with radiation
  - we need a specification separate from code to define what "works"
  - we need specifications because people generally implement incompatible components
  - write specs and:
    - write down what software should do
    - make sure everyone understands it
    - keep the specs up to date
  - specs still have ambiguities, but problem is made more manageable
  - specs let us check whether software works
  - methods to check software:
    - code reviews
    - static analysis tools
    - testing

- problem 2: how do we code efficiently?

  - assume we want to minimize time (time to market is a big pressure)
  - how to go faster? more programmers
  - parallel development:
    - make independent tasks for programmers / work on different modules
    - challenge: more people -> more communication
    - challenge: tasks can't be too fine-grained (communication overhead)
    - challenge: some inherent sequential constraints
  - interfaces:
    - interfaces make work independent, isolate components
    - interfaces shouldn't change much
    - they're a special kind of spec that defines boundaries between components / people
    - interfaces should be stable + everyone should understand them -> both require planning + time
    - let programmers handle internals individually
  - system decomposition into interfaces driven by:
    - **what** it does
    - **how** we build it
    - **who** builds it
  - **what**: applications often dictate natural decomposition; for example, compiler is a pipeline of lexer -> parser -> type checker -> optimizer
  - **how**: to build, we use scaffolding - extra code not part of final product (stubs, other ways of building and running partial systems)
  - **who**: architecture reflects organization that build it; e.g. 5 devs = 5 components
  - in summary:
    - decompose system into pieces
    - make good interfaces between pieces
    - pieces should be large
    - interfaces should specify boundaries of pieces

- SE boils down to a few issues:

  - specs: know what to do
  - design: plan to do it
  - programming: do it
  - validation: make sure it's right

- specs are important to define the problem, make sure everyone gets it

- other issues:

  - specs change
  - you can be wrong about what you want
  - the world changes

## Lesson 2: Software Process

