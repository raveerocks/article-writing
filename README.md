# Dijkstra's Shortest Path Algorithm

Imagine a scenario when it is past midnight on a Saturday night. You are watching a show on Netflix with a bunch of your friends Alice, Bob, Carol and David. It’s 2 am and your friends plan to leave now. You have booked cabs for each of them that shows an ETA(Estimated Time of Arrival) of 20 minutes. Within 5 minutes you get a call from the cab customer service executive. He says  “Because it’s Saturday, we have a large number of bookings. the drivers are busy so it might take more than 30 minutes.”

What do you do next? Just wait for your cab and nothing much, right? That’s when one of your friends comes up with an idea. The idea for finding the shortest path. If you know the shortest path from your home to theirs, they can reach faster once the cab  arrives. All started brainstorming.

The drivers on field are busy taking customers from one place to another. As the bookings come in they ride the cab without even thinking of optimisation. Let’s handle this in a better way now:

Say, green marker  represents your home location in the map below. The markers stands for the each of their residents. The arrows represents directions of each one way path and time taken on that path. In each of the scenarios below, find out which path driver should take to drop your friends.


<img align = "center" src="https://github.com/raveerocks/article-writing/blob/master/map.jpg" width="800" height="500" />


## Brute Force Approach

Alice suggested this idea. One possible way would be to enumerate all the routes from your home to theirs, add up the distances on each route. Even if we remove the paths containing cycles, you would have to exmine enormous number of possibilities, some of them are not even woth considering. For example, David can take a path via Alice, Bob and Carol's home. Obviously it's a bad choice.


## Dijkstra's Approach

Bob suggested we could use Dijkstra's Algorithm. This algorithm is used to solve the single source shortest path problem on a weighted, direcred graph. The map above is graph `G = (V,E)`. Each of the circles are verices `(V)` and the one way paths are the edges `(E)` in the graph. In our case the source `s` is your home and weights `w` will be the time taken to reach each destination.

Dijkstra's Approach maintains a set `S` of vertices whose final shortest-path weights from the source `s` have already been determined. In this approach we repeatedly select a vertex `u ∈ V-S` with minimum shortest-path estimate, adds `u` to `S`, and updates the shortest distnaces to other vertices possible via `u`. 

## Algorithm

```
DIJKSTRA( Graph G, Weights w, Source s)

      # Initialisation of datastructures
  
  1.  for each vertext v ∈ G.V
  
      1.1 v.distance = ∞                # Initially all the vertices are at ∞ distance from s
    
      1.2 v.path = NIL                  # Initially no paths are known
    
  2. s.distance = 0                     # Source is a at a distance 0 from itself
  
  3. S = Φ                              # No verices initially included in final set
  
  4. Q = G.V                            # All the vertices except the source itself are initially in a queue
  
  
      # Repeatedly selecting the vertex with minimum distance to include into final set
  
  5. while Q is not empty
  
      5.1 u = minimum(Q)                # Extracting the vertex u with minimum distance
      
      5.2 S = S U {u}                   # Adding u to the final set
      
      5.3 for each vertex v ∈ G.Adj[u]  # For each vertext v adjacent to u we need to upate the distance
      
        5.3.1 if v.d > u.d + w(u,v)     # If the current distance is more than the distance via u update the distance
            
            5.3.1.1 v.d = u.d + w (u,v)
            5.3.1.2 v.path = u
          
  

```
