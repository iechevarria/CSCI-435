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

    ​

## Lesson 2: Software Process

- process: framework of required tasks (e.g. waterfall, XP)

- methods: technical "how to" (e.g. design review, code review, testing)

- tools: automate processes and methods

- waterfall process phases:

  - 1)  gather requirements
    - write down what you have to do
    - talk to clients, users, customers - but they might not know what they need
    - purpose: build the right thing, gather information for planning
  - 2)  specification
    - **written document** that says *what* the system does in all circumstances, for all inputs, in each state
    - more comprehensive than requirements
  - 3)  design
    - system architecture
    - decompose system into modules; specify interfaces between modules
    - about *how* more than *what*
  - 4)  implementation
    - make a plan for order of build (by priority or testability) 
    - code and test each module
  - 5)  integration
    - put pieces together
    - QA makes sure to test full system
  - 6)  product
    - ship, start maintenance

- waterfall model outline:

  - a standard model where each stage leads to the next
  - test after each phase - verify requirements, spec, design, **not just code**
  - top-down design, bottom-up implementation

- waterfall model risks:

  - need to start with good requirements
  - little feedback until late 
  - problems in spec may be found very late
  - long time before first working versions seen (intermediate builds in general are good for confidence)
  - programmers have nothing to do until design is done

- professor's waterfall opinions:

  - waterfall adopted from other kinds of engineering
  - little software actually made this way
  - good: emphasis on spec, design, testing, communication through documents

- time is enemy of software:

  - tech becomes obsolete
  - competitors crop up
  - 3rd party pieces change
  - taking a long time to see product is therefore risky

- CA DMV software '87 - '93 was supposed to be \$8M, but became \$50M and never finished

- advantages of speed:

  - world won't change much
  - only near-term planning necessary

- rapid prototyping is an option because waterfall isn't fast

  - write a quick prototype
  - show it to users, refine requirements
  - proceed in waterfall (throw away prototype)

- prof's comments on rapid prototypes:

  - hard to get rid of prototype
  - prototype useful for refining requirements
  - exposes design mistakes
  - improves accuracy of plans

- prof's comments on reality:

  - neither model is accurate
  - actually feedback between all stages (design, spec, requirements can change)

- how to succeed with waterfall:

  - accept that later events will change early decisions, plan for change
  - minimize risk by identifying likely revisions, get fast feedback

- iterative models:

  - use same stages as waterfall, but iterate through full cycle several times
  - break project into build which lead from prototype to finished product
  - **gather requirements:** same as before, but without product, likely can't get full picture of requirements
  - **specification:** same as before, but recognize that it will evolve
  - **design:** 
    - same as before, but recognize where change happens and put abstraction there
    - incremental progress from skeletal component to full functionality
    - from most critical to least critical
  - **implementation (build 1):**
    - get skeleton working
    - all pieces there, none doing very much; all interfaces implemented
    - allows development of individual components to rely on interfaces only
  - **implementation (subsequent builds):**
    - after build 1, always have a demo to show to customer, team; bolsters communication
    - each build adds functionality
  - **integration:** 
    - major testing on each build - it's a stabilization point
    - happens until last build
  - advantages:
    - find problems from feedback to get idea of spec/design
    - more quantifiable than waterfall
  - disadvantages:
    - major mistakes in requirement, spec, design can happen b/c not as much time before build 1
    - can begin coding before problem fully understood

- in general, better to have product with feedback than to study problem in abstract

- in practice:

  - most SW dev uses iterative models (daily builds, system always working)
  - many hard-to-test systems still use waterfall (e.g. unmanned space probes)

- conclusions:

  - important to follow process

  - waterfall:

    - top-down design, bottom-up implementation
    - lots of upfront thinking, slow, tough to iterate

  - iterative:

    - build prototype quickly

    - postpone thinking

      ​

## Lecture 3: Extreme Programming

- SE is not civil engineering - SW is more organic, can expand 
- extreme programming (XP) addresses this
- goals:
  - minimize unnecessary work
  - maximize communication + feedback
  - make sure devs do most important work
  - make system flexible, ready to meet requirements
- history: Kent Beck wrote 1999 book "Extreme Programming Explained"
- **XP practices:** on-site customer, metaphor, planning, pair programming, small releases, testing, collective ownership, testing, CI, simple design, 40-hour week, refactoring, code standards
- **XP processes** (multiple short cycles, 2 weeks):
  1. meet with client to get requirements (user stories, acceptance tests)
  2. planning game (break stories to tasks, estimate costs); client prioritizes stories
  3. implementation - tests first, simplest design to pass tests, code in pairs, occasional refactoring
  4. evaluate progress, reiterate
