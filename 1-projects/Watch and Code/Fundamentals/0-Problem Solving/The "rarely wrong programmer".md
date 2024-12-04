1. Devise a strategy from the top-down.
2. As a starting point, assume the strategy is _wrong_. Hunt for counterexamples over _many_ inputs. Pay special attention to inputs that seem tricky or problematic.
3. If a counterexample is found, stop and write a proof of incorrectness, then return to step 1.
4. Develop a proof of correctness (logical argument for _why_ the strategy is correct). If none can be found, go back and rethink the approach.
5. Hold that _IF_ the reasoning in the proof is valid, the strategy is correct.

Notice that the rarely wrong programmer writes proofs in **both** directions. The “sometimes wrong” programmer’s confidence is based entirely on how thoroughly they have tested their algorithm. Meanwhile, “rarely wrong” programmer’s confidence is based on the validity of their proofs.