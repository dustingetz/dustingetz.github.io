publish:: false

- In reactive dataflow programming, there are two primary abstractions: stream and signal (aka "property"). What's the difference?
- Streams model events – they are discrete and eager. Mouse clicks. Database transactions. Commands. They are undefined between events.
- Signals model values. They are like Clojure atoms - they always have a current value and you only care about the most recent value.
- Streams are discrete and eager.
  Signals are continuous and lazy.
  Signals let you sample the current most recent value. This idea of "latest" matches reactive DOM rendering– you always want the freshest value. Why would you ever want to render a stale view? (You wouldn't)
- To synthesize the differences, the quintessential example to consider is an event-sourced database. When seen as dataflow, the transaction side is an event stream (tx are a discrete command and eagerly written to the log).
- The query side (polling a database value as needed) is a lazy signal. The query is not computed until asked for and you always want the freshest result. Request/response is lazy sampling.
- Event streams are fundamentally diffs. You need to reduce the log to know what the current database value is. Streams are history sensitive – you cannot skip or miss a diff!
- In the database model, transactions are differential and can never be missed. They write through to the log. The db indexes, a reduction of the log, apply the diffs and patch the index eagerly. At that point, the database index is a lazy signal; clients will sample/poll on demand
- But why do databases work like that? What if the system was fully differential?
- Imagine a fully differential client/server system, a closed loop where the client sends transaction events to the server, the tx flow through the active database queries, the server streams query diffs to the client, the client streams the diffs through the UI to get a dom delta
- But we've assumed the "active" queries are known in advance! Every time you navigate to a new UI screen, the set of active queries changes. That means you need to reflow the entire log.
- In event sourced systems this process of reflowing the log through a new query is called "booting" and if your log is big this can take hours or days!
- You can optimize the booting process with snapshots, but guess what: snapshots are values not diffs! The concept of a snapshot is modeled by a continuous time value that is lazily sampled on demand the next time a query boots
- There is also a compile-time vs run-time question. Are all your queries known at compile time? If so, you can potentially keep all the queries alive (subject to having enough memory to save the accumulator state to apply new diffs as they come in)
- In the case of a user interface, this means your UI process (browser tab) needs to have enough memory to store all possible views of the database.
- Imagine a UI infinite scroll spreadsheet component. You scroll to the next page of records. No new database event in the log, just a scroll. In the differential model, those records need to be in memory already!
- This is why differential dataflow is a poor fit for reactive UI rendering. Clients are resource constrained, you need to be lazy and skip as much work as possible, by polling exactly what you need when you need it.
- Rendering is fundamentally lazy. Commands are fundamentally eager. To model real world systems you need both
- Our Photon language models signals. (Photon is a fully reactive programming language for fullstack UI development. It does not just reactive rendering, but also reactive backend, all connected together into a streaming fullstack application)