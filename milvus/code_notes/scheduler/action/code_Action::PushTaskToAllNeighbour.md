#1.Action::PushTaskToAllNeighbour

```
Action::PushTaskToAllNeighbour
--auto neighbours = get_neighbours(self);
--for (auto& neighbour : neighbours) {
----neighbour->task_table().Put(task_item->get_task(), task_item);
  }
```