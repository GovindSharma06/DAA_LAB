#include <iostream>
#include <vector>
#include <queue>
#include <algorithm>

using namespace std;

// Structure to represent an edge for Kruskal's Algorithm
struct Edge {
    int u, v, weight;
    bool operator<(const Edge& other) const {
        return weight < other.weight;
    }
};

// Disjoint Set Union (DSU) / Union-Find data structure for Kruskal's
class DSU {
    vector<int> parent, rank;
public:
    DSU(int n) {
        parent.resize(n);
        rank.resize(n, 0);
        for (int i = 0; i < n; i++) parent[i] = i;
    }

    int find(int i) {
        if (parent[i] == i)
            return i;
        return parent[i] = find(parent[i]); // Path compression
    }

    bool unite(int i, int j) {
        int root_i = find(i);
        int root_j = find(j);
        if (root_i != root_j) {
            // Union by rank
            if (rank[root_i] < rank[root_j])
                swap(root_i, root_j);
            parent[root_j] = root_i;
            if (rank[root_i] == rank[root_j])
                rank[root_i]++;
            return true;
        }
        return false;
    }
};

// Prim's Algorithm Implementation
void primMST(int V, const vector<vector<pair<int, int>>>& adj) {
    // Min-heap storing pairs: {weight, vertex}
    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;
    
    vector<int> key(V, 1e9);      // Minimum edge weight to connect each vertex
    vector<int> parent(V, -1);    // Stores MST structure
    vector<bool> inMST(V, false); // Tracks included vertices

    int src = 0;
    pq.push({0, src});
    key[src] = 0;

    int totalWeight = 0;

    while (!pq.empty()) {
        int u = pq.top().second;
        pq.pop();

        if (inMST[u]) continue;
        inMST[u] = true;
        totalWeight += key[u];

        for (auto& neighbor : adj[u]) {
            int v = neighbor.first;
            int weight = neighbor.second;

            if (!inMST[v] && weight < key[v]) {
                key[v] = weight;
                pq.push({key[v], v});
                parent[v] = u;
            }
        }
    }

    cout << "\n--- Prim's Algorithm MST ---\n";
    cout << "Edge \tWeight\n";
    for (int i = 1; i < V; i++) {
        if (parent[i] != -1) {
            cout << parent[i] << " - " << i << " \t" << key[i] << "\n";
        }
    }
    cout << "Total MST Weight (Prim's): " << totalWeight << "\n";
}

// Kruskal's Algorithm Implementation
void kruskalMST(int V, vector<Edge>& edges) {
    // Sort all edges in non-decreasing order of their weight
    sort(edges.begin(), edges.end());

    DSU dsu(V);
    int totalWeight = 0;
    vector<Edge> mstEdges;

    for (const auto& edge : edges) {
        if (dsu.unite(edge.u, edge.v)) {
            totalWeight += edge.weight;
            mstEdges.push_back(edge);
        }
    }

    cout << "\n--- Kruskal's Algorithm MST ---\n";
    cout << "Edge \tWeight\n";
    for (const auto& edge : mstEdges) {
        cout << edge.u << " - " << edge.v << " \t" << edge.weight << "\n";
    }
    cout << "Total MST Weight (Kruskal's): " << totalWeight << "\n";
}

int main() {
    int V, E;
    cout << "Enter number of vertices (V) and edges (E): ";
    cin >> V >> E;

    vector<vector<pair<int, int>>> adj(V);
    vector<Edge> edges;

    cout << "Enter edges in format (source destination weight):\n";
    for (int i = 0; i < E; i++) {
        int u, v, w;
        cin >> u >> v >> w;
        
        // For Prim's (Adjacency List)
        adj[u].push_back({v, w});
        adj[v].push_back({u, w});

        // For Kruskal's (Edge List)
        edges.push_back({u, v, w});
    }

    // Run Prim's Algorithm starting from node 0
    primMST(V, adj);

    // Run Kruskal's Algorithm
    kruskalMST(V, edges);

    return 0;
}
