#1. ErrorCode


```cpp
// server error code
constexpr ErrorCode SERVER_UNEXPECTED_ERROR = ToServerErrorCode(1);
constexpr ErrorCode SERVER_UNSUPPORTED_ERROR = ToServerErrorCode(2);
constexpr ErrorCode SERVER_NULL_POINTER = ToServerErrorCode(3);
constexpr ErrorCode SERVER_INVALID_ARGUMENT = ToServerErrorCode(4);
constexpr ErrorCode SERVER_FILE_NOT_FOUND = ToServerErrorCode(5);
constexpr ErrorCode SERVER_NOT_IMPLEMENT = ToServerErrorCode(6);
constexpr ErrorCode SERVER_CANNOT_CREATE_FOLDER = ToServerErrorCode(8);
constexpr ErrorCode SERVER_CANNOT_CREATE_FILE = ToServerErrorCode(9);
constexpr ErrorCode SERVER_CANNOT_DELETE_FOLDER = ToServerErrorCode(10);
constexpr ErrorCode SERVER_CANNOT_DELETE_FILE = ToServerErrorCode(11);
constexpr ErrorCode SERVER_BUILD_INDEX_ERROR = ToServerErrorCode(12);
constexpr ErrorCode SERVER_CANNOT_OPEN_FILE = ToServerErrorCode(13);

constexpr ErrorCode SERVER_COLLECTION_NOT_EXIST = ToServerErrorCode(100);
constexpr ErrorCode SERVER_INVALID_COLLECTION_NAME = ToServerErrorCode(101);
constexpr ErrorCode SERVER_INVALID_COLLECTION_DIMENSION = ToServerErrorCode(102);
constexpr ErrorCode SERVER_INVALID_VECTOR_DIMENSION = ToServerErrorCode(104);
constexpr ErrorCode SERVER_INVALID_INDEX_TYPE = ToServerErrorCode(105);
constexpr ErrorCode SERVER_INVALID_ROWRECORD = ToServerErrorCode(106);
constexpr ErrorCode SERVER_INVALID_ROWRECORD_ARRAY = ToServerErrorCode(107);
constexpr ErrorCode SERVER_INVALID_TOPK = ToServerErrorCode(108);
constexpr ErrorCode SERVER_ILLEGAL_VECTOR_ID = ToServerErrorCode(109);
constexpr ErrorCode SERVER_ILLEGAL_SEARCH_RESULT = ToServerErrorCode(110);
constexpr ErrorCode SERVER_CACHE_FULL = ToServerErrorCode(111);
constexpr ErrorCode SERVER_WRITE_ERROR = ToServerErrorCode(112);
constexpr ErrorCode SERVER_INVALID_NPROBE = ToServerErrorCode(113);
constexpr ErrorCode SERVER_INVALID_INDEX_NLIST = ToServerErrorCode(114);
constexpr ErrorCode SERVER_INVALID_INDEX_METRIC_TYPE = ToServerErrorCode(115);
constexpr ErrorCode SERVER_INVALID_INDEX_FILE_SIZE = ToServerErrorCode(116);
constexpr ErrorCode SERVER_OUT_OF_MEMORY = ToServerErrorCode(117);
constexpr ErrorCode SERVER_INVALID_PARTITION_TAG = ToServerErrorCode(118);
constexpr ErrorCode SERVER_INVALID_BINARY_QUERY = ToServerErrorCode(119);

// db error code
constexpr ErrorCode DB_META_TRANSACTION_FAILED = ToDbErrorCode(1);
constexpr ErrorCode DB_ERROR = ToDbErrorCode(2);
constexpr ErrorCode DB_NOT_FOUND = ToDbErrorCode(3);
constexpr ErrorCode DB_ALREADY_EXIST = ToDbErrorCode(4);
constexpr ErrorCode DB_INVALID_PATH = ToDbErrorCode(5);
constexpr ErrorCode DB_INCOMPATIB_META = ToDbErrorCode(6);
constexpr ErrorCode DB_INVALID_META_URI = ToDbErrorCode(7);
constexpr ErrorCode DB_EMPTY_COLLECTION = ToDbErrorCode(8);
constexpr ErrorCode DB_BLOOM_FILTER_ERROR = ToDbErrorCode(9);
constexpr ErrorCode DB_PARTITION_NOT_FOUND = ToDbErrorCode(10);
constexpr ErrorCode DB_OUT_OF_STORAGE = ToDbErrorCode(11);

// knowhere error code
constexpr ErrorCode KNOWHERE_ERROR = ToKnowhereErrorCode(1);
constexpr ErrorCode KNOWHERE_INVALID_ARGUMENT = ToKnowhereErrorCode(2);
constexpr ErrorCode KNOWHERE_UNEXPECTED_ERROR = ToKnowhereErrorCode(3);
constexpr ErrorCode KNOWHERE_NO_SPACE = ToKnowhereErrorCode(4);

// knowhere error code
constexpr ErrorCode WAL_ERROR = ToWalErrorCode(1);
constexpr ErrorCode WAL_META_ERROR = ToWalErrorCode(2);
constexpr ErrorCode WAL_FILE_ERROR = ToWalErrorCode(3);
constexpr ErrorCode WAL_PATH_ERROR = ToWalErrorCode(4);

```