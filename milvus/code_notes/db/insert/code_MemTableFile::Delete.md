#1.MemTableFile::Delete

```
MemTableFile::Delete
--segment_writer_ptr_->GetSegment(segment_ptr);
--// Check wither the doc_id is present, if yes, delete it's corresponding buffer
--std::vector<segment::doc_id_t> temp;
--temp.resize(doc_ids.size());
--memcpy(temp.data(), doc_ids.data(), doc_ids.size() * sizeof(segment::doc_id_t));
--std::sort(temp.begin(), temp.end());
--auto uids = segment_ptr->vectors_ptr_->GetUids();
--size_t loop = uids.size();
--for (size_t i = 0; i < loop; ++i) {
----if (std::binary_search(temp.begin(), temp.end(), uids[i])) {
------segment_ptr->vectors_ptr_->Erase(i - deleted);
--------Vectors::Erase
------++deleted;

```