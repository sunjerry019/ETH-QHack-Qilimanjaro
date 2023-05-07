# ETH QHack Qilimanjaro Challenge (Red Squishy Fishy)

**Repository:** https://github.com/sunjerry019/ETH-QHack-Qilimanjaro

**Contributers:** Andrea Lizzit (EPFL), Yudong Sun (LMU/TU Munich), Giorgio Trespidim (Politecnico di Milano), Federico Simoni (Politecnico di Milano)


## Software Challenge

### N^2 Solution Implementation
With reference to https://cs269q.stanford.edu/projects2019/radzihovsky_murphy_swofford_Y.pdf, we implement the version using the $N^2$ encoding method. Unfortunately, we did not get very far with this method. The results and implementations may be seen at 

```Software Challenge/TSP_introductory_challenge_two.ipynb```

### A space-efficient QAOA solution for the traveling salesman problem
An instance of the traveling salesman problem is defined by a graph of $n$ nodes and weight matrix $\lambda_{ij}$ which defines the cost of travelling the path from node $i$ to node $j$. If there is no edge between such nodes, the weight is set to a very large value. A solution is given by a sequence of nodes $\{C_i\}_{i=0}^{n-1}$ where $C_i$ is the city visited at time $i$. We can define a cost function that produces the cost of traversing that path.
$$ \hat{H_4} = \sum_{j=0}^{n-2} \lambda_{C_j, C_{j+1}}$$
Through an injective map from the set of nodes to a set of orthonormal states $|A\rangle$ (city-states) the quantum Hamiltonian can be written as: $$\hat{H_4} = \sum_{j=0}^{n-2} \lambda_{A,B} (|A\rangle_i|B\rangle_j\langle A|_i\langle B|_j + |B\rangle_i|A\rangle_j\langle B|_i\langle A|_j)$$
For encoding the city-states, we need only $n \log(n)$ qubits. Indeed, there are $n!$ permutations of paths, so the lower bound grows as $\log(n!) = O(n\log(n))$. This lower bound can be reached by indexing each city with an index A from $0$ to $n-1$ and associating to the city the corresponding state $|A\rangle = |\text{bitstring}(A)\rangle$ where $\text{bitstring}(x)$ is the binary representation of $x$.
We use the $X$ mixer Hamiltonian and set as the input state the maximal superposition state $H^{\otimes n} |0\rangle^{\otimes n}$.

This allows us to greatly reduce the number of qubits required to solve the TSP problem. As a comparison, given $Q = 1000$ qubits:
- Using the $N^2$ encoding, we can solve for a problem with maximally 31 nodes.
- Using the $N \log N$ encoding, we can solve for a problem with a whopping 140 nodes.

To compute the circuit depth we start from recognizing that for each projector over a state $|A\rangle$ we need a depth $[\log(n)]$, where we take the ceiling of the number in brackets, and so the $H_4$ Hamiltonian takes up a depth of $[\log(n)]^2$. For the mixing Hamiltonian, we use the $X$ mixer. Finally, there are $t$ layers, so the final circuit depth ends up being $t(1 + [\log(n)]^2)$. 


For more information and analysis, please refer to the Jupyter notebook. The results and implementations may be seen at 

```Software Challenge/TSP_introductory_challenge.ipynb```

## Hardware Challenge
The hardware challenge was not attempted during the Hackathon due to time constraints.
