# How to build a Java project with modules the old-school way
2 modules: `api` and `service`. `api` depends on (requires) `service`.

Compile the service class and module (has to be compiled as well). 
Output to `service/target/classes`.
```bash
javac \
    -d service/target/classes \
    service/src/module-info.java \
    service/src/example/service/Service.java
```

Compile the API class and module. 
Output to `service/target/classes`.
Pass a path to the `service` module that `api` depends on.
```bash
javac \
    -d api/target/classes \
    api/src/module-info.java \
    api/src/example/api/API.java \
    --module-path service/target/classes/
```

Run the `api` module with main class `example.api.API` specified. 
Pass all required classes and modules in the `module-path` (colon-separated).
```bash
java \
    --module-path service/target/classes/:api/target/classes/ \
    --module api/example.api.API
```
