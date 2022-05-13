#1.class Node
```cpp
class Node : public interface::dumpable {
 public:
    Node();

    void
    AddNeighbour(const NeighbourNodePtr& neighbour_node, Connection& connection);

    std::vector<Neighbour>
    GetNeighbours();

 public:
    json
    Dump() const override;

 private:
    std::mutex mutex_;
    uint8_t id_;
    std::map<uint8_t, Neighbour> neighbours_;
};
```