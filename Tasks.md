# Tasks

## Issues
Issue tracking [here](https://github.com/calincru/iptables-sefl/issues).

## High-level
- [ ] Look into Z3 and potential optimizations in how it's used in Symnet
- [ ] Simple implementation of filtering in iptables (using only DROP/ACCEPT jumps):
    - [ ] Parse it and create an in-memory model (of iptables)
        - [ ] Make sure that some rules can only appear in some tables/chains.
    - [ ] Generate SEFL code (in-memory too)
    - [ ] Symbolically execute it

## Ideas
- [ ] Replace all `isValid' functions with something like `validate' (or
  semaValidate or the like) which returns a data structure aggregating useful
  data gathered during the semantic validation (such as the PlaceholderTarget
  to actual targets map).
    - [ ] Implementation wise, this could be a `Maybe <T>', with `None' meaning
    failure to validate that particular structure.
    - [ ] The nice part about this is that it is monadic (or applicative) in
      nature making the recursive validation easy.
        - [ ] The problem with this is that the validation function which call
          down the AST has to somehow 'merge' those `Maybe's.
        - [ ] A better solution is to add an implicit parameter which is that
          data structure (a semantic validation 'context') which is filled by
          recursively descending (and validating) the AST.