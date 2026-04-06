Two sets are called **disjoint sets** if they don't have any element in common. The disjoint set data structure is used to store such sets. It supports following operations:

- Merging two disjoint sets to a single set using **Union** operation.
- Finding representative of a disjoint set using **Find** operation.

The use case for this pretty simple, If we want to perform a find operation on a graph, we can do it in O(1) time along with finding it's parents. It's usually used in dynamic graph. 

Union can be done by rank or by size. 

What is a dynamic graph.
If we're creating a graph and we have to perform operations while building it. Like find, that means its a dynamic graph. 

## Union 
### Rank
So initially we'll need only two arrays for this, one would be the rank array and the other one would be the parents array. Let's say we have a graph with 7 nodes. Here's the rank and parent array initialisation.

| `node`   | 1   | 2   | 3   | 4   | 5   | 6   | 7   |
| -------- | --- | --- | --- | --- | --- | --- | --- |
| `rank`   | 0   | 0   | 0   | 0   | 0   | 0   | 0   |
| `parent` | 1   | 2   | 3   | 4   | 5   | 6   | 7   |

Initially every node is a parent to itself.

Pseudocode for Union of u, v
-> `union(u,v)` 
1. Find the ultimate parent of u and v, parentU and parentV. 
2. Find the rank of parentU and parentV. 
3. Connect the smaller rank to the larger rank always.

-> `union(1,2)`
`parentU = 1 and parentV = 2`
`rankParentU = 0 and rankParentV = 0`

| `node`   | 1   | 2   | 3   | 4   | 5   | 6   | 7   |
| -------- | --- | --- | --- | --- | --- | --- | --- |
| `rank`   | 1   | 0   | 0   | 0   | 0   | 0   | 0   |
| `parent` | 1   | 1   | 3   | 4   | 5   | 6   | 7   |

-> `union(2,3)`
`parentU = 1 and parentV = 3`
`rankParentU = 1 and rankParentV = 0`
We did no increase rank of one here because we can directly connect 3 with 2

| `node`   | 1   | 2   | 3   | 4   | 5   | 6   | 7   |
| -------- | --- | --- | --- | --- | --- | --- | --- |
| `rank`   | 1   | 0   | 0   | 0   | 0   | 0   | 0   |
| `parent` | 1   | 1   | 1   | 4   | 5   | 6   | 7   |

-> `union(4,5)`
`parentU = 4 and parentV = 5`
`rankParentU = 0 and rankParentV = 0`

| `node`   | 1   | 2   | 3   | 4   | 5   | 6   | 7   |
| -------- | --- | --- | --- | --- | --- | --- | --- |
| `rank`   | 1   | 0   | 0   | 1   | 0   | 0   | 0   |
| `parent` | 1   | 1   | 1   | 4   | 4   | 6   | 7   |

-> `union(6,7)`
`parentU = 6 and parentV = 7`
`rankParentU = 0 and rankParentV = 0`

| `node`   | 1   | 2   | 3   | 4   | 5   | 6   | 7   |
| -------- | --- | --- | --- | --- | --- | --- | --- |
| `rank`   | 1   | 0   | 0   | 1   | 0   | 1   | 0   |
| `parent` | 1   | 1   | 1   | 4   | 4   | 6   | 6   |

-> `union(5,6)`
`parentU = 4 and parentV = 6`
`rankParentU = 1 and rankParentV = 1`
 We increased the rank because we're adding joining 2 same rank sets

| `node`   | 1   | 2   | 3   | 4   | 5   | 6   | 7   |
| -------- | --- | --- | --- | --- | --- | --- | --- |
| `rank`   | 1   | 0   | 0   | 2   | 0   | 1   | 0   |
| `parent` | 1   | 1   | 1   | 4   | 4   | 4   | 6   |

-> `union(3,7)`
`parentU = 1 and parentV = 4`
`rankParentU = 1 and rankParentV = 2`
 Rank does not increase because we're joining a smaller and a greater set.
Why did 7 -> 4 (directly made a connection with)? This is path compression.

| `node`   | 1   | 2   | 3   | 4   | 5   | 6   | 7   |
| -------- | --- | --- | --- | --- | --- | --- | --- |
| `rank`   | 1   | 0   | 0   | 2   | 0   | 1   | 0   |
| `parent` | 4   | 1   | 1   | 4   | 4   | 4   | 4   |

### Path compression
So every time we're running a find operation, we're gonna make sure that every node is directly connected to its ultimate parent, this called path compression. This helps us get the time complexity of the find down to O(1).

```java
int find (int u){
	if(u == parent[u]) return u;
	return parent[u] = find(parent[u]);
}
```


Here's the java code for Disjoint Set with Union by rank.

```java
class DisjointSet {
	int[] rank;
	int[] parent;

	DisjointSet(int n) {
		for (int i = 0; i < n; i++) {
			parent[i] = i;
			rank[i] = 0;
		}
	}

	int find(int u) {
		if (parent[u] == u)
			return u;
		return parent[u] = find(parent[u]);
	}

	boolean rankByUnion(int u, int v) {
		int parentOfU = find(u);
		int parentOfV = find(v);

		if (parentOfU == parentOfV)
			return false;
		else {
			int rankOfParentOfU = rank[parentOfU];
			int rankOfParentOfV = rank[parentOfV];

			if (rankOfParentOfU > rankOfParentOfV)
				parent[parentOfV] = parentOfU;
			else if (rankOfParentOfU < rankOfParentOfV)
				parent[parentOfU] = parentOfV;
			else {
				parent[parentOfV] = parentOfU;
				rank[parentOfU]++;
			}
			return true;
		}
	}
}
```

### Size
Union by size only considers size at the time of merge, so basically. It considers size instead of rank and then adds its. So basically merge the smaller sized set with the bigger sized one. 

```java
class DisjointSet {
	int[] size;
	int[] representative;

	DisjointSet(int n) {
		size = new int[n];
		representative = new int[n];

		for (int i = 0; i < n; i++) {
			size[i] = 1;
			representative[i] = i;
		}
	}

	int find(int u) {
		if (representative[u] == u)
			return u;
		return representative[u] = find(representative[u]);
	}

	boolean rankBySize(int u, int v) {
		int repU = find(u);
		int repV = find(v);

		if (repU == repV)
			return false;
		else {
			if (size[repU] > size[repV]) {
				representative[repV] = repU;
				size[repU] += size[repV];
			} else {
				representative[repU] = repV;
				size[repV] += size[repU];
			}
			return true;
		}
	}
}
```