- XP like iterative but taken to extreme
- XP customer:
  - expert customer part of team (onsite, always available)
  - customer involved in requirements, what to do next, acceptance tests (writes them), evaluates versions
  - this ideal may not always be feasible
- **user stories**
  - write on index cards or wiki; have meaningful title, are short
  - focus on "what" not "why" or "how" 
  - use client language (so client know what's happening)
  - not all stories needed in first iteration
  - **example:** CEO says "I need accounting SW where  I can make an account, list accounts, query account balance, delete account"; good user stories follow:
    - create account - I can create a named account
    - query account balance - I can query account balance
    - list accounts - I can get an *alphabetical* list of all accounts
    - delete account - I can delete a named account *if the balance is zero*****
  - **example:** not a user story - The user interface will use AJAX tech for online experience - because it's about the *how* and *why* not the *what*
  - customer must describe how user stories will be tested; tests can be for one or more stories
  - **example:** 
    1. if I make account "savings" and another "checking", and I ask for account list, I get "checking", "savings"
    2. if I create "checking" again, I get an error
    3. if I query balance of "checking", I get 0
    4. if I delete "stocks", I get an error
    5. if I delete "checking" it should not appear in list 
  - customer should write and be able to rerun tests
- **tasks**
  - every story broken into tasks to split work
  - stories are customer-focused, tasks are dev-focused
  - **example:** story is "I can create named accounts"; tasks are:
    - "ask user the name of the account"
    - "check if account exists"
    - "create empty account"
  - break down only enough to estimate costs; validate tasks with customer
  - if story has too many tasks, break it down
  - team assigns costs to tasks - relative cost is what matters, so use abstract units
  - experience will dictate what a unit is; devs can bid units to determine value
- **planning game**
  - customer chooses important stories for next release; devs bid on tasks
  - pick completion date, pick stories until budget full
  - customer may need to reprioritize
- **test-driven development** (TDD)
  - write unit tests (tests on one module) before implementing; check for good and bad behavior
  - TDD **clarifies** task, forces **simplicity**, acts as **documentation** (shows dev intent), increases **confidence**
  - if failing acceptance test, add user test and fix code to pass
  - if fail on beta, add more unit tests from scenario
  - **always write code to fix tests**
- simplicity
  - just-in-time design (only what you need now, don't worry about future)
  - no premature optimization
- **refactoring**
  - make code easier to read/use/modify
  - improving the design of code; needed b/c of limited early design
  - remove duplicated code - easier to change, understand
  - change names to suggest what method does / how it's used
    - method 1: rename method, fix compiler errors (takes a long time)
    - method 2: copy method with new name, make old one call new one, slowly change references ( allows you to run tests)
  - test suite needed for refactoring
  - only refactor working code
- CI: integrate work after each task, all unit test must run after integration (Travis does this)
- **pair programming**
  - one types, one monitors high-level issues (simplicity, integration, assumptions)
  - reveals early design problems
  - shuffle pairs periodically
  - results in better code, reduces risk, improves focus, helps learning + spread of good habits
  - programmers think they're too dumb or smart for it
  - managers don't do it because of programmer resistance + thinking it's inefficient
- **evaluation** at end of sprint
  - run acceptance tests
  - assess progress, discuss issues  (team and tech)
  - compute team speed, re-estimate user stories
  - plan w/ client for next iteration
- **unique characteristics of XP**
  - no analysts, architects, programmers, testers, integrators: every XP programmer does it all
  - no complete up-front analysis an design, just brief period in beginning and continuous iteration throughout development
  - develop infrastructure and frameworks with app, not up-front
- **use XP for:**
  - dynamic project in small teams
  - project w/ requirements prone to change
  - project w/ customer available
- **not for:**
  - requirements known and fixed
  - cost of late changes is high
  - customer not available
- requirements defined incrementally, so there can be scope creep
- design is on the fly, so there can be major redesigns
- customer rep might stink, so there's a single point of failure
- XP conclusions: incremental process for coping with change; never miss a deadline, just deliver less
- **agile SW dev**
  - from "Agile Manifesto" 2001
  - scrum project management + XP engineering
  - **team structure**
    - cross functional team (devs, testers, product owner, scrum master)
    - **product owner** (PO) drives product w/ business perspective; makes requirements, determines release date, leads iteration + release meetings; accepts / rejects work
    - **scrum master** (SM) ensures team productive, enables cooperation, tracks progress
  - team works to deliver user stories, keeps unfinished stories in backlog
  - iteration time fixed (1-4 weeks), stories chosen by priority/size/team capacity
  - stories -> collection of tasks, estimated in hours
  - story is done when all tasks completed (dev, test, doc), all acceptance tests run, accepted by PO
  - scrum has set of practices and predefined roles 
  - sprints planned by taking stories from backlog, team decides how much they can do; during sprint, backlog is frozen
  - daily 15 minute meetings happen to determine what's been done, what the plan for today is, what are the problems stopping goals
  - scrum of scrums after the scrum; meet with clusters of teams
  - **sprint meetings:** sprint planning, review, retrospective
- conclusion: no silver bullet (adaptation necessary)



## Lecture 4: An Introduction to Scrum

- agile process that gets working software quickly, business sets priorities
- people: Jeff Sutherland, Ken Schwaber, Mike Beedle, Mike Cohn
- constant duration sprint -> good rhythm 
- no changes during sprint
- scrum team does specs, design, code, test every sprint
- roles:
  - **product owner** defines features, decides release date, profitability, prioritizes features, accepts/rejects
  - **scrummaster** enacts scrum practices, shields team from external interferences, is management
  - **team** is self-organizing, membership changes only between sprints, is cross-functional, is full-time
- ceremonies:
  - **sprint planning** team selects items from backlog to complete, high level design is discusses, tasks identified, quantified
  - **daily scrum** daily 15 minute meetings not for problem solving, scrum roles have input; 3 questions: what did you do yesterday? what will you do today? anything in your way?; about **commitments**, not status updates
  - **sprint review** team talks about accomplishments, is a demo, 2-hour prep time rule, no slides, open to public, whole team talks
  - **sprint retrospective** look at what's working, what's not; 15-30 minutes; after each sprint, whole team talks, customer may attend; many ways of doing retrospective
- artifacts:
  - **product backlog** is requirements, list of all work to do on project, prioritized by PO each sprint
  - **sprint goal** statement of what work will be focused on during sprint
  - **sprint backlog** individuals sign up for work, never assigned; estimated work remaining updated every day
  - **burndown chart** show remaining work on graph
- scalability: team is 5-9 people, scale with teams of teams



## Lecture 5: Requirements

- requirements: descriptions of system services / constraints generated in engineering process - written for customers; should be high-level
- hardest part of making software is choose what to make
- requirements are about what the customer *needs*
- user requirements should be understandable by people without technical knowledge, should be defined in natural language, tables, diagrams
- need to determine stakeholders (people who benefit from system)
- **interviewing**:
  - can ask questions, listen to what they say/don't say
  - ask them to teach you what they do, watch task
  - in all interviews, get details - they can augment interview
  - should have other ways of getting info, too
- client writes user stories using their vocab; each story has acceptance tests
- **strawmen:** sketch product for the user/client
- **rapid prototyping:** major functionality superficially implemented, show to users
  - pitfalls: needs to happen fast, can become product, can serve as spec
  - if done well, very useful
- **system specification:** structured document setting out detailed descriptions of system functions; defines what should be implemented; can be part of contract
  - describes functionality completely
  - ideally unambiguous, complete, consistent
  - almost impossible goal
- user requirements -> client managers, end-users, engineers, contractor managers, sys architects
- sys requirements -> end-users, engineers, sys architects, SW devs
- informal specs are in natural language, can be bad
  - true formal specs time-consuming
  - customers can read them
- semi-formal specs use UML, more precision than natural language
- **functional requirements:** services system should provide, how system should react to inputs, should behave in situations
  - be specific in functional reqs
- **non-functional:** constraints on services or functions like time constraints, dev process, standards
  - programming language
  - dev method
  - I/O device capability
  - categories:
    - product requirements (speed, reliability)
    - organizational requirements (process standards)
    - external requirements (legal)
- **domain requirements:** reqs that come from app domain of system
  - example: Z39.50 standard user interface for database
  - example: delete documents b/c copyright restrictions
  - issues: understandability, implicitness
- guidelines for requirements:
  - use standard format for all requirements
  - use shall or must for mandatory, should for desirable
  - use emphasis on important bits
  - don't use jargon
- requirements and design are inseparable in practice
- reqs official statement of what's needed from devs; not a design document, should be about WHAT not HOW
- NL has drawbacks - ambiguity, not modular
- alternatives:
  - structured language spec: templates for requirements, can be done in a form
  - tabular spec can be used to supplement NL, useful when there are alternatives
  - sequence diagram: show sequence of events during user interaction, read top to bottom
  - interface spec: talk about interfaces, basically
- key points:
  - user reqs are high-level statements about what system should do
  - system specs communicate functions that system provides



##Lecture 6: Use Cases