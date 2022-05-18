#1.WebServer::StartService

```
WebServer::StartService
--oatpp::base::Environment::init();
--AppComponent components = AppComponent(std::stoi(port));
--/* create ApiControllers and add endpoints to router */
--auto user_controller = WebController::createShared();
--auto router = components.http_router_.getObject();
--user_controller->addEndpointsToRouter(router);
--/* Get connection handler component */
--auto connection_handler = components.server_connection_handler_.getObject();

--/* Get connection provider component */
--auto connection_provider = components.server_connection_provider_.getObject();

--/* create server */
--auto server = oatpp::network::server::Server(connection_provider, connection_handler);
--std::thread stop_thread([&server, this] {
            while (!this->try_stop_.load()) {
                std::this_thread::sleep_for(std::chrono::milliseconds(50));
            }

            server.stop();
            OATPP_COMPONENT(std::shared_ptr<oatpp::network::ClientConnectionProvider>, client_provider);
            client_provider->getConnection();
        });

--// start synchronously
--server.run();
--connection_handler->stop();
--stop_thread.join();
--oatpp::base::Environment::destroy();
```