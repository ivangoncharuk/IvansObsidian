#MATH-330 #fall2023 

# Probability Study Notes

## Probability Theory Concepts

### Experiment
- **Experiment**: A procedure with an uncertain outcome.
  
## Sample Space
- **Sample Space** ($S$): Set of all possible outcomes of an experiment.
  - **Coin Flip**: $S = \{\text{Heads, Tails}\}$, $n = 2$
  - **Six-Sided Die**: $S = \{1, 2, 3, 4, 5, 6\}$, $n = 6$
  - **Two Dice (Red, Green)**: 
    $$
    S = \{(1,1), (1,2), (1,3), \ldots, (6,5), (6,6)\}
    $$
    $$
    n = 36
    $$

## Event
- **Event**: A subset of the sample space, usually denoted by capital letters like $A$, $B$, $C$.
- An *event*, denoted as $A$, is a subset of the sample space $S$. 
- It collects outcome of a particular interest. The probability of an event A, $P(A)$ is obtained by summing the probabilities of the outcomes contained within the event $A$.
  - **Event A**: Sum equals 5 when rolling two dice
    $$
    A = \{(1,4), (2,3), (3,2), (4,1)\}
    $$

## Probability of Events

### Basic Probability Formula
- Probability of an event $A$: 
  $$
  P(A) = \frac{\text{\# of elements in } A}{\text{\# of elements in } S}
  $$
  - **Example**: $P(A) = \frac{4}{36} = \frac{1}{9}$

### Complement
- Complement of an event $A$ is denoted $A^c$
  $$
  P(A^c) = 1 - P(A)
  $$
  - **Example**: $P(A^c) = \frac{32}{36} = \frac{8}{9}$

## Union and Intersection
- **Union** ($\cup$): "or"
- **Intersection** ($\cap$): "and"
  
  - **Example**: 
    $$
    P(A \cup B) = P(A) + P(B) - P(A \cap B)
    $$
    $$
    = \frac{4}{36} + \frac{20}{36} - \frac{4}{36} = \frac{20}{36}
    $$

## Conditional Probability
- Example with a table:

 |             | Female | Male | Total |
 | ----------- | ------ | ---- | ----- |
 | Don't Smoke | 153    | 166  | 319   |
 | Smoke       | 16     | 27   | 43    |
 | Total       | 169    | 193  | 362   |


  - $P(\text{Female}) = \frac{169}{362}$
  - $P(\text{Smoke}) = \frac{43}{362}$
  - $P(\text{Female} \cap \text{Smoke}) = \frac{16}{362}$
  - $P(\text{Female} \cup \text{Smoke}) = \frac{196}{362}$
$P(\text{Female} \cup \text{Smoke}) =$
$$
     P(\text{Female}) + P(\text{Smoke}) - P(\text{Female} \cap \text{Smoke})
$$
$$
    = \frac{169+43-16}{362} 
    = \frac{196}{362}
$$

Refer to these notes for a quick review of probability concepts and formulas.

The event $A \cap B$ is the **intersection** of the events $A$ and $B$ and consists of outcomes that are contained within both events A and B. The probability of this event, $P(A\cap B)$ is the probability that both events $A$ and $B$ occur simultaneously. Sometime people just simply write it as $P(AB)$.

Important Formulas
>  "The probability of an event A, $P(A)$ is obtained by summing the probabilities of the outcomes contained within the event $A$."
- $P(A \cup B) = P(A) + P(B) - P(A\cap B)$
- If $A_1,...,A_n$ are mutually exclusive events, then the 
