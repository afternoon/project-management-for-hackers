Project Management for Hackers
==============================

> "Why is it taking so long?"

98% of project management is outmoded, wrong-headed rubbish. 2% of project
management is essential for all but the smallest organisations to function.

Data model
----------

A project, _p_, consists of a set of tasks, _T_, and a set of resources, _R_.

Tasks have a status. Tasks can depend on other tasks. Tasks can have
constraints on the type of resource that can work on them.

Tasks are worked on by resources. Resources have a set of abilities that
determine the tasks they can work on.

What is project management?
---------------------------

Project management is the activity of tracking the status of tasks and sharing
this information with anybody who's interested.

Tasks
-----

Tasks are units of work, things like "add a search feature," "reduce the product
list page load time" or "support new database version."

Organisations use different nomenclature for tasks: user stories, features.

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

https://en.wikipedia.org/wiki/Process_state

Created
Waiting
Running
Blocked
Terminated

Dependencies
------------

Scheduling
----------

Big upfront planned scheduling vs pull.

Tasks are scheduled into resources in much the same way processes are scheduled
on to CPUs.

"Baselining"

Choosing what to work on
------------------------

Bad: random selection, flavour of the month
Good: qualatitative scheduling algorithm
Great: quantative scheduling algorithm using an economic frame (Don Reinertsen
et al)

Reporting
---------

- Kanban boards
- Gantt charts
- Tracker dashboards
- Oh my!

Fixed Deadlines
---------------

Reversing back from the deadline X
Scope - time - quality triangle
