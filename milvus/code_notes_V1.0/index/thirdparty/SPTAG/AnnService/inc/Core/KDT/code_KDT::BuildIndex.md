#1.Index<T>::BuildIndex


```
Index<T>::BuildIndex
--m_pSamples.Initialize(p_vectorNum, p_dimension, (T*)p_data, false);
--if (DistCalcMethod::Cosine == m_iDistCalcMethod)
----int base = COMMON::Utils::GetBase<T>();
------for (SizeType i = 0; i < GetNumSamples(); i++) {
--------COMMON::Utils::Normalize(m_pSamples[i], GetFeatureDim(), base);
--m_workSpacePool.reset(new COMMON::WorkSpacePool(m_iMaxCheck, GetNumSamples()));
--m_workSpacePool->Init(m_iNumberOfThreads);

--m_pTrees.BuildTrees<T>(this);
----SPTAG::COMMON::KDTree::BuildTrees
--m_pGraph.BuildGraph<T>(this);
----SPTAG::COMMON::NeighborhoodGraph::BuildGraph
```