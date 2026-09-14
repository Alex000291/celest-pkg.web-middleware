# web-middleware

Composable logging, request ID, CORS, security header, body limit, deadline, compression, ETag, authentication, CSRF, rate limit, recovery, and static-file middleware.

```text
cpm install web-middleware@1.0.0
```

```celest
import "web-middleware" as middleware;
app.use(middleware.secureHeaders());
app.use(middleware.bodyLimit(1048576));
```

Each exported constructor returns a middleware Function compatible with `app.use`. `compose` preserves the supplied order; `when` and `unless` conditionally enter one middleware. Security, authentication, CSRF, rate-limit, cache, proxy, static-file, recovery, and response middleware share the request context but keep their own explicit state objects.

Configuration is borrowed by the returned middleware and must outlive the application unless the constructor documents a copy. `staticFiles` and `proxy` can perform filesystem or network I/O and therefore expose native platform failures; pure header and routing middleware are platform-neutral. `timeout` is a request deadline, not forced thread termination. Recovery middleware catches language exceptions but cannot catch fatal runtime faults or undefined behavior.
