# perplexity-permutation-puzzle-2024

## Objective
Minimize the perplexity of text sequences by rearranging jumbled words into coherent sentences. Lower perplexity means better fluency and semantic coherence.

## Solution
A solution is represented by a permutation of words or elements in an order that aims to minimise perplexity . Each permutation represents a different configuration of the set of words.

## Objective Function
The objective function for this problem, as calculated by the Gemma 2 9B model, evaluates the quality of a permutation of words in a sequence. The goal is to minimize the perplexity of the rearranged sequence.

## Solution Space
The solution space is defined by all possible permutations of the elements. For a set of `n` words, the solution space comprises `n!` permutations.

1. Components of the Solution Space
    For each sequence in dataset the words represent the elements in the solution, Then solution space is the set of all permutations of these words
    for example: for the sequenace: `{w1,w2,w3}` the space is 
    `{{w1,w2,w3}, {w1,w3,w2}, {w2,w1,w3}, {w2,w3,w1}, {w3,w1,w2}, {w3,w2,w1}}`
    it's of size `3!=6`

2. Characteristics of the Solution Space
    - Discrete: Each solution is a distinct permutation of words.
    - Combinatorial Explosion: The size of the solution space grows factorially with the number of words in each sequence.

3. Constraints on the Solution Space
    - **Validity**: Each solution must be a valid permutation of the corresponding base sequence. No additions, deletions, or duplicates are allowed.
    - **Optimization Objective**: Search for the permutation that minimizes the perplexity score for each sequence

## Type of Problem : Combinatorial
The problem is **combinatorial** in nature since the solutions are defined by permutations of discrete elements (words). Each solution is a finite set of possible choices, and the search for an optimal solution involves exploring these solutions.

## Metaheuristics

- **Solution**:
  - word sequence

- **Movements**
    1. **Word Swaps**: Swap two words in the sequence to create a new permutation.
        - Example:
            - Original Sequence: `["Rudolph", "sleigh", "with", "reindeer"]`
            - After Swap: `["Rudolph", "with", "reindeer", "sleigh"]`
            - In this case, we swap "sleigh" and "with", which might lead to a more fluent sequence.
    
    2. **Mutation**: Introduce a random change in the sequence. This could involve shuffling a group of words or performing a series of swaps to create a new permutation.
    - Example:
        - Original Sequence: `["Santa", "claus", "is", "coming"]`
        - After Mutation: `["coming", "is", "Santa", "claus"]`
        - Here, a more substantial change is made compared to a simple swap. A larger portion of the sequence may be shuffled or rearranged.

    3. **Selection**: After generating several permutations, **selection** is the process of choosing the best-performing permutations based on their perplexity score. The best permutations (those with the lowest perplexity) are retained for further exploration.
    - Example:
        - Sequence 1: `["the", "reindeer", "sleigh"]` → Perplexity: 10
        - Sequence 2: `["the", "sleigh", "reindeer"]` → Perplexity: 8
        - Sequence 3: `["reindeer", "the", "sleigh"]` → Perplexity: 12
        - After selection, Sequence 2 would be kept as it has the lowest perplexity (8).

    4. **Insertion**: Insert a word into a new position in the sequence, potentially creating a better flow. This is similar to a **mutation** but focuses specifically on the insertion of one word at a time, rather than shuffling or swapping multiple words.
    - Example:
        - Original Sequence: `["Santa", "is", "coming"]`
        - After Insertion: `["Santa", "coming", "is"]`
        - Here, we moved "coming" closer to "Santa," which might make the sentence sound more natural.

- **Evaluation**:
  - Evaluation is performed by calculating the perplexity for each generated sentence, allowing the quality of the solution to be determined and guiding the optimization process.
  - will be calculated basing on the [gemma-2-9b](https://www.kaggle.com/models/google/gemma-2/Transformers/gemma-2-9b/2) model

## Algorithme