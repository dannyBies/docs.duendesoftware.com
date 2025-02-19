---
title: "Issuing internal Tokens"
date: 2020-09-10T08:22:12+02:00
weight: 45
---

Sometimes, extensibility code running on your IdentityServer needs access tokens to call other APIs. In this case is is not necessary to use the protocol endoints. The tokens can be issued internally.

The *IdentityServerTools* class is a collection of useful internal tools that you might need when writing extensibility code
for IdentityServer. To use it, inject it into your code, e.g. a controller::

    public MyController(IdentityServerTools tools)
    {
        _tools = tools;
    }

The *IssueJwtAsync* method allows creating JWT tokens using the IdentityServer token creation engine. The *IssueClientJwtAsync* is an easier
version of that for creating tokens for server-to-server communication (e.g. when you have to call an IdentityServer protected API from your code):

```cs
public async Task<IActionResult> MyAction()
{
    var token = await _tools.IssueClientJwtAsync(
        clientId: "client_id",
        lifetime: 3600,
        audiences: new[] { "backend.api" });

    // more code
}
```