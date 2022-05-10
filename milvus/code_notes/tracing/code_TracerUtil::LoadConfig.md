#1.TracerUtil::LoadConfig

```
TracerUtil::LoadConfig
--std::ifstream tracer_config(config_path);// Parse JSON config
--using json = nlohmann::json;
--json tracer_config_json;
--tracer_config >> tracer_config_json;
--std::string tracing_shared_lib = tracer_config_json[TRACER_LIBRARY_CONFIG_NAME];
--std::string tracer_config_str = tracer_config_json[TRACER_CONFIGURATION_CONFIG_NAME].dump();
--tracer_context_header_name_ = tracer_config_json[TRACE_CONTEXT_HEADER_CONFIG_NAME].dump().c_str();
-- // Load the tracer library.
--handle_maybe = opentracing::DynamicallyLoadTracingLibrary(tracing_shared_lib.c_str(), error_message);
--// Construct a tracer.
--tracer_factory = handle_maybe->tracer_factory();
--tracer_maybe = tracer_factory.MakeTracer(tracer_config_str.c_str(), error_message);
--auto& tracer = *tracer_maybe;
--opentracing::Tracer::InitGlobal(tracer);
```