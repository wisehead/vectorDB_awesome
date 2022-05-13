#1.Action::PushTaskToAllNeighbour

```
Action::PushTaskToAllNeighbour
--auto neighbours = get_neighbours(self);
--for (auto& neighbour : neighbours) {
----neighbour->task_table().Put(task_item->get_task(), task_item);
  }
```

#2.get_neighbours

```
get_neighbours
--std::vector<ResourcePtr> neighbours;
--for (auto& neighbour_node : self->GetNeighbours()) 
----auto node = neighbour_node.neighbour_node;
----auto resource = std::static_pointer_cast<Resource>(node);
----neighbours.emplace_back(resource);
--return neighbours;
```

#3.Node::GetNeighbours

```
Node::GetNeighbours
--for (auto& e : neighbours_) {
----ret.push_back(e.second);
--}
```