#1.class Neighbour

```cpp
struct Neighbour {
    Neighbour(NeighbourNodePtr nei, Connection conn) : neighbour_node(std::move(nei)), connection(std::move(conn)) {
    }

    ~Neighbour() {
        neighbour_node = nullptr;
    }

    NeighbourNodePtr neighbour_node;
    Connection connection;
};
```