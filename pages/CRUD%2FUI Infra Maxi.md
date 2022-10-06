title:: CRUD/UI Infra Maxi

- I've been trying an idea for a while that all core application stack infrastructure is trending to eventually be PL infrastructure:
  
  > “Increasingly we are seeing old and new languages that incorporate distributed systems concepts into their syntax. Why think of the network as a bolt-on module which is conceptually hard to program when it can be embedded into the language itself? Error handling and scaffolding coding can be eliminated.” — Tyler Jewell, Dell Technologies Capital
  
  "Language-maxi" 
  
  So like
  Node/Deno/Bun, wasm, .NET/JVM/Python
  Spark, TensorFlow, React.js, Erlang process supervision, Reactive programming, actors, functional effect systems
  Long term unification of PL and database - all databases actually become language runtimes
  
  Rise of the DAG langs -
  
  > "In the future there will only be two data structures , DAGs and data frames and you will only be able to be either a DAG person or a DataFrame person and the hostility will become so intense that someone will do a talk on it with stills from West Side Story" — some tweet
- Two connections to Open Source
  1. Languages are virtually always open source, why?
  2. Idea: Language-based infra brings a degree of excellence that is unparalleled today, due to building the infrastructure directly into the foundational element of mathematical abstraction (Lambda) (edited)
- ![Image](https://media.discordapp.net/attachments/1015291875361562644/1016685729746796615/unknown.png?width=829&height=750)
- I think this is a possible solution to the "CRUD/UI maxi" hypothesis as stated by Casado which solves the following lowcode problem statement:
  
  > "One of the seemingly inevitable side effects of making software easier to build is that you tend to sacrifice customizability and a much deeper understanding of how the software works. Low-code/no-code tools tend to look for a general use case and that can restrict how flexible that software can be: there seems to be a tradeoff between ease-of-use and control in all of these tools that I haven’t seen anyone tackle really well (yet). As it stands now, there seems to be a tradeoff between ease-of-use and control, and until someone figures out how to remove that tradeoff, there will always be a need for engineers who can fully manipulate software to meet the full range of use cases businesses (and individuals) need." — Jon Chan, Stack Overflow’s Director of Engineering for Community Products
- Here is the @casado quote from a few weeks ago:
	- "I think a perfect valid definition of infra is "consumed by an app builder." Here seem to be the rough levels:
		- infra mini - infra is low level compute / network / storage / db
		- infra midi - infra is any horizontal layer consumed by app builders
		- infra maxi - infra is everything that isn't the specific UI/CRUD needed by the business
	- being a maxi .. I think the entire app industry is going to shrink to a bunch of MBAs running around with some low code crud thing. Apps become a spreadsheet and integration. Everything else is infra"