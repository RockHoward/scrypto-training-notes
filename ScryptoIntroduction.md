# How Does the Radix Engine V2 Work?
This background information is based on the videos posted by Matt Hine on Feb. 3rd, 2021.

## Part 1 -- https://www.youtube.com/watch?v=Z5jLiR11gtY
What is the purpose of the Radix Engine V2?
	- Smart contracts intended for defi
	- New way of building decentralized apps

### The Old Way (Ethereum):
	- backend dev creates smart contracts
	- frontend dev uses 'methods' from the smart contracts
	- frontend dev creates the User App UI
	- smart contracts run on the EVM
	- Nakamoto Consensus
	- no code sharing, cut and paste methodology

### The New way (Radix Engine V2)
	- backend dev creates 'component blueprints' using scrypto
		- component blueprints live on the ledger
	- backend dev instantiates components using 'actions' offered by components
		and by interacting with Constructor / Libraries
		- instantiated components live on the ledger
	- frontend dev uses components via 'actions' defined in instantiated components
	- frontend dev creates the User App UI
	- instantiated components run within the Radix Finite State Machine
	- the Radix Finite State Machine runs within the Radix VM
	- the Radix VM uses Cerberus Consenses
	- Blueprints and instantiated componets are sharable

### Major Features
	- Component Blueprint Catalog
		- Blueprints can be instantiated or else imported and extended via scrypto
	- Tokens are independent entities and not just a balance amount kept within a contract
		- This makes things easier for the frontend dev and requires less computation

## Part 2 -- https://www.youtube.com/watch?v=Lkt0y8DTx9A
### The Radix Finite State Machine
	- Definite predictable outcomes
		- So is Solidity but it is very unintuitive
		- Universal Finite State Machine (UFSM)
			- more predictable behaviors are enforced
	
### Gumball Machine Example
#### Elements
		- The gumball machine
		- a quarter
		- a gumball
		- rowdy roddy piper (a gumball user)

#### Each of these elements is modelled as a component
		- quarters and gumballs have owners
			- pecifically they have one owner at a time
			- they have the ability to transfer from one owner to another
			- they are instantiated from a Token Blueprint
		- Roddy and the gumball machine are more like containers
			- they have ids and aggregations of quarters and gumballs
			- they both could be instantiated from an Account Blueprint

	The Gumball Machine has extra functionality and so might actually be instantiated from a "Seller Blueprint" that imports and extends the Account Blueprint. For example the Seller Blueprint might add a "buy" action to exchange a quarter token for a gumball token.

	All of these elements would be modelled as blueprints.
	
#### Here is a closed atomic tranasaction
Roddy wants to transfer a quarter to the gumball machine and get back a gumball.
	
	- Roddy uses the "buy" action of the Gumball Machine.
	
	- The Radix FSM translates this into a set of inputs:
		- "Roddy", "Gumball Machine: Buy"
		- "Quarter: Transfer"
		- "Gumball: Transfer";
	and output state changes:
		- "Quarter:owner -> Gumball Machine"
		- "Gumball:owner -> Roddy"
	
Everything has to work correctly or else nothing happens and we end up back with the original state. This is true even though the various state transitions may occur in different shards (providing parallelization and scaling), but the programmer doesn't have to worry about those details.

So the Radix Engine V2 can change requests for actions encoded in Blueprints into a set of transitions that affect instantiated components in an "all or nothing manner" within an environment built for safety, speed and scalability.

END OF NOTES
