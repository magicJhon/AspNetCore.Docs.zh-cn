---
title: 托管和部署 ASP.NET Core Blazor Server
author: guardrex
description: 了解如何使用 ASP.NET Core 托管和部署 Blazor Server 应用。
monikerRange: '>= aspnetcore-3.1'
ms.author: riande
ms.custom: mvc
ms.date: 06/04/2020
no-loc:
- Blazor
- Identity
- Let's Encrypt
- Razor
- SignalR
uid: blazor/host-and-deploy/server
ms.openlocfilehash: 891714250bc4e8b0b241e589efb268b8f8e9f0d5
ms.sourcegitcommit: 490434a700ba8c5ed24d849bd99d8489858538e3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2020
ms.locfileid: "85103176"
---
# <a name="host-and-deploy-blazor-server"></a><span data-ttu-id="ca077-103">托管和部署 Blazor Server</span><span class="sxs-lookup"><span data-stu-id="ca077-103">Host and deploy Blazor Server</span></span>

<span data-ttu-id="ca077-104">作者：[Luke Latham](https://github.com/guardrex)、[Rainer Stropek](https://www.timecockpit.com) 和 [Daniel Roth](https://github.com/danroth27)</span><span class="sxs-lookup"><span data-stu-id="ca077-104">By [Luke Latham](https://github.com/guardrex), [Rainer Stropek](https://www.timecockpit.com), and [Daniel Roth](https://github.com/danroth27)</span></span>

## <a name="host-configuration-values"></a><span data-ttu-id="ca077-105">主机配置值</span><span class="sxs-lookup"><span data-stu-id="ca077-105">Host configuration values</span></span>

<span data-ttu-id="ca077-106">[Blazor Server 应用](xref:blazor/hosting-models#blazor-server)可以接受[通用主机配置值](xref:fundamentals/host/generic-host#host-configuration)。</span><span class="sxs-lookup"><span data-stu-id="ca077-106">[Blazor Server apps](xref:blazor/hosting-models#blazor-server) can accept [Generic Host configuration values](xref:fundamentals/host/generic-host#host-configuration).</span></span>

## <a name="deployment"></a><span data-ttu-id="ca077-107">部署</span><span class="sxs-lookup"><span data-stu-id="ca077-107">Deployment</span></span>

<span data-ttu-id="ca077-108">使用 [Blazor Server 托管模型](xref:blazor/hosting-models#blazor-server)，可从 ASP.NET Core 应用中在服务器上执行 Blazor。</span><span class="sxs-lookup"><span data-stu-id="ca077-108">Using the [Blazor Server hosting model](xref:blazor/hosting-models#blazor-server), Blazor is executed on the server from within an ASP.NET Core app.</span></span> <span data-ttu-id="ca077-109">UI 更新、事件处理和 JavaScript 调用是通过 [SignalR](xref:signalr/introduction) 连接进行处理。</span><span class="sxs-lookup"><span data-stu-id="ca077-109">UI updates, event handling, and JavaScript calls are handled over a [SignalR](xref:signalr/introduction) connection.</span></span>

<span data-ttu-id="ca077-110">能够托管 ASP.NET Core 应用的 Web 服务器是必需的。</span><span class="sxs-lookup"><span data-stu-id="ca077-110">A web server capable of hosting an ASP.NET Core app is required.</span></span> <span data-ttu-id="ca077-111">Visual Studio 包括“Blazor Server 应用”\*\*\*\* 项目模板（使用 [dotnet new](/dotnet/core/tools/dotnet-new) 命令时为 `blazorserverside` 模板）。</span><span class="sxs-lookup"><span data-stu-id="ca077-111">Visual Studio includes the **Blazor Server App** project template (`blazorserverside` template when using the [dotnet new](/dotnet/core/tools/dotnet-new) command).</span></span>

## <a name="scalability"></a><span data-ttu-id="ca077-112">可伸缩性</span><span class="sxs-lookup"><span data-stu-id="ca077-112">Scalability</span></span>

<span data-ttu-id="ca077-113">计划部署以将可用的基础设施充分用于 Blazor Server 应用。</span><span class="sxs-lookup"><span data-stu-id="ca077-113">Plan a deployment to make the best use of the available infrastructure for a Blazor Server app.</span></span> <span data-ttu-id="ca077-114">请参阅以下资源来解决 Blazor Server 应用的可伸缩性：</span><span class="sxs-lookup"><span data-stu-id="ca077-114">See the following resources to address Blazor Server app scalability:</span></span>

* <span data-ttu-id="ca077-115">[Blazor Server 应用的基础知识](xref:blazor/hosting-models#blazor-server)</span><span class="sxs-lookup"><span data-stu-id="ca077-115">[Fundamentals of Blazor Server apps](xref:blazor/hosting-models#blazor-server)</span></span>
* <xref:blazor/security/server/threat-mitigation>

### <a name="deployment-server"></a><span data-ttu-id="ca077-116">部署服务器</span><span class="sxs-lookup"><span data-stu-id="ca077-116">Deployment server</span></span>

<span data-ttu-id="ca077-117">考虑单一服务器（纵向扩展）的可伸缩性时，应用可用的内存可能是用户需求增加时应用将耗尽的第一个资源。</span><span class="sxs-lookup"><span data-stu-id="ca077-117">When considering the scalability of a single server (scale up), the memory available to an app is likely the first resource that the app will exhaust as user demands increase.</span></span> <span data-ttu-id="ca077-118">服务器上的可用内存影响以下因素：</span><span class="sxs-lookup"><span data-stu-id="ca077-118">The available memory on the server affects the:</span></span>

* <span data-ttu-id="ca077-119">服务器可以支持的主动电路数。</span><span class="sxs-lookup"><span data-stu-id="ca077-119">Number of active circuits that a server can support.</span></span>
* <span data-ttu-id="ca077-120">客户端上的 UI 延迟。</span><span class="sxs-lookup"><span data-stu-id="ca077-120">UI latency on the client.</span></span>

<span data-ttu-id="ca077-121">有关生成安全且可伸缩的 Blazor 服务器应用的指南，请参阅 <xref:blazor/security/server/threat-mitigation>。</span><span class="sxs-lookup"><span data-stu-id="ca077-121">For guidance on building secure and scalable Blazor server apps, see <xref:blazor/security/server/threat-mitigation>.</span></span>

<span data-ttu-id="ca077-122">每个电路使用约 250 KB 的内存来实现至少为 Hello World \*\* 样式的应用。</span><span class="sxs-lookup"><span data-stu-id="ca077-122">Each circuit uses approximately 250 KB of memory for a minimal *Hello World*-style app.</span></span> <span data-ttu-id="ca077-123">电路大小取决于应用代码和与每个组件相关的状态维护要求。</span><span class="sxs-lookup"><span data-stu-id="ca077-123">The size of a circuit depends on the app's code and the state maintenance requirements associated with each component.</span></span> <span data-ttu-id="ca077-124">我们建议你在开发应用和基础设施的过程中衡量资源需求，但在计划部署目标时可以将以下基准作为起点：如果希望应用支持 5,000 个并发用户，请考虑为应用预算至少 1.3 GB 服务器内存（或每用户 ~273 KB）。</span><span class="sxs-lookup"><span data-stu-id="ca077-124">We recommend that you measure resource demands during development for your app and infrastructure, but the following baseline can be a starting point in planning your deployment target: If you expect your app to support 5,000 concurrent users, consider budgeting at least 1.3 GB of server memory to the app (or ~273 KB per user).</span></span>

### <a name="signalr-configuration"></a>SignalR<span data-ttu-id="ca077-125"> 配置</span><span class="sxs-lookup"><span data-stu-id="ca077-125"> configuration</span></span>

Blazor<span data-ttu-id="ca077-126"> Server 应用使用 ASP.NET Core SignalR 与浏览器进行通信。</span><span class="sxs-lookup"><span data-stu-id="ca077-126"> Server apps use ASP.NET Core SignalR to communicate with the browser.</span></span> <span data-ttu-id="ca077-127">[SignalR 的托管和缩放条件 ](xref:signalr/publish-to-azure-web-app) 适用于 Blazor Server 应用。</span><span class="sxs-lookup"><span data-stu-id="ca077-127">[SignalR's hosting and scaling conditions](xref:signalr/publish-to-azure-web-app) apply to Blazor Server apps.</span></span>

<span data-ttu-id="ca077-128">由于低延迟、可靠性和[安全性](xref:signalr/security)，使用 WebSocket 作为 SignalR 传输时，Blazor 的效果最佳。</span><span class="sxs-lookup"><span data-stu-id="ca077-128">Blazor works best when using WebSockets as the SignalR transport due to lower latency, reliability, and [security](xref:signalr/security).</span></span> <span data-ttu-id="ca077-129">当 WebSocket 不可用时，或在将应用显式配置为使用长轮询时，SignalR 将使用长轮询。</span><span class="sxs-lookup"><span data-stu-id="ca077-129">Long Polling is used by SignalR when WebSockets isn't available or when the app is explicitly configured to use Long Polling.</span></span> <span data-ttu-id="ca077-130">部署到 Azure 应用服务时，请在服务的 Azure 门户设置中将应用配置为使用 WebSocket。</span><span class="sxs-lookup"><span data-stu-id="ca077-130">When deploying to Azure App Service, configure the app to use WebSockets in the Azure portal settings for the service.</span></span> <span data-ttu-id="ca077-131">有关为 Azure 应用服务配置应用的详细信息，请参阅 [SignalR 发布指南](xref:signalr/publish-to-azure-web-app)。</span><span class="sxs-lookup"><span data-stu-id="ca077-131">For details on configuring the app for Azure App Service, see the [SignalR publishing guidelines](xref:signalr/publish-to-azure-web-app).</span></span>

#### <a name="azure-signalr-service"></a><span data-ttu-id="ca077-132">Azure SignalR 服务</span><span class="sxs-lookup"><span data-stu-id="ca077-132">Azure SignalR Service</span></span>

<span data-ttu-id="ca077-133">我们建议将 [Azure SignalR 服务](/azure/azure-signalr)用于 Blazor Server 应用。</span><span class="sxs-lookup"><span data-stu-id="ca077-133">We recommend using the [Azure SignalR Service](/azure/azure-signalr) for Blazor Server apps.</span></span> <span data-ttu-id="ca077-134">该服务允许将 Blazor Server 应用扩展到大量并发 SignalR 连接。</span><span class="sxs-lookup"><span data-stu-id="ca077-134">The service allows for scaling up a Blazor Server app to a large number of concurrent SignalR connections.</span></span> <span data-ttu-id="ca077-135">此外，SignalR 服务的全球覆盖和高性能数据中心可帮助显著减少由于地理位置造成的延迟。</span><span class="sxs-lookup"><span data-stu-id="ca077-135">In addition, the SignalR service's global reach and high-performance data centers significantly aid in reducing latency due to geography.</span></span> <span data-ttu-id="ca077-136">若要配置应用（并选择性地预配），Azure SignalR 服务应：</span><span class="sxs-lookup"><span data-stu-id="ca077-136">To configure an app (and optionally provision) the Azure SignalR Service:</span></span>

1. <span data-ttu-id="ca077-137">启用该服务以支持粘滞会话\*\*，在此情况下，客户端在[预呈现时被重定向回同一服务器](xref:blazor/hosting-models#connection-to-the-server)。</span><span class="sxs-lookup"><span data-stu-id="ca077-137">Enable the service to support *sticky sessions*, where clients are [redirected back to the same server when prerendering](xref:blazor/hosting-models#connection-to-the-server).</span></span> <span data-ttu-id="ca077-138">将 `ServerStickyMode` 选项或配置值设置为 `Required`。</span><span class="sxs-lookup"><span data-stu-id="ca077-138">Set the `ServerStickyMode` option or configuration value to `Required`.</span></span> <span data-ttu-id="ca077-139">通常，应用使用下述方法之一创建配置\*\*\*\*：</span><span class="sxs-lookup"><span data-stu-id="ca077-139">Typically, an app creates the configuration using **one** of the following approaches:</span></span>

   * <span data-ttu-id="ca077-140">`Startup.ConfigureServices`：</span><span class="sxs-lookup"><span data-stu-id="ca077-140">`Startup.ConfigureServices`:</span></span>
  
     ```csharp
     services.AddSignalR().AddAzureSignalR(options =>
     {
         options.ServerStickyMode = 
             Microsoft.Azure.SignalR.ServerStickyMode.Required;
     });
     ```

   * <span data-ttu-id="ca077-141">配置（使用下述方法之一）\*\*\*\*：</span><span class="sxs-lookup"><span data-stu-id="ca077-141">Configuration (use **one** of the following approaches):</span></span>
  
     * <span data-ttu-id="ca077-142">appsettings.json\*\*：</span><span class="sxs-lookup"><span data-stu-id="ca077-142">*appsettings.json*:</span></span>

       ```json
       "Azure:SignalR:ServerStickyMode": "Required"
       ```

     * <span data-ttu-id="ca077-143">Azure 门户中的应用服务“配置” > “应用程序设置”（名称：`Azure:SignalR:ServerStickyMode`，值：`Required`）\*\*\*\* \*\*\*\* \*\*\*\* \*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="ca077-143">The app service's **Configuration** > **Application settings** in the Azure portal (**Name**: `Azure:SignalR:ServerStickyMode`, **Value**: `Required`).</span></span>

1. <span data-ttu-id="ca077-144">在 Visual Studio 中创建适用于 Blazor Server 应用的 Azure 应用发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="ca077-144">Create an Azure Apps publish profile in Visual Studio for the Blazor Server app.</span></span>
1. <span data-ttu-id="ca077-145">将 **Azure SignalR 服务**依赖项添加到配置文件。</span><span class="sxs-lookup"><span data-stu-id="ca077-145">Add the **Azure SignalR Service** dependency to the profile.</span></span> <span data-ttu-id="ca077-146">如果 Azure 订阅没有要分配给应用的预先存在的 Azure SignalR 服务实例，请选择“创建新的 Azure SignalR 服务实例”\*\*\*\* 以预配新的服务实例。</span><span class="sxs-lookup"><span data-stu-id="ca077-146">If the Azure subscription doesn't have a pre-existing Azure SignalR Service instance to assign to the app, select **Create a new Azure SignalR Service instance** to provision a new service instance.</span></span>
1. <span data-ttu-id="ca077-147">将应用发布到 Azure。</span><span class="sxs-lookup"><span data-stu-id="ca077-147">Publish the app to Azure.</span></span>

#### <a name="iis"></a><span data-ttu-id="ca077-148">IIS</span><span class="sxs-lookup"><span data-stu-id="ca077-148">IIS</span></span>

<span data-ttu-id="ca077-149">使用 IIS 时，请启用：</span><span class="sxs-lookup"><span data-stu-id="ca077-149">When using IIS, enable:</span></span>

* <span data-ttu-id="ca077-150">[IIS 上的 WebSocket](xref:fundamentals/websockets#enabling-websockets-on-iis)。</span><span class="sxs-lookup"><span data-stu-id="ca077-150">[WebSockets on IIS](xref:fundamentals/websockets#enabling-websockets-on-iis).</span></span>
* <span data-ttu-id="ca077-151">[具有应用程序请求路由的粘性会话](/iis/extensions/configuring-application-request-routing-arr/http-load-balancing-using-application-request-routing)。</span><span class="sxs-lookup"><span data-stu-id="ca077-151">[Sticky sessions with Application Request Routing](/iis/extensions/configuring-application-request-routing-arr/http-load-balancing-using-application-request-routing).</span></span>

#### <a name="kubernetes"></a><span data-ttu-id="ca077-152">Kubernetes</span><span class="sxs-lookup"><span data-stu-id="ca077-152">Kubernetes</span></span>

<span data-ttu-id="ca077-153">使用以下[粘滞会话的 Kubernetes 注释](https://kubernetes.github.io/ingress-nginx/examples/affinity/cookie/)创建入口定义：</span><span class="sxs-lookup"><span data-stu-id="ca077-153">Create an ingress definition with the following [Kubernetes annotations for sticky sessions](https://kubernetes.github.io/ingress-nginx/examples/affinity/cookie/):</span></span>

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: <ingress-name>
  annotations:
    nginx.ingress.kubernetes.io/affinity: "cookie"
    nginx.ingress.kubernetes.io/session-cookie-name: "affinity"
    nginx.ingress.kubernetes.io/session-cookie-expires: "14400"
    nginx.ingress.kubernetes.io/session-cookie-max-age: "14400"
```

#### <a name="linux-with-nginx"></a><span data-ttu-id="ca077-154">Linux 与 Nginx</span><span class="sxs-lookup"><span data-stu-id="ca077-154">Linux with Nginx</span></span>

<span data-ttu-id="ca077-155">要使 SignalR Websocket 正常运行，请确保将代理的 `Upgrade` 和 `Connection` 标头设置为以下值，并将 `$connection_upgrade` 映射到以下值之一：</span><span class="sxs-lookup"><span data-stu-id="ca077-155">For SignalR WebSockets to function properly, confirm that the proxy's `Upgrade` and `Connection` headers are set to the following values and that `$connection_upgrade` is mapped to either:</span></span>

* <span data-ttu-id="ca077-156">默认情况下为升级标头值。</span><span class="sxs-lookup"><span data-stu-id="ca077-156">The Upgrade header value by default.</span></span>
* <span data-ttu-id="ca077-157">缺少升级标头或升级标头为空时为 `close`。</span><span class="sxs-lookup"><span data-stu-id="ca077-157">`close` when the Upgrade header is missing or empty.</span></span>

```
http {
    map $http_upgrade $connection_upgrade {
        default Upgrade;
        ''      close;
    }

    server {
        listen      80;
        server_name example.com *.example.com
        location / {
            proxy_pass         http://localhost:5000;
            proxy_http_version 1.1;
            proxy_set_header   Upgrade $http_upgrade;
            proxy_set_header   Connection $connection_upgrade;
            proxy_set_header   Host $host;
            proxy_cache_bypass $http_upgrade;
            proxy_set_header   X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header   X-Forwarded-Proto $scheme;
        }
    }
}
```

<span data-ttu-id="ca077-158">有关详细信息，请参阅以下文章：</span><span class="sxs-lookup"><span data-stu-id="ca077-158">For more information, see the following articles:</span></span>

* [<span data-ttu-id="ca077-159">NGINX 作为 WebSocket 代理</span><span class="sxs-lookup"><span data-stu-id="ca077-159">NGINX as a WebSocket Proxy</span></span>](https://www.nginx.com/blog/websocket-nginx/)
* [<span data-ttu-id="ca077-160">WebSocket 代理</span><span class="sxs-lookup"><span data-stu-id="ca077-160">WebSocket proxying</span></span>](http://nginx.org/docs/http/websocket.html)
* <xref:host-and-deploy/linux-nginx>

## <a name="linux-with-apache"></a><span data-ttu-id="ca077-161">Linux 与 Apache</span><span class="sxs-lookup"><span data-stu-id="ca077-161">Linux with Apache</span></span>

<span data-ttu-id="ca077-162">若要在 Linux 上托管 Apache 后面的 Blazor 应用，请为 HTTP 和 WebSocket 流量配置 `ProxyPass`。</span><span class="sxs-lookup"><span data-stu-id="ca077-162">To host a Blazor app behind Apache on Linux, configure `ProxyPass` for HTTP and WebSockets traffic.</span></span>

<span data-ttu-id="ca077-163">如下示例中：</span><span class="sxs-lookup"><span data-stu-id="ca077-163">In the following example:</span></span>

* <span data-ttu-id="ca077-164">Kestrel 服务器正在主机上运行。</span><span class="sxs-lookup"><span data-stu-id="ca077-164">Kestrel server is running on the host machine.</span></span>
* <span data-ttu-id="ca077-165">应用侦听端口 5000 上的流量。</span><span class="sxs-lookup"><span data-stu-id="ca077-165">The app listens for traffic on port 5000.</span></span>

```
ProxyRequests       On
ProxyPreserveHost   On
ProxyPassMatch      ^/_blazor/(.*) http://localhost:5000/_blazor/$1
ProxyPass           /_blazor ws://localhost:5000/_blazor
ProxyPass           / http://localhost:5000/
ProxyPassReverse    / http://localhost:5000/
```

<span data-ttu-id="ca077-166">启用以下模块：</span><span class="sxs-lookup"><span data-stu-id="ca077-166">Enable the following modules:</span></span>

```
a2enmod   proxy
a2enmod   proxy_wstunnel
```

<span data-ttu-id="ca077-167">检查浏览器控制台中的 WebSocket 错误。</span><span class="sxs-lookup"><span data-stu-id="ca077-167">Check the browser console for WebSockets errors.</span></span> <span data-ttu-id="ca077-168">示例错误：</span><span class="sxs-lookup"><span data-stu-id="ca077-168">Example errors:</span></span>

* <span data-ttu-id="ca077-169">Firefox 无法通过 ws://the-domain-name.tld/_blazor?id=XXX 与服务器建立连接。</span><span class="sxs-lookup"><span data-stu-id="ca077-169">Firefox can't establish a connection to the server at ws://the-domain-name.tld/_blazor?id=XXX.</span></span>
* <span data-ttu-id="ca077-170">错误：未能启动传输“WebSocket”：错误：传输出现错误。</span><span class="sxs-lookup"><span data-stu-id="ca077-170">Error: Failed to start the transport 'WebSockets': Error: There was an error with the transport.</span></span>
* <span data-ttu-id="ca077-171">错误：未能启动传输“LongPolling”：TypeError：未定义 this.transport</span><span class="sxs-lookup"><span data-stu-id="ca077-171">Error: Failed to start the transport 'LongPolling': TypeError: this.transport is undefined</span></span>
* <span data-ttu-id="ca077-172">错误：无法使用任何可用传输连接到服务器。</span><span class="sxs-lookup"><span data-stu-id="ca077-172">Error: Unable to connect to the server with any of the available transports.</span></span> <span data-ttu-id="ca077-173">WebSocket 失败</span><span class="sxs-lookup"><span data-stu-id="ca077-173">WebSockets failed</span></span>
* <span data-ttu-id="ca077-174">错误：如果连接未处于“已连接”状态，则无法发送数据。</span><span class="sxs-lookup"><span data-stu-id="ca077-174">Error: Cannot send data if the connection is not in the 'Connected' State.</span></span>

<span data-ttu-id="ca077-175">有关详细信息，请参阅 [Apache 文档](https://httpd.apache.org/docs/current/mod/mod_proxy.html)。</span><span class="sxs-lookup"><span data-stu-id="ca077-175">For more information, see the [Apache documentation](https://httpd.apache.org/docs/current/mod/mod_proxy.html).</span></span>

### <a name="measure-network-latency"></a><span data-ttu-id="ca077-176">衡量网络延迟</span><span class="sxs-lookup"><span data-stu-id="ca077-176">Measure network latency</span></span>

<span data-ttu-id="ca077-177">可以使用 [JS 互操作](xref:blazor/call-javascript-from-dotnet)来衡量网络延迟，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="ca077-177">[JS interop](xref:blazor/call-javascript-from-dotnet) can be used to measure network latency, as the following example demonstrates:</span></span>

```razor
@inject IJSRuntime JS

@if (latency is null)
{
    <span>Calculating...</span>
}
else
{
    <span>@(latency.Value.TotalMilliseconds)ms</span>
}

@code
{
    private DateTime startTime;
    private TimeSpan? latency;

    protected override async Task OnInitializedAsync()
    {
        startTime = DateTime.UtcNow;
        var _ = await JS.InvokeAsync<string>("toString");
        latency = DateTime.UtcNow - startTime;
    }
}
```

<span data-ttu-id="ca077-178">为获得合理的 UI 体验，我们建议使用 250 毫秒或更低的持续 UI 延迟。</span><span class="sxs-lookup"><span data-stu-id="ca077-178">For a reasonable UI experience, we recommend a sustained UI latency of 250ms or less.</span></span>