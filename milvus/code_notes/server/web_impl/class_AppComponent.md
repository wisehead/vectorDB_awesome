#1.class AppComponent

```cpp
class AppComponent {

 public:

    explicit AppComponent(int port) : port_(port) {
    }

 private:
    const int port_;

 public:
    OATPP_CREATE_COMPONENT(std::shared_ptr<oatpp::network::ServerConnectionProvider>, server_connection_provider_)
    ([this] {
        try {
            return oatpp::network::server::SimpleTCPConnectionProvider::createShared(this->port_);
        } catch (std::exception& e) {
            std::string error_msg = "Cannot bind http port " + std::to_string(this->port_) + ". " + e.what() +
                "(errno: " + std::to_string(errno) + ", details: " + strerror(errno) + ")";
            std::cerr << error_msg << std::endl;
            throw std::runtime_error(error_msg);
        }
    }());

    OATPP_CREATE_COMPONENT(std::shared_ptr<oatpp::network::ClientConnectionProvider>, client_connection_provider_)
    ([this] {
        return oatpp::network::client::SimpleTCPConnectionProvider::createShared("localhost", this->port_);
    }());

    OATPP_CREATE_COMPONENT(std::shared_ptr<oatpp::web::server::HttpRouter>, http_router_)([] {
        return oatpp::web::server::HttpRouter::createShared();
    }());

    OATPP_CREATE_COMPONENT(std::shared_ptr<oatpp::network::server::ConnectionHandler>, server_connection_handler_)([] {
        OATPP_COMPONENT(std::shared_ptr<oatpp::web::server::HttpRouter>, router);
        return oatpp::web::server::HttpConnectionHandler::createShared(router);
    }());

    OATPP_CREATE_COMPONENT(std::shared_ptr<oatpp::data::mapping::ObjectMapper>, api_object_mapper_)([] {
        auto serializerConfig = oatpp::parser::json::mapping::Serializer::Config::createShared();
        auto deserializerConfig = oatpp::parser::json::mapping::Deserializer::Config::createShared();
        deserializerConfig->allowUnknownFields = false;
        return oatpp::parser::json::mapping::ObjectMapper::createShared(serializerConfig, deserializerConfig);
    }());
};
```