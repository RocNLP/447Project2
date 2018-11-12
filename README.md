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
|[APPLY-FORCE :agent ANIMAL] | [PUSH :agent PERSON :affected PHYS-OBJECT] | success | PUSH < APPLY-FORCE |
| |[PUSH :affected PHYS-OBJECT :agent PERSON]| success | role order doesn't matter|
| |[PUSH :affected PHYS-OBJECT :agent PHYS-OBJECT]| fail | not (PHYS-OBJECT < ANIMAL |
| |[PUSH :affected PHYS-OBJECT | fail | no "agent" role|
| |[EVENT-OF-ACTION :agent ANIMAL] | fail | not (EVENT-OF-ACTION < APPLY-FORCE) |

## Notes

Your code should be able to match nested structures of arbitrary depths, eg
```python
pattern = {
  "root": "WANT", 
  "experiencer": {"root": "PERSON"},
  "formal": {
    "root": "CONSUME",
    "agent": {"root": "PERSON"}
  }
}
```
is a valid pattern graph.  Note that we are using an extension of the `json` format for graphs from the last project for the patterns.  Each node is defined as a dictionary, with a guaranteed `"root"` element.  Any outgoing edges from a node are also included in the dictionary.  All the patterns we use here are trees.

However, the target graphs will be in the trips-json format outputted by `trips-web`.  You should store the `trips-web` output to files first (eg, `trips-web "this is a test sentence" > examples/sentence1.json`) and load them in your code.

Your code should take in a pattern graph and a target graph and output `true` or `false` based on whether the pattern matches or not.

## Provided starter code

I've written up a basic libarary for the Trips Ontology from the previous project.  Details on how to use it are available
in  `demo.ipynb`.  Additionally, [this repo](http://github.com/mrmechko/trips-web) allows you to access the Step Web Parser and retrieve a json formatted version of the parse.  You can install it via `pip install git+git://github.com/mrmechko/trips-web`.  Please report any problems with this code to me asap.  **Your code should be able to deal with target graphs in this format.**  See instructions on how to install.  You are not required to use the starter code if you don't want.  However, the `trips-web` tool should be useful for generating examples to work with.  Open issues for questions in the relevant repository.

Within reason, I will be happy to provide sample code demonstrating the basic functionality of the starter code and `trips-web` tool.

Sophie will hold office hours regarding coding issues from 5-6pm on Wednesday and Thursday.

## Report

* How could you use patterns to extract information? Describe the procedure.  
* What kind of facts can you extract? 
* What kind of questions can you answer? 
* What modifications would you have to make in order to answer simple questions?

## Submission

Submit your final code as a Jupyter notebook.  Your report can be included in the notebook.  
Submit a zip file containing all the relevant project files.  Your report should contain a description of any design
decisions you made and any issues you encountered.  Feel free to put additional non-notebook code in your submission if you want, just make sure to comment it well.

The first cell of your Jupyter notebook should have clear instructions on how to load a file containing a pattern graph and a file containing a target graph

eg

```
target_graph_file = "my_target_graph.json"
pattern_graph_file= "my_pattern_graph.json"
```

Additionally, include 3 pattern graphs, including one pattern with at least 2 levels of nesting (like the example above)
and 3 sentences that each pattern should match (for a total of 3 patterns and 9 sentences).

If I cannot just unzip and run your notebook, I will ask you to come and demonstrate your system in my office.  Barring reasonable unforseen circumstances, this will incur a penalty of 10%.

## Extra Credit

Implement the modifications for information extraction and question answering.  Describe how your system works.  You should be able to pose a question as a collection of pattern graphs and use the matching results to answer your question.  Demonstrate a few questions/answer pairs.  Make sure you describe any changes you make to the input format sufficiently for me to create more examples.
