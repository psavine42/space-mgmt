

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
    
3) Task based scheduling stuff is fundamentally a graph. 

## Questions 
    
1) is there any use to to thinking about vspace as a manifold, and do some trickery 
to clump physical dimensions onto it, and think of each task as some of the dimensions of that space?

2) There is also a space of things that happen outside of software - human space: H

3) Example - Change order approval
    1) some event happens in H implying a change in some Existing task in T in P.
    2) a record is create (pco = Rp) is created in V, connected to another record (cco = Rc) in V. 
    3) an approval process takes place for both Rp and Rc which can be thought of as a mapping Rc -> Rc', Rp -> Rp'
    4) an invoice is sent as a record in V (Ri)
    5) work happens in P, and record added in V
    6) invoice is paid: Ri -> Ri'
    
how would this be reprsented, and gathered concretely? 
    1)  assumption: initial record T must exist , and T ∈ V, T ∈ P
    2)  
    
        # lets say this step relates to the 'project management' dataset 
        # Rc is picked up from database (same with Rp)
        Rc, Rp = scan_dbs()
        
        new_record(Rc)
        new_record(Rp)
        
        def new_record(R)
            # mapping is generated to tasks in V space:
            R' = relate_V(R, V)
            
            # mapping is generate to something in P space
            # where P' is new representation of P with R' record related to some P-record
            R'', P' = relate_P(R', P)
            
            # update task with new information from RC
            T' = T U R''
            
            # (maybe) find possible paths for the record to take
            # or alternatively, apply some predefined path to initialize future records
            generate_paths_for(R'') 
                
            # update summary metrics 
            update_metrics(R'', T' P')

        # procedures used 
        def relate_V :: abstract interface
        def relate_P :: abstract interface
        def scan_dbs :: abstract interface
        def update_metrics :: 
        
    3)  record is updated, but we are dealing with same record
        # upon db scans - some changes are picked in the Rc record (eg it is approved)
        Rc_upd = scan_dbs()
        updated_record(Rc_upd)
        
        def updated_record(R'):
            # get the current state of the record, and expectred next paths previously generated
            R, exp = current_state(R')
            
            # if this was expected - awsome
            if R' ∈ apply_step(R, exp):
                # perhaps update expecations 
                
            else:
                # somthing else happened - is there any reason to handle these ? 
                # probably not for now, but can be useful for 
            
            # apply and save as new R
            R'' = apply_step(R, R')
            
            generate_paths_for(R'')
            update_metrics(R'', T' P')
    
    4)  lets say this step relates to the 'accounting' dataset
        now for this step, it is in real case more difficult (as invoice record is not tied to current)
        We can approach this in a few ways. 
        1) define the types of 'next records' to look for, and do some ridiculous pattern mathing over time. 
        2) #todo i had 3 when i started the list, but got distracted  
            
    5)  # lets say this step relates to the 'schedule' dataset 
        # same as step (4), but with changes to particular scheduling records
        
        
    6)  same as step(4)
    
        
now the guts of relate_P, the difficulty of relating unlabeled model space to text space.


## misc 
    
Can physical space be abstracted into just space (with som preference in viz phase?) 
    
aka - can we get build task tree just on db (eg timberline state walk idea)

what is the idea of walking the financial state space. Each entry has an opposite entry somewhere. 
There exist flows 


## unrelated 

Tensile forces between N rows in M columns of a table.
lets say two columns are normalized and sorted, and both are ordered:
F = 0

    0   |   0
    0.1 |   0.1
    0.2 |   0.2
    ... |   ...
    ... |   ...
    1.0 |   1.0
    
now if both are normalized and sorted and max(c1)_i = min(c2)_i, max2(c1)_i = min2(c2)_i
then F = 1.

    0   |   1.0
    0.1 |   ...
    0.2 |   ...
    ... |   0.2
    ... |   0.1
    1.0 |   1.0
    
How to think about many 'columns' acting on each other like a tensigrity structure? 
Can this be extended to discrete data ? 
    
    