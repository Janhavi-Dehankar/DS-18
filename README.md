# DS-18
DS code
#include <stdio.h>
#include <stdlib.h>

#define SIZE 100

int adj[SIZE][SIZE], visited[SIZE], n;

void BFS(int start) {
    int queue[SIZE], front = 0, rear = 0;
    int visitedBFS[SIZE] = {0};
    queue[rear++] = start;
    visitedBFS[start] = 1;
    printf("BFS: ");
    while (front < rear) {
        int v = queue[front++];
        printf("%d ", v);
        for (int i = 0; i < n; i++) {
            if (adj[v][i] && !visitedBFS[i]) {
                queue[rear++] = i;
                visitedBFS[i] = 1;
            }
        }
    }
    printf("\n");
}

void DFSUtil(int v, int visitedDFS[]) {
    visitedDFS[v] = 1;
    printf("%d ", v);
    for (int i = 0; i < n; i++)
        if (adj[v][i] && !visitedDFS[i])
            DFSUtil(i, visitedDFS);
}

void DFS(int start) {
    int visitedDFS[SIZE] = {0};
    printf("DFS: ");
    DFSUtil(start, visitedDFS);
    printf("\n");
}

int main() {
    int edges, u, v, start;
    printf("Enter number of vertices: ");
    scanf("%d", &n);
    printf("Enter number of edges: ");
    scanf("%d", &edges);
    for (int i = 0; i < edges; i++) {
        printf("Enter edge (u v): ");
        scanf("%d %d", &u, &v);
        adj[u][v] = 1;
        adj[v][u] = 1; 
    }
    printf("Enter starting vertex: ");
    scanf("%d", &start);
    BFS(start);
    DFS(start);
    return 0;
}
