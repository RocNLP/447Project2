# 447Project2

**Due Sunday, November 18th, 11:59 pm**

## Description

Expanding on the ideas from Project 1, write a program that can match a smaller pattern graph to a larger target graph.
A pattern graph matches if every node and arc can be aligned to a corresponding node or arc in the target graph.
In particular, if an arc from the pattern graph aligns to an edge in the target graph, then they must have the same label and
the nodes at the end points of the arcs must also align.  Take into account the type hierarchy for nodes.

The graphs are simplified versions of the full logical form, containing only types and roles.

## Examples

|pattern  |target   |result   |reason   |
|---------|---------|---------|---------|
|[APPLY-FORCE :agent ANIMAL] | [PUSH :agent PERSON :affected PHYS-OBJ] | success | PUSH < APPLY-FORCE |
| |[PUSH :affected PHYS-OBJ :agent PERSON]| success | role order doesn't matter|
| |[PUSH :affected PHYS-OBJ :agent PHYS-OBJECT]| fail | not (PHYS-OBJ < ANIMAL |
| |[PUSH :affected PHYS-OBJ | fail | no "agent" role|
| |[EVENT-OF-ACTION :agent ANIMAL] | fail | not (EVENT-OF-ACTION < APPLY-FORCE) |

## Notes

Your code should be able to match nested structures of arbitrary depths, eg
```
[WANT 
  :experiencer PERSON
  :formal [CONSUME
              :agent PERSON
          ]
]
```
is a valid pattern graph.

## Provided starter code

I've written up a basic libarary for the Trips Ontology from the previous project.  Details on how to use it are available
in  `demo.ipynb`.  Additionally, [this repo](http://github.com/mrmechko/trips-web) allows you to access the Step Web Parser and retrieve a json formatted version of the parse.  See instructions on how to install.  You are not required to use either if you don't want.  However, the `trips-web` tool should be useful for generating examples to work with.  Open issues for questions in the relevant repository.  Sophie will hold office hours regarding coding issues from 5-6pm on Wednesday and Thursday.

## Report

* How could you use patterns to extract information? Describe the procedure.  
* What kind of facts can you extract? 
* What kind of questions can you answer? 
* What modifications would you have to make in order to answer simple questions?

## Submission

Submit your final code as a jupyter notebook.  Your report can be included in the notebook.  
Submit a zip file containing all the relevant project files.  Your report should contain a description of any design
decisions you made and any issues you encountered.  Feel free to put additional non-notebook code in your submission if you want, just make sure to comment it well.

Additionally, include 3 pattern graphs, including one pattern with at least 2 levels of nesting (like the example above)
and 3 sentences that each pattern should match (for a total of 3 patterns and 9 sentences)

## Extra Credit

Implement the modifications for information extraction and question answering.  Describe how your system works.  You should be able to pose a question as a collection of pattern graphs and use the matching results to answer your question.  Demonstrate a few questions/answer pairs.
