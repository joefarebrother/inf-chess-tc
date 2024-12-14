A **strategy** for a player P from a starting board B is a function that takes a sequence of legal moves from B for which it's P's turn and outputs a legal move for P. 
A strategy is **computable** if it's a computable function.
A strategy for P **wins** against a strategy P' for the other player if playing the strategies against each other (i.e. building a sequence of moves by calling the appropriate strategy function with the sequence so far at each step) results in P winning in a finite number of moves. 
A strategy is a **winning strategy** if it wins against *all* opposing strategies. 
(a weaker notion in which you only must win against all *computable* strategies can be considered; and the difference is meaningful for some infinite chess positions. [TODO: reference]. this notion wil not be considered here.)

For a system to be "Turing complete" is not a very precise concept especially when there's no notion of the system "running by itself". 
Typically what is meant is "some interesting question about the system is undecidable (via reduction to the halting problem)"
For infinite chess, this question will be "Does white have a (computable) winning strategy?"

I will aim to prove the following strongest reasonable definition for TC:

- There is a *computable* function that takes a turing machine M, and returns a board `B` and a computable strategy `s` for white, such that the following are equivalent:
- - M halts 
- - `s` is a winning strategy 
- - The game value for white is a finite ordinal (i.e. no "mate in omega" type situations, plus white has a winning strat that's not necessarily computable) [TODO: ref for game value]

Chess rules:
- normal piece movement
- for 3d, generalisations are explained there
- no castling, promotion, pawn doublemoves, en passant
- you win when you capture any opposing king. there can be multiple kings per side.
- for simplicity, check and checkmate are removed from win conditions (and are just shorthand for "threatens a win in 1" and "has an unstoppable win in 1")
- stalemate can also be removed, no legal moves = you lose. 
- these modifications to check, checkmate, and stalemate don't actually affect the results. positions are constructed to always have a legal move that doesn't put one in check so the stalemate rule is actually irrelevant. 