#1.KDTree::BuildTrees

```
KDTree:: BuildTrees
--std::vector<SizeType> localindices;
--if (indices == nullptr) {
----ocalindices.resize(p_index->GetNumSamples());
----for (SizeType i = 0; i < p_index->GetNumSamples(); i++) localindices[i] = i;
--else {
----localindices.assign(indices->begin(), indices->end());
--m_pTreeRoots.resize(m_iTreeNumber * localindices.size());
--m_pTreeStart.resize(m_iTreeNumber, 0);
--for (int i = 0; i < m_iTreeNumber; i++)
----Sleep(i * 100); std::srand(clock());                                                                                                                                                                              
----std::vector<SizeType> pindices(localindices.begin(), localindices.end());                                        
----std::random_shuffle(pindices.begin(), pindices.end());                                                                                                                                                                          
----m_pTreeStart[i] = i * (SizeType)pindices.size();                                                                 
----std::cout << "Start to build KDTree " << i + 1 << std::endl;                                                     
----SizeType iTreeSize = m_pTreeStart[i];                                                                            
----DivideTree<T>(p_index, pindices, 0, (SizeType)pindices.size() - 1, m_pTreeStart[i], iTreeSize);                  
----std::cout << i + 1 << " KDTree built, " << iTreeSize - m_pTreeStart[i] << " " << pindices.size() << std::endl;   

```