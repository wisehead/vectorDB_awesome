#1.ShortestPath

```
//图的各种最短路径算法，需要时细看
ShortestPath
--uint64_t num_of_resources = res_mgr->GetAllResources().size();
--std::unordered_map<uint64_t, std::string> id_name_map;
--std::unordered_map<std::string, uint64_t> name_id_map;
--for (uint64_t i = 0; i < num_of_resources; ++i) {
        id_name_map.insert(std::make_pair(i, res_mgr->GetAllResources().at(i)->name()));
        name_id_map.insert(std::make_pair(res_mgr->GetAllResources().at(i)->name(), i));
--}
--std::vector<std::vector<uint64_t>> dis_matrix;
--dis_matrix.resize(num_of_resources);
--for (uint64_t i = 0; i < num_of_resources; ++i) {
        dis_matrix[i].resize(num_of_resources);
        for (uint64_t j = 0; j < num_of_resources; ++j) {
            dis_matrix[i][j] = MAXINT;
        }
        dis_matrix[i][i] = 0;
--}
--
```