

## Concept

We want to track tasks in physical space. Information about these tasks exiost in several
software systems (databases) . 
    
Databases can be thought of spaces as well (dimensions of table, 
row, some of which are continous, some discrete)
    
therefore we can unify phyiscal and virtual space into a single notion with two types. 
    
Each task has normal predecessors in physical space, but also in virtual space.  
A task in physical space can be represented 1-to-1 in virtual space, but also as 1to many and many to 1 in vspace. 
The virtual space is All Database schemas which hold precursor information to a task 
    
Each task has an equivelant 'reaction' or 'double-entry' in the managers court 

- The target is to be able to explore completion of a project in physical and virutal space. 
    
- The model should be amenable to probobalistic analysis for prediction and such 
    

## Structure

Components:
    
1) Interface to arbitrary databases / apis on which checkpoints can be defined
    
2) Interface to abstract phyiscal space - eg revit model , drawings, etc. 
    
3) Mechanism for defining checkpoints, and connecting them as successors and predecessors
    - this may have to be a pure ML model, but maybe not necessary - either way
        
4) Mechanism for MLing characteristics of space to match data 
     - aka - I have some RFIS, connected to blah in my model. How to attach full tree


## Interface

1) view everything as a big table such as
    
        Room   |  Concrete   | Roughing | ...
        -------+-------------+----------+------
        lobby  |    100%     |   30%    | ...
    
Each task can be drilled into eg Roughing
    
        Room    |  Task      | procurement | submittal | install
        -------+-------------+-------------+-----------+----------
        lobby  |   Roughing  |   100%      | 80 %      |   40 %
    
Or pivoted out: 
    
        Room   |  Concrete   |            Roughing                | ...
               |             | procurement | submittal | install  |
        -------+-------------+-------------+----------------------+-----
        lobby  |    100%     |   100%      | 80 %      | 40 %     |
    
    
2) view things in space as some sort of stacked layer thing on the 3D model/drawings.



## Properties 

Some ideas for starting assumptions:

1) Each checkpoint relates to atleast one physical space (converse not true)
        -> map max probability of any single space | previous similar checkpoint types
    
2) money | abstact-space ~ sqft | physical-space ????
    
3) 

## Questions 
    
1) is there any use to to thinking about vspace as a manifold, and do some trickery 
to clump physical dimensions onto it, and think of each task as 
   
   
## misc 
    
Can physical space be abstracted into just space (with som preference in viz phase?) 
    
aka - can we get build task tree just on db (eg timberline state walk idea)

what is the idea of walking the financial state space. Each entry has an opposite entry somewhere. 
There exist flows 


## unrelated 

Tensile forces between N rows in M columns of a table.
lets say two columns are normalized and sorted, and both are ordered:
F = 0
    
now if both are normalized and sorted and max(c1)_i = min(c2)_i, max2(c1)_i = min2(c2)_i
then F = 1.
    
How to think about many 'columns' acting on each other like a tensigrity structure? 
    
    