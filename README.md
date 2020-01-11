# Distributed Api Test

**Description:**

This is an example and learning resource for myself on how to handle API communication when the project has multiple umbrella projects inside.

The example is comprised of 3 specific projects:

- **common**: This project contains all the structures that are passed via the API and are common in all the other projects;
- **core**: This is an umbrella project that will contain common logic that other projects use (Machine learning algorithms for example) and will be started and access as a remote node;
- **client_1**: This is an umbrella project that simulates an specific product, the ideia is that you can have multiple type of clients (products) that are independent but access **core** node.

The objective of these projects is to allow the communication to be compiler resolved, without compiler warnings, dialyzer errors, etc. Also tests need to be able to work correctly in local or node mode and have the ability to test node logic too.

**Usage**

To run core node, run this command inside core directory:

``` shell
iex --sname core -S mix
```

Then, go to the client_1 directory and run:
``` shell
iex --sname client_1 -S mix
```

Now, inside client_1 iex, call this function:

``` elixir
Main.run_predict
```

You should see this as output in client_1 terminal:
``` elixir
predict result: %Common.SomeStruct{property_1: 12, property_2: "bla bla"}

21:22:20.470 [info]  ML.predict called!
%Common.SomeStruct{property_1: 12, property_2: "bla bla"}
```

and also this in the core terminal:
``` elixir
21:22:20.470 [info]  ML.predict called!
```

**Tests**

You can run tests inside the cluster or without it, to do it inside the cluster, run this command in core directory:
``` shell
iex --sname core -S mix test
```

After that, you can run client_1 tests if you do not close the core iex, just go to the client_1 directory and run:
``` shell
iex --sname client_1 -S mix test
```

You can also run the test without the cluster, note that in this case, some tests (that require the cluster to be alive) will be excluded, for that you can simply run `mix test` normally inside each project.
