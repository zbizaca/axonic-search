# axonic-search

Search based on relationships among entities

### Outline

Entities and their relations are maintained as a graph with a multiple
link types. Messages are propagated from one node to another
and each message specifies which type of links it should be propagated with, 
potentially how many hops, which kind of node to stop and some other navigation directions.
A message can carry another message as a payload that in turn can be emitted from designated nodes.

A message can carry a condition based on itself and other messages received by a node
 that will determine if to notify an external output.
 
 A search for nodes that is based on conditions imposed to 
 other nodes that are linked in a specified can be performed by mapping those 
 conditions and relations into graph messages.
 
### Motivation
 
 Here are some examples:
 
 1. In a graph that contains people their friendships links
 for each person in a list find all the first and second degree friends that 
 are 3 degrees removed from an actor that was never in an Indie movie. The
 information movies and actors can be streamed from a third party
 provider.
 
 2. In a graph that contains companies as nodes, ownership links and
 "trades with" links, find all the companies in New York City that 
 have a parent company on the West Coast but no company in
 their company hierarchy trades with any company that is
 in some black list.
 
 3. Graph consisting of articles linked by references, by subject classification,
  by the authors and by the funding. For a given set of funding sources,
  find all articles are funded by or refer to articles funded by and that include authors
  from a third party list.
  
 Each of these problems could potentially have millions of nodes satisfying 
 some of the conditions. Finding bodes that directly satisfy a given criteria 
 is a solved problem that  can be easily handled by relational databases 
 or  search engines like ElasticSearch.  Graph based searches can provide 
 list of liked candidates that themselves could be in millions. The problem
 could be reduced to intersections of huge sets.
 
 One can deal with problems like these by streaming.  Each set of nodes can be identified
 in an traditional external system and the results can be streamed to graph, generating 
 an appropriate graph message for each marked node.
 
 At the firs glance using graph as network of messages seems to not have any benefits. It does not provide
 a magical reduction of needed processing, at least not in generic cases. But still there are
 benefits:
 1. All the intermediate result are collocated inside the graph
 2. When linked nodes satisfy the same partial condition, only the first one will cause a 
 cascade of messages, those marked later wil send no messages.
 3. If a query needs to modified by changing a condition, only the changed or new condition 
 needs to streamed into the graph, the other ones are already distributed among the nodes.
 3. Query could be persisted in the graph if needed.  Graph links could be added and messages
 pass through the links to obtain new matches.  Also a condition that changed by affecting new
 nodes will only needed to be rerun to those nodes.
  
  ## Toy Messaging Graph
  
  It will use Akka actors as nodes.
  
  Under Construction.
 
