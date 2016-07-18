Project Management for Hackers
==============================

> "Why is it taking so long?"

Organisations are greater than the sum of their parts. They bring people
together and create valuable products and services for their customers. As
organisations grow, communication becomes more challenging. It becomes hard to
know who everyone is and what they're doing. This is a broad challenge, but
project management has a role to play. The goals of project management are to
work out what needs to be done to acheive big things and to communicate how
things are going to the rest of the organisation.

98% of project management is outmoded, wrong-headed rubbish. 2% of project
management is essential for an organisation to function. Project management is
part of every hacker's job. If you're not doing it, either you're giving your
customers a terrible service or somebody else is having to do it for you. Doing
it yourself will give you more insight into the value engineers have to their
customers and make you a more valuable member of an engineering team. It might
even get you promoted.

Data model
----------

A _project_ consists of:

- 1 or more _tasks_
- 1 or more _resources_
- 0 or more _stakeholders_
- 1 or more _outputs_ (or _deliverables_)

Tasks have a status. Tasks can depend on other tasks.

Tasks are worked on by resources. Resources have a set of _skills_ that
determine the tasks they can work on.

Outputs are the side-effects of resources working on tasks.

Stakeholders are people who depend on a project's outputs, are indirectly
responsible for the project's delivery or anyone else who might be interested to
know how things are going over in engineering.

Example
-------

- Resources: Alice, Ben, Carol, David
- Tasks:

Timeline:

```
+------------------------------------------------------------------------------+
| Alice                                                                        |
+------------------------------------------------------------------------------+
| Ben                                                                          |
+------------------------------------------------------------------------------+
| Carol                                                                        |
+------------------------------------------------------------------------------+
| David                                                                        |
+------------------------------------------------------------------------------+
```

What is project management?
---------------------------

Project management consists of 3 core activities:

- _Scheduling_ tasks on to the set of available resources
- _Tracking_ the status of tasks and thus of the project
- _Sharing_ status information with stakeholders, often by means of
  visualisation

Project managers are people who specialise in doing project management,
but anyone can do it.

