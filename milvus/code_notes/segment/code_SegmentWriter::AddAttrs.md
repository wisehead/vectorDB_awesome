#1.SegmentWriter::AddAttrs

```
SegmentWriter::AddAttrs
--auto attr_data_it = attr_data.begin();
--auto attrs = segment_ptr_->attrs_ptr_->attrs;
--for (; attr_data_it != attr_data.end(); ++attr_data_it) {
----AttrPtr attr = std::make_shared<Attr>(attr_data_it->second, attr_nbytes.at(attr_data_it->first), uids,
                                              attr_data_it->first);
----segment_ptr_->attrs_ptr_->attrs.insert(std::make_pair(attr_data_it->first, attr));
```