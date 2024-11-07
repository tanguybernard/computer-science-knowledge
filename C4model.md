# C4 Model


## Modeling vs Diagramming


Before we dive deeper into the C4 model, it’s important to understand the difference between modeling and diagramming. Modeling is the act of describing the system, including its actors, systems, containers, components, and their relationships. It focuses on capturing the structure and behavior of the system. On the other hand, diagramming is the process of visually representing the model. It involves creating diagrams that depict the different elements of the model in a clear and understandable way.

The distinction between modeling and diagramming becomes powerful when we can create a single model and reuse different elements of it in multiple diagrams. This allows us to apply the DRY (Don’t Repeat Yourself) principle to our diagrams, making them more maintainable and reducing duplication of effort.

source: https://sheldonrcohen.medium.com/understanding-the-c4-model-for-software-architecture-documentation-e59c4edd0d56



## 1. Context Diagram

## 2. Container Diagram

### Container

- Web Application
- API Server
- Database
- Message Broker
- Admin Console (ex: Dedicated interface for administrators to manage inventory and orders)

## 3. Composant Diagram

OrderController, OrderService, OrderRepository...

## 4. Code Diagram

## Sources

E-commerce example

https://mattjhayes.com/2020/05/10/diagrams-with-c4-model/

https://github.com/mattjhayes/PlantUML-Examples/tree/master/docs/Misc/BlogSource/C4Model



https://medium.com/@shubhadeepchat/the-c4-model-for-software-architecture-visualization-explained-93b85ea3e2e3

https://sheldonrcohen.medium.com/understanding-the-c4-model-for-software-architecture-documentation-e59c4edd0d56
