---
title: "Overview"
date: 2020-09-10T08:22:12+02:00
weight: 1
---

An ASP.NET Identity-based implementation is provided for managing the identity database for users of IdentityServer.
This implementation implements the extensibility points in IdentityServer needed to load identity data for your users to emit claims into tokens.

To use this library, configure ASP.NET Identity normally. 
Then use the ``AddAspNetIdentity`` extension method after the call to ``AddIdentityServer``::

    public void ConfigureServices(IServiceCollection services)
    {
        services.AddIdentity<ApplicationUser, IdentityRole>()
            .AddEntityFrameworkStores<ApplicationDbContext>()
            .AddDefaultTokenProviders();

        services.AddIdentityServer()
            .AddAspNetIdentity<ApplicationUser>();
    }

``AddAspNetIdentity`` requires as a generic parameter the class that models your user for ASP.NET Identity (and the same one passed to ``AddIdentity`` to configure ASP.NET Identity).
This configures IdentityServer to use the ASP.NET Identity implementations of ``IUserClaimsPrincipalFactory``, ``IResourceOwnerPasswordValidator``, and ``IProfileService``.
It also configures some of ASP.NET Identity's options for use with IdentityServer (such as claim types to use and authentication cookie settings).

When using your own implementation of ``IUserClaimsPrincipalFactory``, make sure that you register it before calling the IdentityServer ``AddAspNetIdentity`` extension method.