# ETH QHack Qilimanjaro Challenge (Red Squishy Fishy)

**Repository:** https://github.com/sunjerry019/ETH-QHack-Qilimanjaro

**Contributers:** Andrea Lizzit (EPFL), Yudong Sun (LMU/TU Munich), Giorgio Trespidim (Politecnico di Milano), Federico Simoni (Politecnico di Milano)


## Software Challenge

### A space-efficient QAOA solution for the traveling salesman problem
An instance of the traveling salesman problem is defined by a graph of $n$ nodes and weight matrix $\lambda_{ij}$ which defines the cost of travelling the path from node $i$ to node $j$. If there is no edge between such nodes, the weight is set to a very large value. A solution is given by a sequence of nodes $\{C_i\}_{i=0}^{n-1}$ where $C_i$ is the city visited at time $i$. We can define a cost function that produces the cost of traversing that path.
$$ \hat{H_4} = \sum_{j=0}^{n-2} \lambda_{C_j, C_{j+1}}$$
Through an injective map from the set of nodes to a set of orthonormal states $|A\rangle$ (city-states) the quantum Hamiltonian can be written as: $$\hat{H_4} = \sum_{j=0}^{n-2} \lambda_{A,B} (|A\rangle_i|B\rangle_j\langle A|_i\langle B|_j + |B\rangle_i|A\rangle_j\langle B|_i\langle A|_j)$$
For encoding the city-states, we need only $n \log(n)$ qubits. Indeed, there are $n!$ permutations of paths, so the lower bound grows as $\log(n!) = O(n\log(n))$. This lower bound can be reached by indexing each city with an index A from $0$ to $n-1$ and associating to the city the corresponding state $|A\rangle = |\text{bitstring}(A)\rangle$ where $\text{bitstring}(x)$ is the binary representation of $x$.

This allows us to greatly reduce the number of qubits required to solve the TSP problem. As a comparison, given $Q = 1000$ qubits:
- Using the $N^2$ encoding, we can solve for a problem with maximally 31 nodes.
- Using the $N \log N$ encoding, we can solve for a problem with a whopping 190 nodes.

To compute the circuit depth we start from recognizing that for each projector over a state $|A\rangle$ we need a depth $[\log(n)]$, where we take the ceiling of the number in brackets, and so the $H_4$ Hamiltonian takes up a depth of $[\log(n)]^2$. For the mixing Hamiltonian, we use the $X$ mixer. Finally, there are $t$ layers, so the final circuit depth ends up being $t(1 + [\log(n)]^2)$.

Mixing Hamiltonian:
$$\hat{H}_{enc\, \{i,j\},\{A,B\}}=|A\rangle_j |B\rangle_i \langle B|_j \langle A|_i$$

For more information and analysis, please refer to the Jupyter notebook.

## Hardware Challenge
The hardware challenge was not attempted during the Hackathon due to time constraints.
