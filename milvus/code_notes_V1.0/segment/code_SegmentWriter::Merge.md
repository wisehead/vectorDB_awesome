#1.SegmentWriter::Merge

```
SegmentWriter::Merge
--SegmentReader segment_reader_to_merge(dir_to_merge);
--auto status = segment_reader_to_merge.LoadCache(in_cache);
--status = segment_reader_to_merge.Load();
----SegmentReader::Load
------default_codec.GetVectorsFormat()->read(fs_ptr_, segment_ptr_->vectors_ptr_);
------default_codec.GetAttrsFormat()->read(fs_ptr_, segment_ptr_->attrs_ptr_);
------default_codec.GetDeletedDocsFormat()->read(fs_ptr_, segment_ptr_->deleted_docs_ptr_);
--segment_reader_to_merge.GetSegment(segment_to_merge);
----SegmentWriter::GetSegment
--if (segment_to_merge->deleted_docs_ptr_ != nullptr) {
----auto offsets_to_delete = segment_to_merge->deleted_docs_ptr_->GetDeletedDocs();
----// Erase from raw data
----segment_to_merge->vectors_ptr_->Erase(offsets_to_delete);
------Vectors::Erase
--AddVectors(name, segment_to_merge->vectors_ptr_->GetData(), segment_to_merge->vectors_ptr_->GetUids());
----SegmentWriter::AddVectors
------segment_ptr_->vectors_ptr_->AddData(data);
      segment_ptr_->vectors_ptr_->AddUids(uids);
      segment_ptr_->vectors_ptr_->SetName(name);
--auto attr_it = segment_to_merge->attrs_ptr_->attrs.begin();
--for (; attr_it != segment_to_merge->attrs_ptr_->attrs.end(); attr_it++) {
----attr_nbytes.insert(std::make_pair(attr_it->first, attr_it->second->GetNbytes()));
----attr_data.insert(std::make_pair(attr_it->first, attr_it->second->GetData()));

        if (segment_to_merge->deleted_docs_ptr_ != nullptr) {
            auto offsets_to_delete = segment_to_merge->deleted_docs_ptr_->GetDeletedDocs();

            // Erase from field data
            attr_it->second->Erase(offsets_to_delete);
        }
    }      
--AddAttrs(name, attr_nbytes, attr_data, segment_to_merge->vectors_ptr_->GetUids());    
```