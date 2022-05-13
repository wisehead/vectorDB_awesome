#1.class TraceContext

```cpp
class TraceContext {
 public:
    explicit TraceContext(std::unique_ptr<opentracing::Span>& span);

    std::unique_ptr<TraceContext>
    Child(const std::string& operation_name) const;

    std::unique_ptr<TraceContext>
    Follower(const std::string& operation_name) const;

    const std::unique_ptr<opentracing::Span>&
    GetSpan() const;

 private:
    //    std::unique_ptr<opentracing::SpanContext> span_context_;
    std::unique_ptr<opentracing::Span> span_;
};
```