A note on terminology: we use the term _scheduling_ according to the Computer
Science definition, as in process scheduling. In the project management
literature, the
_[schedule](https://en.wikipedia.org/wiki/Schedule_(project_management))_ is a
plan showing when each task will be completed by each resource. We refer to this
as _planning_.

The [agile manifesto](http://agilemanifesto.org/) values "responding to change
over following a plan." Scrum hangs on to planning, but constrains plans to 1
iteration in length. Iteration length varies, but is commonly 1-4 weeks. The
phrase _agile planning_ commonly refers to Scrum-style planning.

Cohn presents discusses both project and agile planning in [Agile Estimation and
Planning](https://books.google.co.uk/books?id=BuFWHffRJssC).

Pulling and pushing
-------------------

> "No plan survives contact with the enemy" -- Field Marshal Helmuth Graf von
> Moltke

There are 2 major classes of scheduling: pull systems in which resources take
tasks from a queue as they become available and push, in which an optimal
execution plan is created ahead of time and then followed. To avoid ambiguity I
will refer to this type of scheduling as planning.

> “In preparing for battle I have always found that plans are useless, but
> planning is indispensable.” -- Dwight D. Eisenhower

Planning is a 4th activity in project management. Organisations vary in the
amount of planning that they do. Lean organisations strive to avoid planning by
creating and optimising pull systems. [Soviet governments famously plan entire
economies](https://en.wikipedia.org/wiki/Soviet-type_economic_planning).
Planning is valuable for making concrete the vision for a project. Plans are one
way to answer the question "where are we trying to get to."

Tasks
-----

Tasks are units of work, things like "add a search feature," "reduce the product
list page load time" or "support new database version."

Organisations use different nomenclature for tasks: _user stories_, _features_.

The set of tasks is often called the _project scope_.

Depending on the scope of the project, tasks may be simple things that take an
hour for one person to complete, or they may be projects in themselves, taking
multiple teams of people months or even years.

It's useful to apply project management at multiple levels. A programmer might
track a few different tasks they plan to work on during the day to deliver a
story. A team might track a couple of different stories that they're working on
between them. An organisation might track groups of stories, describing them as
_features_, _projects_ or _epics_. Project management at the organisational
level is sometimes called _programme management_, the process of managing
multiple projects.

Under the hood, tasks themselves are aggregates of multiple activities. The size
of tasks is defined in relation to the target audience. Some stakeholders need
only know the status of a project as an enum (to do, doing, done), others need
to know the detail. Beyond some [Planck
length](https://en.wikipedia.org/wiki/Planck_length) finer granularity reduces
the value of project management. Let's say a marketer is working on a simple
task: "tweet about our new home page redesign." Breaking that down into subtasks
like "open twitter.com," "login," "compose tweet" etc, makes tracking and
communicating status excessively costly or ineffective.

Tasks are interruptible.

Resources
---------

Resources are things that do work. In software projects, resources are usually
humans and may be programmers, testers, designers, or a myriad of other roles.

In theory, at least, a resource can only work on one task at a time. However,
just as a single CPU interleaves processes, pausing those which are waiting for
IO, tasks abstract asynchronous activities which may become blocked. It's
convenient to allow resources to work on multiple tasks in parallel. The task
"increase available space on server 27b" might require ordering some new drives,
waiting for them to be delivered, installing them and so on. The task will
remain assigned to the same person who will likely make tea, then work on
another task.

Status
------

Processes (the operating system kind) can be in one of 5 different states
[1](https://en.wikipedia.org/wiki/Process_state) at any given time. It's not so
different for tasks.

- Created
- Waiting
- Running
- Blocked
- Terminated

Dependencies
------------

A task, _t_, has zero or more dependencies. If `task2` has a dependency on
`task1`, then `task2` can not be completed until `task1` has been completed. It
may be wasteful to begin work on `task2` before `task1` has completed.

Dependencies define a directed acyclic graph (DAG).

Tasks with dependencies are blocked until all their dependencies have been
completed.

Scheduling
----------

Big upfront planned scheduling vs pull.

Tasks are scheduled into resources in much the same way processes are scheduled
on to CPUs.

Choosing what to work on
------------------------

- Bad: random selection, flavour of the month
- Good: qualititative scheduling algorithm
- Great: quantative scheduling algorithm using an economic frame (Don Reinertsen
  et al)

Visualising project status
--------------------------

- Kanban boards (Google Sheets example)
- Gantt charts
- Tracker dashboards
- Oh my!
- Tracking dependencies

Scope, time, cost
-----------------

Uncertainty
-----------

Software projects routinely go over time and budget due to a number of sources
of uncertainty and overconfidence.

Task durations are known unknowns. It might take a day to change the navigation
CSS for the home page, but a conflict between some `!important` rules might
require a developer to rewrite all the styles for the page, meaning the task
takes much longer.

The expected set of tasks is likely a subset of the actual required set of
tasks. There is an additional set of tasks which are unknown unknowns. As
resources work on tasks, they discover new dependencies. These dependencies are
part of the project scope. It's common for this additional scope to go
undocumented leading stakeholders to question the perceived disparity between
the duration of a project and the documented scope.

Some techniques for dealing with task duration uncertainty include:

- Estimating task duration by disaggregating the task into sub-tasks reduces
  uncertainty
- Estimating task durations as a group increases the pool of available knowledge
  and provides calibration across tasks
- Limiting the maximum acceptable estimate forces tasks to be broken down into
  smaller tasks which can be estimated with higher certainty

Implicit dependency uncertainty is harder to deal with. One approach is
[reference-class
forecasting](https://en.wikipedia.org/wiki/Reference_class_forecasting) which
we'll consider later.

Incidentally, the process of working on implicit dependencies is known as
[yak-shaving](http://www.hanselman.com/blog/YakShavingDefinedIllGetThatDoneAsSoonAsIShaveThisYak.aspx).

Risk
----

Classes of risk in project management: requirements risk, 3rd party risk.

Risk logs.

http://blog.scottlogic.com/2014/09/10/does-scrum-make-project-managers-redundant.html

Estimation
----------

Ideal person days: the days that a task might take if the person working on it
didn't get distracted by anything else.

Fixed Deadlines
---------------

Organisations define deadlines for a number of reasons, some valid:

- An external party, a regulator for example, requires commitment to a deadline
- The organisation wants to model the costs of a project against cash flows and
  so picks an arbitrary completion date to plug into this model
- A commitment is necessary to persude a customer to buy a product or service (a
  risky practice in software)

And some invalid:

- A flawed estimation of the project duration outputs a completion date which
  then goes unchanged when scope and available resources change
- An unnecessary commitment is volunteered to an external party

Forecasting completion dates
----------------------------

Completion dates should be estimated by considering the set of tasks and
resources, the ordering required by resource limits and dependencies and the
estimated task durations. Let's call this _forward estimation_.

_Reverse estimation_ is the process of defining a completion date and then
manipulating the tasks, resources and scheduling in to fit the required
timeline. The aggregate effects of overconfidence, peer pressure, task duration
uncertainty and implicit dependency uncertainty frequently cause reverse
estimates to be wrong by a significant degree.

An alternative to reverse estimation is to communicate a forward estimation then
cut scope. A workshop is an effecient way of doing this as all the stakeholders
can raise concerns then and there.

Adding resources to projects
----------------------------

[Amdahl](https://en.wikipedia.org/wiki/Amdahl%27s_law) observed that the speedup
acheived by parallelising a program is a function of the proportion of time
spent in the part of the program which can be parallelised. In a MapReduce
operation, mapping and intermediate reductions may be [embarrassingly
parallel](https://en.wikipedia.org/wiki/Embarrassingly_parallel), but the final
reduction may resist parallelisation. If this final reduction takes a long time,
the speedup available by parallelising everything else is only going to get you
so far.

Adding resources to a project does not linearly impact the duration.
[Brooks](https://en.wikipedia.org/wiki/Brooks%E2%80%99_law) observed that
"adding manpower to a late software project makes it later." This is a
simplification, but there are a number of factors that cause a non-linear
relationship:

- Ramp up: it takes time for people added to a project to become productive.
  They need to be familiar with the project, the requirements, the code, the
  tools, the people, the process, etc. Some people may be familiar with the
  project, perhaps they were previously part of the team, others may be
  completely new, the learning curve is very steep for a newly hired and
  inexperiend contractor, for example.
- Helping new people become familiar with the project diverts members of the
  team from being productive themselves.
- New people might even make negative contributions, for example, if they
  introduce bugs that move the project further from completion and may require
  the existing team to spend more time fixing the issues
- Communication overheads increase as the number of people increases. Due to
  combinatorial explosion, the number of different communication channels
  increases rapidly with the number of people.[3] Everyone working on the same
  task needs to keep in sync, so as more people are added they spend more time
  trying to find out what everyone else is doing.
- Limited divisibility of tasks. Adding more people to a highly divisible task
  such as reaping a field by hand decreases the overall task duration (up to the
  point where additional workers get in each others way). Some tasks are less
  divisible; Brooks points out that while it takes one woman nine months to make
  one baby, "nine women can't make a baby in one month".
- Dependencies limit the degree of parallelism of tasks. If Steve wants to
  deploy the website, but Jenny hasn't built the server yet, then Steve must
  either wait or context-switch to another task.

_(Parts of this section taken from the Wikipedia article on [Brooks'
law](https://en.wikipedia.org/wiki/Brooks%E2%80%99_law).)_

Planning algorithms
-------------------

### Critical Path Method

https://en.wikipedia.org/wiki/Critical_path_method

"Crash duration"

### Naive

Each task has an estimated duration. A naive forecast would take the graph of
tasks, schedule them to the resources, respecting those resources skills, and
take the completion date of the last task as the project completion date.

### Risk-adjusted

Task duration estimates are uncertain. The duration uncertainty can also be
estimated and used to inflate duration estimates. An estimate with a medium
degree of uncertainty may be doubled, an estimate with a very high degree of
uncertainty might be multiplied 5 times. This probabalistic approach to reducing
the error in a forecast is flawed. Software projects are vulnerable to
combinatorial explosion of complexity leading to very large blow ups in
duration. In practice, long- or even mid-term planning is extremely error-prone
and is strongly discouraged by the agile community amongst others.

### Monte Carlo

Another approach is to do a monte-carlo simulation.

### Logic programming approach

https://en.wikipedia.org/wiki/Job_shop_scheduling
http://neuron-ai.tuke.sk/schmotze/Optimal_Scheduling_Using_Constraint_Logic_Programming.pdf
http://4c.ucc.ie/~hsimonis/Scheduling%20and%20Planning%20with%20Constraint%20Logic%20Programming.pdf
https://en.wikipedia.org/wiki/Fixed-priority_pre-emptive_scheduling

Context-switching

[Reference-class
forecasting](https://en.wikipedia.org/wiki/Reference_class_forecasting)

"Rebaselining"

Affinity - resource1 worked on task1, so would be a good choice for task2.

[Slack, float](https://en.wikipedia.org/wiki/Float_(project_management))

Don't forecast, course-correct
------------------------------

Kanban, XP, agile.

Tools
-----

COMPROMAN: COMputerised PROject MANager

- Forward estimator
- Monte carlo simulation
- Dependency graphers
- Backlog and kanban board in Google Sheet

Appendix 1: Primer on process scheduling
----------------------------------------

Throughout this book, I compare scheduling in project management to how
processes are scheduled on to CPUs. Here's a quick primer in case you haven't
come across this area of operating systems implementation before.

TODO
- https://en.wikipedia.org/wiki/Process_state
