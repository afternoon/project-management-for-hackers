Project Management for Hackers
==============================

> "Why is it taking so long?"

98% of project management is outmoded, wrong-headed rubbish. 2% of project
management is essential for an organisation to function. Project management
is part of every hacker's job. If you're not doing it, either you're giving
your customers a terrible service or somebody else is having to do it for
you. Doing it yourself will give you more insight into the value engineers
have to their customers and make you a more valuable member of an
engineering team. It might even get you promoted.

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
responsible for the project's delivery or anyone else who might be
interested to know how things are going over in engineering.

What is project management?
---------------------------

Project management consists of 3 activities: 

- Scheduling tasks on to the set of available resources
- Tracking the status of tasks and thus of the project
- Sharing status information with stakeholders

Project managers are people who specialise in doing project management,
but anyone can do it.

Tasks
-----

Tasks are units of work, things like "add a search feature," "reduce the product
list page load time" or "support new database version."

Organisations use different nomenclature for tasks: user stories, features.

The set of tasks is often called the _project scope_.

Depending on the scope of the project, tasks may be simple things that take an
hour for one person to complete, or they may be projects in themselves, taking
multiple teams of people months or even years.

It's useful to apply project management at multiple levels. A programmer might
track a few different tasks they plan to work on during the day to deliver a
story. A team might track a couple of different stories that they're working on.
An organisation might track groups of stories grouped, describing them as
features, projects or epics. Project management at the organisational level is
sometimes called programme management.

Tasks are aggregates of multiple activities. The granularity of aggregation is
generally determined by the audience. Let's say a marketer is working on a
simple task: "tweet about our new home page redesign." It's not valuable to
break that down into subtasks like "open twitter.com," "login," "compose tweet"
etc, even for the marketer himself. As project information is shared with a
wider audience, the granularity decreases.

Resources
---------

Resources are things that do work. In software projects, resources are usually
humans and may be programmers, testers, designers, or a myriad of other roles.

In theory, at least, a resource can only work on one task at a time. However,
just as a single CPU interleaves processes, pausing those which are waiting for
IO tasks abstract asynchronous activities, so it's convenient to allow resources
to work on multiple tasks in parallel - . For example, the task "increase
available space on server 27b" might require ordering some new drives, waiting
for them to be delivered, installing them and so on.

Status
------

Processes (the operating system kind) can be in one of 5 different states [1](https://en.wikipedia.org/wiki/Process_state) at any given time. It's not so different for tasks.

- Created
- Waiting
- Running
- Blocked
- Terminated

Dependencies
------------

A task, _t_, has zero or more dependencies. If `task2` has a dependency on `task1`, then `task2` can not be completed until `task1` has been completed. It may be wasteful to begin work on `task2` before `task1` has completed.

Dependencies define a directed acyclic graph (DAG).

Tasks with dependencies are blocked until all their dependencies have been completed.

Scheduling
----------

Big upfront planned scheduling vs pull.

Tasks are scheduled into resources in much the same way processes are scheduled
on to CPUs.

"Baselining"

Affinity - resource1 worked on task1, so would be a good choice for task2.

Choosing what to work on
------------------------

- Bad: random selection, flavour of the month
- Good: qualititative scheduling algorithm
- Great: quantative scheduling algorithm using an economic frame (Don Reinertsen et al)

Reporting
---------

- Kanban boards (Google Sheets example)
- Gantt charts
- Tracker dashboards
- Oh my!

Scope, time, cost
-----------------

Fixed Deadlines
---------------

Organisations define deadlines for a number of reasons, some valid:

- An external party, a regulator for example, requires commitment to a deadline
- The organisation wants to model the costs of a project against cash flows and so picks an arbitrary completion date to plug into this model
- A commitment is necessary to persude a client to buy a product or service (this is a very risky practice)

And some invalid:

- A flawed estimation of the project duration outputs a completion date which then goes unchanged when scope and available resources change

Forecasting completion dates
----------------------------

Completion dates should be estimated by considering the set of tasks and resources, the ordering required by resource limits and dependencies and the estimated task durations. Let's call this _forward estimation_.

_Reverse estimation_ is the process of defining a completion date and then manipulating the tasks, resources and scheduling in to fit the required timeline. This is flawed.

- Overconfidence
- Peer pressure

An alternative to reverse estimation is to communicate a forward estimation then cut scope. A workshop is an effecient way of doing this as all the stakeholders can raise concerns then and there.

Adding resources to projects
----------------------------

[Amdahl](https://en.wikipedia.org/wiki/Amdahl%27s_law) observed that the speedup acheived by parallelising a program is a function of the proportion of time spent in the part of the program which can be parallelised. In a MapReduce operation, mapping and intermediate reductions may be [embarrassingly parallel](https://en.wikipedia.org/wiki/Embarrassingly_parallel), but the final reduction may resist parallelisation. If this final reduction takes a long time, the speedup available by parallelising everything else is only going to get you so far.

Adding resources to a project does not linearly impact the duration. [Brooks](https://en.wikipedia.org/wiki/Brooks%E2%80%99_law) observed that "adding manpower to a late software project makes it later." This is a simplification, but there are a number of factors that cause a non-linear relationship:

- Ramp up: it takes time for people added to a project to become productive. They need to be familiar with the project, the requirements, the code, the tools, the people, the process, etc. Some people may be familiar with the project, perhaps they were previously part of the team, others may be completely new, the learning curve is very steep for a newly hired and inexperiend contractor, for example.
- Helping new people become familiar with the project diverts members of the team from being productive themselves.
- New people might even make negative contributions, for example, if they introduce bugs that move the project further from completion and may require the existing team to spend more time fixing the issues
- Communication overheads increase as the number of people increases. Due to combinatorial explosion, the number of different communication channels increases rapidly with the number of people.[3] Everyone working on the same task needs to keep in sync, so as more people are added they spend more time trying to find out what everyone else is doing.
- Limited divisibility of tasks. Adding more people to a highly divisible task such as reaping a field by hand decreases the overall task duration (up to the point where additional workers get in each others way). Some tasks are less divisible; Brooks points out that while it takes one woman nine months to make one baby, "nine women can't make a baby in one month".
- Dependencies limit the degree of parallelism of tasks. If Steve wants to deploy the website, but Jenny hasn't built the server yet, then Steve must stand wait or context-switch to another task.

_(Parts of this section taken from the Wikipedia article on [Brooks' law](https://en.wikipedia.org/wiki/Brooks%E2%80%99_law).)_

Ideal person days: the days that a task might take if the person working on it didn't get distracted by anything else.

Software projects routinely go over time and budget. Task durations are known unknowns. It might take a day to redo the CSS for the home page, but a routine upgrade 

Forecasting algorithms
----------------------

Each task has an estimated duration. A naive forecast would take the graph of tasks to which can be associated a level of risk.
