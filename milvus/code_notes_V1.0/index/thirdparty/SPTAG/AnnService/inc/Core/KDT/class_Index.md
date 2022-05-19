#1.class Index

```cpp
namespace SPTAG
{
    namespace KDT
    {
        template<typename T>
        class Index : public VectorIndex
        {
        private:
            // data points
            COMMON::Dataset<T> m_pSamples;

            // KDT structures. 
            COMMON::KDTree m_pTrees;

            // Graph structure
            COMMON::RelativeNeighborhoodGraph m_pGraph;

            std::string m_sKDTFilename;
            std::string m_sGraphFilename;
            std::string m_sDataPointsFilename;
            std::string m_sDeleteDataPointsFilename;

            std::mutex m_dataAddLock; // protect data and graph
            Helper::Concurrent::ConcurrentSet<SizeType> m_deletedID;
            float m_fDeletePercentageForRefine;
            std::unique_ptr<COMMON::WorkSpacePool> m_workSpacePool;
            
            int m_iNumberOfThreads;
            DistCalcMethod m_iDistCalcMethod;
            float(*m_fComputeDistance)(const T* pX, const T* pY, DimensionType length);
 
            int m_iMaxCheck;
            int m_iThresholdOfNumberOfContinuousNoBetterPropagation;
            int m_iNumberOfInitialDynamicPivots;
            int m_iNumberOfOtherDynamicPivots;
        };
    } // namespace KDT
} // namespace SPTAG

```