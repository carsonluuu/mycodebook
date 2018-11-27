# Minimum Spanning Tree

Given a list of Connections, which is the Connection class \(the city name at both ends of the edge and a cost between them\), find some edges, connect all the cities and spend the least amount.  
Return the connects if can connect all the cities, otherwise return empty list.

### Example

Gievn the connections =`["Acity","Bcity",1], ["Acity","Ccity",2], ["Bcity","Ccity",3]`

Return`["Acity","Bcity",1], ["Acity","Ccity",2]`

Note: Return the connections sorted by the cost, or sorted city1 name if their cost is same, or sorted city2 if their city1 name is also same.

### Note

好像微软会考，这里利用并查集来apply Kruskal's algorithm：

* 将边排序后选择边，在选择边的过程中使用并查集维护保证无环
* 这里Union Find得使用Map，不连续了

### Code

```java
/**
 * Definition for a Connection.
 * public class Connection {
 *   public String city1, city2;
 *   public int cost;
 *   public Connection(String city1, String city2, int cost) {
 *       this.city1 = city1;
 *       this.city2 = city2;
 *       this.cost = cost;
 *   }
 * }
 */
public class Solution {
    /**
     * @param connections given a list of connections include two cities and cost
     * @return a list of connections from results
     */
    private String find(String str, Map<String, String> father) {
        if (!father.containsKey(str)) {
            father.put(str, str);
        } else if (!father.get(str).equals(str)) {
            father.put(str, find(father.get(str), father));
        }

        return father.get(str);
    }  

    public List<Connection> lowestCost(List<Connection> connections) {
        // Write your code here
        List<Connection> res = new ArrayList<Connection>();
        Collections.sort(connections, new Comparator<Connection>() {
            public int compare(Connection a, Connection b) {
                if (a.cost != b.cost) {
                    return a.cost - b.cost;
                }
                if (!a.city1.equals(b.city1)) {
                    return a.city1.compareTo(b.city1);
                }
                return a.city2.compareTo(b.city2);
            }
        });

        Map<String, String> father = new HashMap<>();
        for (Connection con : connections) {
            String root1 = find(con.city1, father);
            String root2 = find(con.city2, father);
            /*
            Kruskal's algorithm：
            将边排序后选择边，在选择边的过程中使用并查集维护保证无环。
            */
            if (!root1.equals(root2)) {
                father.put(root1, root2);
                res.add(con);
            }
        }

        if (res.size() != father.size() - 1) {
            return new ArrayList<Connection>();
        }

        return res;
    }
}
```



