## Summary

* Good potential for computation
* Use Montecarlo
* Use genetics algos to select the paths the people should take
* Simulates queues
* Probably possible to distribute as it is stochastically looking for a score maximum: possible to run independent simulations (different random seeds, or different param) and take the overall max
* Run through CLI with: java -cp ../../../matsim-0.10.1/matsim-0.10.1.jar org.matsim.run.Controler myconfig.xml


## Next steps

* Run it in a container, then in Qarnot
* Check who uses it


## General

* MATSimis an activity-based, extendable, multi-agent simulationframeworkimplemented inJava.  Itis open-source
* every agent repeatedlyoptimizes its dailyactivityschedule while in competition for space-time slots with all other agents onthe transportation infrastructure. This is somewhat similar to the route assignment iterative cycle, butgoes beyond route assignment by incorporating other choice dimensions like time choice (Balmer et al.,2005), mode choice (Grether et al.,2009), or destination choice (Horni et al.,2012) into the iterativeloop.
* AMATSim runcontains a configurable number of iterations, represented by the loop of Figure1.1anddetailed below. It starts with an initial demand arising from thestudyarea population’s daily activitychains.  The modeled persons are called agents. During iterations, this initial demand is optimizedindividually by each agent. Every agent possesses a memory containing a fixed number of day plans,where eachplanis composed of a daily activity chain and an associatedscore.  The score can beinterpreted as an econometric utility
* In every iteration, prior to the simulation of the network loading with theMATSimmobsim (mobilitysimulation)(e.g.,Cetin,2005), each agent selects a plan from its memory. This selection is dependent onthe planscores, which are computed after each mobsim run, based on the executed plans’ performances.A certain share of the agents (often 10 %) are allowed to clone the selected plan and modify this clone(replanning).
* Plan modification is performed by thereplanningmodules.  Four dimensions are usually consideredforMATSimat this time: departure time (and, implicitly, activity duration) (Balmer et al.,2005), route(Lefebvre and Balmer,2007), mode (Grether et al.,2009) and destination (Horni et al.,2009,2012).Further dimensions, such as activity adding or dropping, or parking and group choices are currentlyunder development and only available experimentally
* MATSimreplanning offers different strategiesto adapt plans, ranging from random mutation to approximate suggestions, to best-response answerswhere, in every iteration, the currently optimal choice is searched.  For example, routing often is abest-response modification, while time and mode replanning are random mutations
* An iteration is completed by evaluating the agents’ experiences with the selected day plans (scoring).
* The iterative process is repeated until the average population score stabilizes
* Gestion des queues (par exemple à un carrefour): MATSimprovides two internalmobsims:QSimandJDEQSim (Java Discrete Event Queue Simulation); inaddition, external mobility simulations can be plugged in
* MAtSIM a l'air de marcher par pas de temps (discret): TheMATSimtraffic flow model is strongly based on the two link attributes: storage capacity and flowcapacity. Storage capacity defines the number of cars fitting onto a network link.Flow capacity specifies the outflow capacity of a link, i.e., how many travelers can leave the respectivelink per time step.
* Genetics:
  * theMATSimequilibrium is searched for by aco-evolutionary algorithm(see, e.g.,Popovici et al.,2012).  Thesealgorithmsco-evolve different species subject to interaction(e.g., competition). InMATSim, individuals are represented by their plans, where a person representsa species.  With the co-evolutionary algorithm, optimization is performed in terms of agents’ plans,i.e., across the whole daily plan of activities and travel. It achieves more than the standard traffic flowequilibria, which ignores activities. Eventually, an equilibrium is reached, subject to constraints, wherethe agents cannot further improve their plans unilaterally.
  * Note that there is a difference between the application of an evolutionary algorithm and aco-evolutionaryalgorithm. An evolutionary algorithm would lead to a system optimum, as optimization is applied witha global (or population) fitness function. Instead, the co-evolutionary algorithm leads to a (stochastic) userequilibrium, as optimization is performed in terms ofindividualscoring functions and within an agent’s set of plans.


## Run an example

#### Simulation

* Previously: important d'utiliser openjdk-11 (v8 marchait pas)
* ouvrir nautilus (via mod + d, pas via le CLI, sinon ça bug)
* double clicker sur matsim-0.10.1/matsim-0.10.1.jar
* GUI s'ouvre
* chercher le config file dans matsim-example-project(git)/scenarios/equil/config.xml
* lancer la simu


#### Visualisation

* download VIA tool here https://www.simunto.com/via/
* ask for a free license (they send you an email)
* The events file for the zeroth iteration is located in .../ITERS/it.0/...0.events.xml.gz
* Click the first icon (Data Sources). Now you can either drag and drop files into this section (e.g. a network.xml, or events.xml.gz), or click the “+” at the bottom to select a file to be added. add first network.xml to the list of available data and then events.xml.gz
* Next, click on the second icon (“Layers”) in the Controls section. Initially, you will see only the background layer listed. Click on the ‘+’ to select the data you want to have displayed. It should already suggest to visualize the network with the loaded network.xml, so just click Add. After a short moment, the network should be shown in the visualization area. Click the ‘+’ again, but this time choose Vehicles as layer type. The events.xml.gz file will be already pre-selected. Click on Add. As any layer depending on the events, a Load Data button will appear at the bottom of the layer tag. Click it to extract the vehicles’ positions from the events.
* Add Vehicles layer, and Agent layers
* Then modify speed to start the simulation


## Config files

* config du réseau avec max speed, length of lanes, freespeed, capacity, et la configuration des différents noeuds
* config du cas : random seed, snapshot frequency, fréquence des activités comme late departure, différentes probas


## Some links

* Interesting README in the file
* Great documentation here book, whom first 2 chapters are equivalent to a user guide: https://www.ubiquitypress.com/site/books/10.5334/baw/
* Tutorials / classes: https://www.matsim.org/docs/tutorials/general
* https://github.com/matsim-org/matsim-example-project
* https://www.simunto.com/via/
