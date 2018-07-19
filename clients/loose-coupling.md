# Loose Coupling

In addition to the [robustness principle](https://github.com/adidas-group/api-guidelines/tree/e28e6b756cc7b7bdd2b8784e8ebc2bf452a75377/rest/clients/core-principles/robustness.md), API consumers \(clients\) **MUST** **operate independently** on API implementation's internals. Similarly the API consumers **MUST NOT** **assume** or **rely on** any knowledge of the API service internal implementation.

Where available, the clients **SHOULD** utilize **hypermedia controls as the engine of the application state**, and rely on the **protocol, message and vocabulary semantics**.

