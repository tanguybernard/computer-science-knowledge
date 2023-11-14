# Modular Modulith

## Communication

- Asynchronous via events (Event-Driven architecture). Each module sends or subscribes to certain events via Events Bus. This Events Bus can be in memory mechanism or out-of-process component - depending on the needs.
- Synchronous with in memory calls. Here, as in the case of API communication with modules, it can be implemented in a traditional approach or CQRS-style (Commands / Queries). What is important here is that such integration should be explicit - by creating a Gate (adapter) on the consumer side and a Facade (port and its implementation) on the supplier side.

https://medium.com/reevoo-engineering/domain-driven-monolith-35d902ee9f80

https://www.kamilgrzybek.com/blog/posts/modular-monolith-domain-centric-design
