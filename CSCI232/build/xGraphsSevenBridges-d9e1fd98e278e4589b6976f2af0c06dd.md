# Seven Bridges of Königsberg

The **Seven Bridges of Königsberg** is a historically notable problem in mathematics that laid the foundations for graph theory and prefigured the idea of topology. Let’s delve into the details:

1. **The City of Königsberg**:
   - Königsberg (now Kaliningrad, Russia) was a city set on both sides of the Pregel River.
   - It included two large islands: **Kneiphof** and **Lomse**.
   - These islands were connected to each other and to the two mainland portions of the city by **seven bridges**.
1. **The Problem**:
   - The challenge was to find a walk through the city that would **cross each bridge once and only once**.
   - The rules were strict:
     - Solutions couldn’t involve reaching an island or mainland bank without using a bridge.
     - Accessing any bridge without crossing to its other end was unacceptable.
1. **Euler’s Insight**:
   - **Leonhard Euler**, a brilliant mathematician, analyzed the problem.
   - He realized that the choice of route inside each landmass (island or mainland) was irrelevant.
   - The crucial aspect was the **sequence of bridges crossed**.
   - Euler reformulated the problem in abstract terms, focusing only on the list of landmasses and the bridges connecting them.
1. **Graph Theory Approach**:
   - Euler replaced each landmass with an abstract “vertex” or node.
   - Each bridge became an abstract connection or “edge” between vertices.
   - The resulting mathematical structure is a **graph**.
   - The shape of the graph could be distorted without changing its essence—only the number of edges between nodes mattered.
1. **Euler’s Solution**:
   - Euler observed that whenever one enters a vertex by a bridge, one must leave it by a bridge (except at the endpoints of the walk).
   - If every bridge had been traversed exactly once, the number of bridges touching each landmass must be **even**.
   - Euler proved that the problem had **no solution** because the number of bridges touching each landmass was **odd**.
1. **Legacy**:
   - Euler’s negative resolution of the Seven Bridges problem laid the groundwork for graph theory.
   - It also prefigured the concept of **topology**, which studies properties preserved under continuous deformations.