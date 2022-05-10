#1.KnowhereResource::Initialize()

```
KnowhereResource::Initialize
--STATUS_CHECK(config.GetEngineConfigSimdType(simd_type));
--if (simd_type == "avx512") {
        faiss::faiss_use_avx512 = true;
        faiss::faiss_use_avx2 = false;
        faiss::faiss_use_sse = false;
    } else if (simd_type == "avx2") {
        faiss::faiss_use_avx512 = false;
        faiss::faiss_use_avx2 = true;
        faiss::faiss_use_sse = false;
    } else if (simd_type == "sse") {
        faiss::faiss_use_avx512 = false;
        faiss::faiss_use_avx2 = false;
        faiss::faiss_use_sse = true;
    } else {
        faiss::faiss_use_avx512 = true;
        faiss::faiss_use_avx2 = true;
        faiss::faiss_use_sse = true;
    }
--std::string cpu_flag;
--faiss::hook_init(cpu_flag)
```