# Topics for exam questions 

Good/hard questions: 
- 181030: 3bc, 4
- 191030: 1d, 2bcd, 
- 201028:
- 211029: 3c

## 191030

1. DFA, NFA, finite automata, longest match, rule priority
2. LL(1) parse table, LALR, BNF, context-free grammar, 
3. JastAdd, inh, eq, syn, visitor pattern, traversing visitor, stack, allocating memory

## 201028

1. Regex, DFA, NFA
2. Context free grammar, parse tree, equivalent LL(1), EBNF, LR-parsing ("stack • remaining inupt  action"), shift/reduce/accept
3. JastAdd, lookup pattern, synthesized attributes, inherited attributes 
4. root pointer, stack

## 211029

1. regex, DFA, NFA 
2. context free grammar, un-/ambiguous grammar, derivation tree, FOLLOW, EBNF, LL(1) 
3. JastAdd, lookup, abstract grammar, 
4. Stack, pointer, stack frames, stack pointer, frame pointer, dynamic links, local variables, arguments, the static links, frame pointer.

## Study 
- Visitors 
- Heap, stack, pointer etc.
  - dynlink
  - retaddr 
  - stack frames
  - stack pointer
  - frame pointer
  - dynamic links
  - local variables
  - arguments
  - the static links
- root pointer
- allocating memory
- LL(1) parse table
- LR parsing
- LALR
- visitor, traversing visitor
- lookup pattern
- FOLLOW, FIRST, NULLABLE

### x86

Some terms
- `push rbp` == push dynamic link, done in the begining of method
- `mov rsp rbp` == set new base pointer, done in the begining of method

- remember to pop arguments that is not used any more

### LL(1) parse table

#### FOLLOW: 

FOLLOW(X) is the set of tokens that can occur as the first token following X, in any sentential form derived from the start symbol S

```
FOLLOW(X) == ∪ FOLLOW(Y -> g X d ), 
  over all occurrences Y -> g X d

and where
FOLLOW(Y -> g X d ) == 
  FIRST(d) ∪ (if Nullable(d) then FOLLOW(Y) else ∅ fi)
```

#### FIRST:

FIRST(g) is the set of tokens that can occur first in sentences derived from g

```
FIRST(X) == FIRST(g1) ∪ ... ∪ FIRST(gn) 
  where X -> g1, ... X -> gn are all the productions for X in P

FIRST(sg) == FIRST(s) ∪ (if Nullable(s) then FIRST(g) else ∅ fi) 
  where s ∈ N ∪ T, i.e., s is a nonterminal or a termina
```

#### NULLABLE:

Nullable(g) is true iff the empty sequence can be derived from g, i.e.,
iff there exists a derivation g =>* epsilon

```
Nullable(X) == Nullable (g1) || ... || Nullable (gn)
  where X -> g1, ... X -> gn are all the productions for X in P

Nullable(sg) == Nullable (s) && Nullable (g)
  where s ∈ N ∪ T, i.e., s is a nonterminal or a terminal
```

How to construct the table:

```
initialize all entries table[X i, t j ] to the empty set.
for each production p: X -> g
  for each t ∈ FIRST(g)
    add p to table[X, t]
  if Nullable(g)
    for each t ∈ FOLLOW(X)
      add p to table[X, t]
```