---
title: Create a Ninject Kernel that provides VsServices
author: sven
layout: article
permalink: /blog/2013/11/howto-create-a-ninject-kernel-that-provides-vsservices/
categories:
  - 'C#'
  - Ninject
  - Visual Studio
tags:
  - dependency injection
---
Making Visual Studio services available in a Ninject Kernel is actually a fairly easy task. All you need to do is to implement an `IMissingBindingResolver` (let&#8217;s call it `VsServiceResolver`) and register it to the kernel with

<pre class="brush: csharp; title: ; notranslate" title="">kernel.Components.Add&lt;IMissingBindingResolver, VsServiceResolver&gt;();</pre>

Since we don&#8217;t create the resolver instance ourselves, we cannot pass it a reference to the current package for service lookup. Instead, we need to fall back to resolving services by a static call to `Package.GetGlobalService()`. This implies, that VsPackage-local services cannot be retrieved by this approach.

The resolver implementation itself is straightforward:

<pre class="brush: csharp; title: ; notranslate" title="">class VsServiceResolver : NinjectComponent, IMissingBindingResolver
{
    public IEnumerable&lt;IBinding&gt; Resolve(Multimap&lt;Type, IBinding&gt; bindings, IRequest request)
    {
        var service = Package.GetGlobalService(request.Service);
        if (service != null)
        {
            return new[]
            {
                new Binding(requestType)
                {
                    ProviderCallback =
                        context =&gt;
                        {
                            return new ConstantProvider&lt;object&gt;(service);
                        }
                }
            };
        }
        return Enumerable.Empty&lt;IBinding&gt;();
    }
}</pre>

Note that this resolver implementation is rather naive and probably not optimal in terms of performance, since it will try to resolve a service even if the `request.Service` type is not a service interface. If you want to make only certain service available to the kernel, I&#8217;d recommend you to check whether the requested type is one of the respective service interfaces. A more general approach could be to check if the `request.Service`&#8216;s name starts with a capital S, since most Visual Studio service interfaces follow this convention. Then, however, you have to take care of special cases, such as the `DTE` interface.