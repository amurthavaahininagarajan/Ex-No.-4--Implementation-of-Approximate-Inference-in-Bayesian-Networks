# Ex-No.4 Implementation of Approximate Inference in Bayesian Networks
## Aim : 
   To construct a python program to implement approximate inference using Gibbs Sampling.

## Algorithm:

Step 1: Bayesian Network Definition and CPDs:<br>
(i) Define the Bayesian network structure using the BayesianNetwork class from pgmpy.models.<br>
(ii) Define Conditional Probability Distributions (CPDs) for each variable using the TabularCPD class.<br>
(iii) Add the CPDs to the network.<br>
Step 2: Printing Bayesian Network Structure:<br>
(i) Print the structure of the Bayesian network using the print(network) statement.
Step 3: Graph Visualization:<br>
(i)Import the necessary libraries (networkx and matplotlib).<br>
(ii)Create a directed graph using networkx.DiGraph().<br>
(iii)Define the nodes and edges of the graph.<br>
(iv)Add nodes and edges to the graph.<br>
(v) Optionally, define positions for the nodes.<br>
(vi) Use nx.draw() to visualize the graph using matplotlib.<br>
Step 4: Gibbs Sampling and MCMC:<br>
(i) Initialize Gibbs Sampling for MCMC using the GibbsSampling class and provide the Bayesian network.<br>
(ii)Set the number of samples to be generated using num_samples.<br>
Step 5: Perform MCMC Sampling:<br>
(i)Use the sample() method of the GibbsSampling instance to perform MCMC sampling.<br>
(ii)Store the generated samples in the samples variable.<br>
Step 6: Approximate Probability Calculation:<br>
(i) Specify the variable for which you want to calculate the approximate probabilities (query_variable).<br>
(ii)Use .value_counts(normalize=True) on the samples of the query_variable to calculate approximate probabilities.<br>
Step 7:Print Approximate Probabilities:
(i) Print the calculated approximate probabilities for the specified query_variable.<br>

## Program :
```
DEVELOPED BY: AMURTHA VAAHINI.KN
REGISTER NO: 212222240008
```
Import the necessary libraries
```
from pgmpy.models import BayesianNetwork
from pgmpy.factors.discrete import TabularCPD
from pgmpy.sampling import GibbsSampling
import networkx as nx
import matplotlib.pyplot as plt
```
Define the Bayesians network Structure
```
network=BayesianNetwork([('Burglary','Alarm'),
                         ('Earthquake','Alarm'),
                         ('Alarm','JohnCalls'),
                         ('Alarm','MaryCalls')])
```
Define the conditional Probability Distractions(CPDs)
```
cpd_burglay=TabularCPD(variable='Burglary',variable_card=2,values=[[0.999],[0.001]])
cpd_earthquake=TabularCPD(variable='Earthquake',variable_card=2,values=[[0.998],[0.002]])
cpd_alarm=TabularCPD(variable='Alarm',variable_card=2,values=[[0.999,0.71,0.06,0.05],[0.001,0.29,0.94,0.95]],evidence=['Burglary','Earthquake'],evidence_card=[2,2])
cpd_john_calls=TabularCPD(variable='JohnCalls',variable_card=2,values=[[0.95,0.1],[0.05,0.9]],evidence=['Alarm'],evidence_card=[2])
cpd_mary_calls=TabularCPD(variable='MaryCalls',variable_card=2,values=[[0.99,0.3],[0.01,0.7]],evidence=['Alarm'],evidence_card=[2])
```
Add CPDs to the network
```
network.add_cpds(cpd_burglay,cpd_earthquake,cpd_alarm,cpd_john_calls,cpd_mary_calls)
```
Print the Bayesian network structure
```
print("Bayesian Network Structure:")
print(network)
```
Create a Directed Graph
```
G=nx.DiGraph()
```
Define nodes and Edges
```
nodes=['Burglary', 'Earthquake', 'Alarm',' JohnCalls',' MaryCalls']
edges=[('Burglary','Alarm'),('Earthquake','Alarm'),('Alarm','JohnCalls'),('Alarm','MaryCalls')]
```
Add nodes and Edges to the Graph
```
G.add_nodes_from(nodes)
G.add_edges_from(edges)
```
Set the positions from nodes
```
pos={'Burglary':(0,0),'Earthquake':(2,0),'Alarm':(1,-2),'JohnCalls':(0,-4),'MaryCalls':(2,-4)}
```
Initialize Gibbs Sampling for MCMC
```
gibbs_sampler=GibbsSampling(network)
```
Set the number of samples
```
num_samples=10000
```
Perfrom MNMC sampling
```
samples=gibbs_sampler.sample(size=num_samples)
```
Calculate approximate probabilities based on the samples
```
query_variable='Burglary' query_result=samples[query_variable].value_counts(normalize=True)
```
Print the approximate probabilities
```
print('\n Approximate probabilities of {}:'.format(query_variable)) print(query_result)
```

## Output :
![image](https://github.com/amurthavaahininagarajan/Ex-No.-4--Implementation-of-Approximate-Inference-in-Bayesian-Networks/assets/118679102/ba5a1562-e350-403c-a180-868afb34da79)
![image](https://github.com/amurthavaahininagarajan/Ex-No.-4--Implementation-of-Approximate-Inference-in-Bayesian-Networks/assets/118679102/4745e207-0cfd-4f7f-a822-073be53d98c9)
![image](https://github.com/amurthavaahininagarajan/Ex-No.-4--Implementation-of-Approximate-Inference-in-Bayesian-Networks/assets/118679102/156bc497-248f-47d6-8920-7257b0b0e15f)


## Result : 
Thus, an Approximate method of interference computation is implemented using Gibbs Sampling in Python.
