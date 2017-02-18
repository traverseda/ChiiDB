#ChiiDB

ChiiDB is a "low-level" database. The current status is "conceptual". No code
has been written.

# Overview

First, data objects are capnproto serialized. Basically, this means that our
basic data format is C structs and is statically typed.

Queries are made using some kind of tiny DSL. Something not entirely unlike
`asm.js`. Queries are essentially a map for a map reduce.

Queries are ongoing. You register a query sort of like registering for inotify
in linux.

Indexes are a variation of queries. Essentially they build a new 'index' data
object
whenever the data in their source data object changes. They use the same DSL as
queries, and are essentially just functions. Indexes are ultimatly just some
preprocessing on data, and that can take whatever format the client wants.

We build our permissions system as a set of filters. Essentially, a permission
is just
a filter that filters the input and output of a user query. This allows us to
easily create filters like `limit user Y to data objects with tag X`, and to
create much more complicated permissions.

We build our replication system using the same query system. Replication is just
a bi-directional pipe for changes between two data objects on different systems.

We allow access to data objects as shared memory, allowing for things
like an ACID layer on what would otherwise be an eventual consistancy model.

Finally, add support for more complicated data types, built on top of our
capnproto C-struct like serialization format. I'm very much in favour of some
sort of duct-typed model built out of statically typed data objects.

#Major Components

