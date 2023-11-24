---
layout: page
title: Hash Rank Join (HRJN)
---
# Hash Rank Join (HRJN)
Ilyas et al. (2003) presents a scheme for supporting top-_k_ joins in relational databases. The input to the scheme is a set of ranked relations, a join condition, and a monotone score combining function. The paper is an important one, and is nice an easy to read.

The paper then presents how this scheme can be translated into physical operators. The description of the Hash Rank Join (HRJN) operation contains an easy to fix bug for the _GetNext()_ operation shown in Table 2. We show the bug here, and suggest a fix.


## Bug
Let's say we the join condition `L.A = R.A`, and the score combining function `L.B + R.B` for the following two relations `L` and `R`:


    L
    --------------
     id | A  | B
    --------------
     1  | 1  | 5
    --------------
     2  | 2  | 4
    --------------
     3 | 3   | 2
    --------------

    R
    --------------
     id | A  | B
    --------------
     1  | 3  | 5
    --------------
     2  | 1  | 4
    --------------
     3  | 2  | 2
    --------------


    
The pseudocode for the _GetNext()_ operation in the paper (Table 2) will result in the threshold _T_ never going lower than `7 = Max((5+2), (2+5))`. This means that only the following two join results will be emitted (projected on the id and combined score columns):

    ----------------------
     L.id | R.id  | score
    ----------------------
     1    | 2     | 9
    ----------------------
     3    | 1     | 7
    ----------------------
    
whereas the join result

    ----------------------
     L.id | R.id  | score
    ----------------------
     2    | 3     | 6
    ----------------------
canot be emitted, since its score is 6, which is lower than 7, the minumum possible value for _T_.

## Fix
The fix seems simple. We need to add a check to see if the relations the operator is reading ran out of tuples. If this is the case for both relations, then we know that we can get join results only from the priority queue _Q_ and that the threshold _T_ is not important.

The changes to the pseudocode are as follows. The two occurrences of the statement:

    if(tuple.score ≥ T)
to

    if(tuple.score ≥ T OR (!L.hasNext() AND !R.hasNext()))
    
where `L.hasNext()` returns true if `L` has an unread tuple, and false otherwise

## References

Ihab F. Ilyas, Walid G. Aref, Ahmed K. Elmagarmid: _Supporting Top-k Join Queries in Relational Databases_. VLDB 2003.


