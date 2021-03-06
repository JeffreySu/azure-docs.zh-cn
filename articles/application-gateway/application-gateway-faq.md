---
title: Azure 应用程序网关常见问题
description: 本页提供有关 Azure 应用程序网关常见问题的解答
services: application-gateway
author: vhorne
ms.service: application-gateway
ms.topic: article
ms.workload: infrastructure-services
ms.date: 3/20/2019
ms.author: victorh
ms.openlocfilehash: c40f372d3574f940e475a6626f998adae37a6d61
ms.sourcegitcommit: 04716e13cc2ab69da57d61819da6cd5508f8c422
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/02/2019
ms.locfileid: "58851156"
---
# <a name="frequently-asked-questions-for-application-gateway"></a>应用程序网关常见问题

[!INCLUDE [updated-for-az](../../includes/updated-for-az.md)]

## <a name="general"></a>常规

### <a name="what-is-application-gateway"></a>什么是应用程序网关？

Azure 应用程序网关是服务形式的应用程序传送控制器 (ADC)，借此为应用程序提供各种第 7 层负载均衡功能。 它提供完全由 Azure 管理的高度可用、可缩放的服务。

### <a name="what-features-does-application-gateway-support"></a>应用程序网关支持哪些功能？

应用程序网关支持自动缩放、SSL 卸载和端到端 SSL、Web 应用程序防火墙、基于 Cookie 的会话相关性、基于 URL 路径的路由、多站点托管，等等。 有关受支持功能的完整列表，请参阅[应用程序网关简介](application-gateway-introduction.md)。

### <a name="what-is-the-difference-between-application-gateway-and-azure-load-balancer"></a>应用程序网关与 Azure 负载均衡器之间有什么区别？

应用程序网关是第 7 层负载均衡器，这意味着它适用于仅用于 web 流量 (HTTP/HTTPS/WebSocket/HTTP/2)。 它支持 SSL 终止、基于 Cookie 的会话相关性以及对流量进行负载均衡的轮循机制等功能。 负载均衡器在第 4 层对流量进行负载均衡 (TCP/UDP)。

### <a name="what-protocols-does-application-gateway-support"></a>应用程序网关支持哪些协议？

应用程序网关支持 HTTP、HTTPS、HTTP/2 和 WebSocket。

### <a name="how-does-application-gateway-support-http2"></a>应用程序网关如何支持 HTTP/2？

请参阅[HTTP/2 支持](https://docs.microsoft.com/azure/application-gateway/configuration-overview#http2-support)若要了解如何应用程序网关支持 HTTP/2 协议。

### <a name="what-resources-are-supported-today-as-part-of-backend-pool"></a>目前支持在后端池中添加哪些资源？

请参阅[支持的后端资源](https://docs.microsoft.com/azure/application-gateway/application-gateway-components#backend-pool)若要了解应用程序网关支持哪些资源。

### <a name="what-regions-is-the-service-available-in"></a>该服务已在哪些区域推出？

应用程序网关已在国际版 Azure 的所有区域推出。 在 [Azure 中国世纪互联](https://www.azure.cn/) 和 [Azure 政府](https://azure.microsoft.com/overview/clouds/government/)中也已推出

### <a name="is-this-a-dedicated-deployment-for-my-subscription-or-is-it-shared-across-customers"></a>应用程序网关是订阅专门的部署，还是在所有客户之间共享？

应用程序网关是虚拟网络中的专用部署。

### <a name="is-http-https-redirection-supported"></a>是否支持 HTTP 到 HTTPS 的重定向？

支持重定向。 若要了解详细信息，请参阅[应用程序网关重定向概述](application-gateway-redirect-overview.md)。

### <a name="in-what-order-are-listeners-processed"></a>按什么顺序处理侦听器？

请参阅[顺序处理侦听器](https://docs.microsoft.com/azure/application-gateway/configuration-overview#order-of-processing-listeners)。

### <a name="where-do-i-find-application-gateways-ip-and-dns"></a>在何处可以找到应用程序网关的 IP 和 DNS？

使用公共 IP 地址作为终结点时，可在公共 IP 地址资源中，或者在门户中应用程序网关的“概述”页上找到此信息。 对于内部 IP 地址，可在“概述”页上找到此信息。

### <a name="what-is-keep-alive-timeout-and-tcp-idle-timeout-setting-on-application-gateway"></a>应用程序网关上的 Keep-Alive 超时和 TCP 空闲超时的设置是什么？

V1 SKU 上保持活动状态的超时值为 120 秒。 v2 SKU 上的保持活动超时是 75 秒的 TCP 空闲超时是前端应用程序网关 VIP 上的 4-最小值默认设置。

### <a name="does-the-ip-or-dns-name-change-over-the-lifetime-of-the-application-gateway"></a>在应用程序网关的生存期内，其 IP 或 DNS 名称是否会变化？

如果停止再启动应用程序网关，则 VIP 可能会变化。 与应用程序网关关联的 DNS 名称在网关的整个生命周期内不会变化。 出于此原因，建议使用 CNAME 别名并使其指向应用程序网关的 DNS 地址。

### <a name="does-application-gateway-support-static-ip"></a>应用程序网关是否支持静态 IP？

是，应用程序网关 v2 SKU 支持静态公共 IP 地址。 v1 SKU 支持静态内部 IP。

### <a name="does-application-gateway-support-multiple-public-ips-on-the-gateway"></a>应用程序网关是否支持在网关上使用多个公共 IP？

应用程序网关仅支持一个公共 IP 地址。

### <a name="how-large-should-i-make-my-subnet-for-application-gateway"></a>应该为应用程序网关创建多大的子网？

请参阅[应用程序网关的子网大小方面的考虑](https://docs.microsoft.com/azure/application-gateway/configuration-overview#size-of-the-subnet)若要了解你的部署所需的子网大小。

### <a name="q-can-i-deploy-more-than-one-application-gateway-resource-to-a-single-subnet"></a>问： 是否可将多个应用程序网关资源部署到单个子网？

是，除了提供给定应用程序网关部署的多个实例以外，还可以在包含不同应用程序网关资源的现有子网中预配另一个唯一的应用程序网关资源。

不支持在同一子网上混合使用 Standard_v2 和标准应用程序网关。

### <a name="does-application-gateway-support-x-forwarded-for-headers"></a>应用程序网关是否支持 x-forwarded-for 标头？

是的。 请参阅[修改请求](https://docs.microsoft.com/azure/application-gateway/how-application-gateway-works#modifications-to-the-request)若要了解有关支持的应用程序网关 x-转发-对于标头。

### <a name="how-long-does-it-take-to-deploy-an-application-gateway-does-my-application-gateway-still-work-when-being-updated"></a>部署应用程序网关需要多长时间？ 更新时我的应用程序网关是否仍正常工作？

预配新的应用程序网关 v1 SKU 部署最多需 20 分钟。 更改实例大小/计数不会出现干扰，且在此期间网关处于活动状态。

预配 V2 SKU 部署可能需要大约 5 到 6 分钟时间。

### <a name="can-exchange-server-be-used-as-backend-with-application-gateway"></a>Exchange 服务器是否可以用作应用程序网关的后端

否，应用程序网关不支持电子邮件协议，如 SMTP、 IMAP 和 POP3。 

## <a name="performance"></a>性能

### <a name="how-does-application-gateway-support-high-availability-and-scalability"></a>应用程序网关如何支持高可用性和可伸缩性？

如果已部署两个或更多个实例，则应用程序网关 v1 SKU 支持高可用性方案。 Azure 将跨更新域和容错域分配这些实例，确保所有实例不会同时发生故障。 为了支持可伸缩性，v1 SKU 将添加同一网关的多个实例来分担负载。

v2 SKU 可以自动确保新实例分布到各个容错域和更新域中。 如果选择了区域冗余，则最新实例还将分布到各个可用性区域中以提供区域性故障复原能力。

### <a name="how-do-i-achieve-dr-scenario-across-data-centers-with-application-gateway"></a>如何使用应用程序网关实现跨数据中心的灾难恢复方案？

客户可以使用流量管理器跨不同数据中心内的多个应用程序网关分配流量。

### <a name="is-autoscaling-supported"></a>是否支持自动缩放？

是，应用程序网关 v2 SKU 支持自动缩放。 有关详细信息，请参阅[自动缩放和区域冗余应用程序网关（公共预览版）](application-gateway-autoscaling-zone-redundant.md)。

### <a name="does-manual-scale-updown-cause-downtime"></a>手动扩展/缩减是否导致停机？

不会出现停机。 实例将跨升级域和容错域分布。

### <a name="does-application-gateway-support-connection-draining"></a>应用程序网关是否支持连接排出？

是的。 可配置连接排出以更改后端池内的成员，而无需中断操作。 这允许继续将现有连接发送到其以前的目标，直到该连接被关闭或可配置超时到期。 连接排出仅等待当前未完成的连接完成。 应用程序网关不了解应用程序会话状态。

### <a name="can-i-change-instance-size-from-medium-to-large-without-disruption"></a>是否可以在不造成中断的情况下，将实例大小从中型更改为大型？

可以。Azure 将跨更新域和容错域分配实例，确保所有实例不会同时发生故障。 为了支持缩放，应用程序网关可添加同一网关的多个实例来分担负载。

## <a name="configuration"></a>配置

### <a name="is-application-gateway-always-deployed-in-a-virtual-network"></a>是否始终要将应用程序网关部署在虚拟网络中？

是的，始终要将应用程序网关部署在虚拟网络子网中。 此子网只能包含应用程序网关。 请参阅[虚拟网络和子网要求](https://docs.microsoft.com/azure/application-gateway/configuration-overview#azure-virtual-network-and-dedicated-subnet)若要了解有关应用程序网关的子网注意事项。

### <a name="can-application-gateway-communicate-with-instances-outside-of-the-virtual-network-it-is-in-or-outside-of-the-subscription-it-is-in"></a>应用程序网关可以与在虚拟网络外部或它所在的订阅外部的实例通信？

只要建立 IP 连接，应用程序网关可以与在虚拟网络外部或订阅中，它是外部的实例通信。 如果打算使用内部 IP 作为后端池成员，则需要使用 [VNET 对等互连](../virtual-network/virtual-network-peering-overview.md)或 [VPN 网关](../vpn-gateway/vpn-gateway-about-vpngateways.md)。

### <a name="can-i-deploy-anything-else-in-the-application-gateway-subnet"></a>是否可以在应用程序网关子网中部署其他任何组件？

不可以。但可以在子网中部署其他应用程序网关。

### <a name="are-network-security-groups-supported-on-the-application-gateway-subnet"></a>应用程序网关子网是否支持网络安全组？

请参阅[应用程序网关子网的网络安全组限制](https://docs.microsoft.com/azure/application-gateway/configuration-overview#network-security-groups-on-the-application-gateway-subnet)了解应用程序网关子网支持网络安全组。

### <a name="are-user-defined-routes-supported-on-the-application-gateway-subnet"></a>应用程序网关子网是否支持用户定义的路由？

请参阅[用户定义的路由限制](https://docs.microsoft.com/azure/application-gateway/configuration-overview#user-defined-routes-supported-on-the-application-gateway-subnet)若要了解有关应用程序网关子网支持用户定义的路由。

### <a name="what-are-the-limits-on-application-gateway-can-i-increase-these-limits"></a>应用程序网关有哪些限制？ 是否可以提高这些限制？

请参阅[应用程序网关限制](../azure-subscription-service-limits.md#application-gateway-limits)来查看限制。

### <a name="can-i-use-application-gateway-for-both-external-and-internal-traffic-simultaneously"></a>是否可以同时对外部和内部流量使用应用程序网关？

可以。每个应用程序网关支持一个内部 IP 和一个外部 IP。

### <a name="is-vnet-peering-supported"></a>是否支持 VNet 对等互连？

是的，支持 VNet 对等互连，这有助于对其他虚拟网络中的流量进行负载均衡。

### <a name="can-i-talk-to-on-premises-servers-when-they-are-connected-by-expressroute-or-vpn-tunnels"></a>如果通过 ExpressRoute 或 VPN 隧道连接本地服务器，是否可与这些服务器通信？

可以，只要允许这种流量。

### <a name="can-i-have-one-backend-pool-serving-many-applications-on-different-ports"></a>是否可以使用一个后端池来为不同端口上的许多应用程序提供服务？

支持微服务体系结构。 需要配置多个 http 设置才能探测不同的端口。

### <a name="do-custom-probes-support-wildcardsregex-on-response-data"></a>自定义探测是否支持对响应数据使用通配符/正则表达式？

自定义探测不支持对响应数据使用通配符或正则表达式。

### <a name="how-are-rules-processed"></a>如何处理规则？

请参阅[的处理规则顺序](https://docs.microsoft.com/azure/application-gateway/configuration-overview#order-of-processing-rules)了解路由规则的原理是在应用程序网关的进程。

### <a name="what-does-the-host-field-for-custom-probes-signify"></a>自定义探测的 Host 字段是什么意思？

Host 字段指定要将探测数据发送到的名称。 仅在应用程序网关上配置了多站点的情况下适用，否则使用“127.0.0.1”。 此值不同于 VM 主机名，它采用 \<协议\>://\<主机\>:\<端口\>\<路径\> 格式。

### <a name="can-i-whitelist-application-gateway-access-to-a-few-source-ips"></a>我可以将某些源 IP 的应用程序网关访问权限列入允许列表吗？

是的。 请参阅[限制对特定源 Ip 的访问](https://docs.microsoft.com/azure/application-gateway/configuration-overview#whitelist-application-gateway-access-to-a-few-source-ips)若要了解如何确保该唯一列入允许列表的源 Ip 可以访问应用程序网关。

### <a name="can-the-same-port-be-used-for-both-public-and-private-facing-listeners"></a>能否对面向公共和面向私人的侦听器使用相同的端口？

否，不支持这样做。

## <a name="configuration---ssl"></a>配置的 SSL

### <a name="what-certificates-are-supported-on-application-gateway"></a>应用程序网关支持哪些证书？

支持自签名证书、CA 证书、EV 证书和通配符证书。

### <a name="what-are-the-current-cipher-suites-supported-by-application-gateway"></a>应用程序网关支持哪些最新的加密套件？

应用程序网关当前支持以下密码套件。 请参阅[在应用程序网关上配置 SSL 策略版本和密码套件](application-gateway-configure-ssl-policy-powershell.md)，了解如何自定义 SSL 选项。

- TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384
- TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
- TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384
- TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
- TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA
- TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA
- TLS_DHE_RSA_WITH_AES_256_GCM_SHA384
- TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
- TLS_DHE_RSA_WITH_AES_256_CBC_SHA
- TLS_DHE_RSA_WITH_AES_128_CBC_SHA
- TLS_RSA_WITH_AES_256_GCM_SHA384
- TLS_RSA_WITH_AES_128_GCM_SHA256
- TLS_RSA_WITH_AES_256_CBC_SHA256
- TLS_RSA_WITH_AES_128_CBC_SHA256
- TLS_RSA_WITH_AES_256_CBC_SHA
- TLS_RSA_WITH_AES_128_CBC_SHA
- TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384
- TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256
- TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384
- TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256
- TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA
- TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA
- TLS_DHE_DSS_WITH_AES_256_CBC_SHA256
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA256
- TLS_DHE_DSS_WITH_AES_256_CBC_SHA
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA
- TLS_RSA_WITH_3DES_EDE_CBC_SHA
- TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA

### <a name="does-application-gateway-also-support-re-encryption-of-traffic-to-the-backend"></a>应用程序网关是否也支持重新加密发往后端的流量？

是的，应用程序网关支持 SSL 卸载和端到端 SSL，因此支持重新加密发往后端的流量。

### <a name="can-i-configure-ssl-policy-to-control-ssl-protocol-versions"></a>是否可以配置 SSL 策略来控制 SSL 协议版本？

是的，可将应用程序网关配置为拒绝 TLS1.0、TLS1.1 和 TLS1.2。 SSL 2.0 和 3.0 默认已禁用，并且不可配置。

### <a name="can-i-configure-cipher-suites-and-policy-order"></a>我是否可以配置密码套件和策略顺序？

是，支持[配置密码套件](application-gateway-ssl-policy-overview.md)。 定义自定义策略时，必须至少启用以下其中一个密码套件。 应用程序网关使用 SHA256 进行后端管理。

* TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256 
* TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
* TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
* TLS_RSA_WITH_AES_128_GCM_SHA256
* TLS_RSA_WITH_AES_256_CBC_SHA256
* TLS_RSA_WITH_AES_128_CBC_SHA256

### <a name="how-many-ssl-certificates-are-supported"></a>支持多少个 SSL 证书？

最多支持 100 个 SSL 证书。

### <a name="how-many-authentication-certificates-for-backend-re-encryption-are-supported"></a>支持使用多少个身份验证证书进行后端重新加密？

最多支持 10 个身份验证证书，默认为 5 个。

### <a name="does-application-gateway-integrate-with-azure-key-vault-natively"></a>应用程序网关是否原生与 Azure Key Vault 集成？

不是，它没有与 Azure Key Vault 集成。

### <a name="how-to-configure-https-listeners-for-com-and-net-sites"></a>如何配置 HTTPS 侦听器的.com 和.net 站点？ 

对于多个基于域的 （基于主机的） 路由，可以创建多站点侦听器，选择 HTTPS 作为侦听器配置中的协议和使用路由规则将侦听器相关联。 有关更多详细信息，请参阅[托管应用程序网关的多个站点](https://docs.microsoft.com/azure/application-gateway/multiple-site-overview)。 

## <a name="configuration---web-application-firewall-waf"></a>配置-Web 应用程序防火墙 (WAF)

### <a name="does-the-waf-sku-offer-all-the-features-available-with-the-standard-sku"></a>WAF SKU 是否提供标准 SKU 所提供的全部功能？

是的，WAF 支持标准 SKU 中的所有功能。

### <a name="what-is-the-crs-version-application-gateway-supports"></a>应用程序网关支持哪个 CRS 版本？

应用程序网关支持 CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) 和 CRS [3.0](application-gateway-crs-rulegroups-rules.md#owasp30)。

### <a name="how-do-i-monitor-waf"></a>如何监视 WAF？

可通过诊断日志记录监视 WAF。有关诊断日志记录的详细信息，请参阅 [Diagnostics Logging and Metrics for Application Gateway](application-gateway-diagnostics.md)（应用程序网关的诊断日志记录和指标）

### <a name="does-detection-mode-block-traffic"></a>检测模式是否会阻止流量？

不会。检测模式仅记录触发了 WAF 规则的流量。

### <a name="can-i-customize-waf-rules"></a>我可以自定义 WAF 规则吗？

可以，WAF 规则可自定义。 有关详细信息，请参阅[自定义 WAF 规则组和规则](application-gateway-customize-waf-rules-portal.md)

### <a name="what-rules-are-currently-available"></a>目前支持哪些规则？

WAF 目前支持 CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) 和 CRS [3.0](application-gateway-crs-rulegroups-rules.md#owasp30)，这些规则针对开放 Web 应用程序安全项目 (OWASP) 识别到的 10 大漏洞中的大多数漏洞提供基准安全要求，相关信息请参阅 [OWASP top 10 Vulnerabilities](https://www.owasp.org/index.php/Top10#OWASP_Top_10_for_2013)（OWASP 10 大漏洞）

* SQL 注入保护

* 跨站点脚本保护

* 常见 Web 攻击保护，例如命令注入、HTTP 请求走私、HTTP 响应拆分和远程文件包含攻击

* 防止 HTTP 协议违反行为

* 防止 HTTP 协议异常行为，例如缺少主机用户代理和接受标头

* 防止自动程序、爬网程序和扫描程序

* 检测常见应用程序错误配置（即 Apache、IIS 等）

### <a name="does-waf-also-support-ddos-prevention"></a>WAF 是否也支持 DDoS 防护？

是的。 可以在部署应用程序网关的 VNet 上启用 DDos 防护。 这可确保还使用 Azure DDos 防护服务保护应用程序网关 VIP。

## <a name="diagnostics-and-logging"></a>诊断和日志记录

### <a name="what-types-of-logs-are-available-with-application-gateway"></a>应用程序网关可以使用哪些类型的日志？

应用程序网关可以使用三种日志。 有关这些日志和其他诊断功能的详细信息，请参阅[应用程序网关的后端运行状况、诊断日志和指标](application-gateway-diagnostics.md)。

* **ApplicationGatewayAccessLog**：访问日志包含提交到应用程序网关前端的每个请求。 数据包括调用方的 IP、请求的 URL、响应延迟、返回代码，以及传入和传出的字节数。每隔 300 秒会收集一次访问日志。 此日志包含每个应用程序网关实例的一条记录。
* **ApplicationGatewayPerformanceLog**：性能日志捕获每个实例的性能信息，包括提供的请求总数、吞吐量（以字节为单位）、失败的请求计数、正常和不正常的后端实例计数。
* **ApplicationGatewayFirewallLog**：防火墙日志包含通过应用程序网关（配置有 Web 应用程序防火墙）的检测或阻止模式记录的请求。

### <a name="how-do-i-know-if-my-backend-pool-members-are-healthy"></a>如何知道后端池成员是否正常？

可以使用 PowerShell cmdlet `Get-AzApplicationGatewayBackendHealth`，或者在门户中访问[应用程序网关诊断](application-gateway-diagnostics.md)来验证运行状况

### <a name="what-is-the-retention-policy-on-the-diagnostics-logs"></a>什么是诊断日志的保留策略？

诊断日志将发往客户存储帐户，客户可以根据偏好设置保留策略。 此外，可将诊断日志发送到事件中心或 Azure Monitor 日志。 有关详细信息，请参阅[应用程序网关诊断](application-gateway-diagnostics.md)。

### <a name="how-do-i-get-audit-logs-for-application-gateway"></a>如何获取应用程序网关的审核日志？

应用程序网关有相应的审核日志。 在门户中，单击**活动日志**应用程序网关，若要访问审核日志菜单边栏选项卡上。 

### <a name="can-i-set-alerts-with-application-gateway"></a>是否可以使用应用程序网关设置警报？

可以，应用程序网关支持警报。 警报是针对指标配置的。 若要了解有关应用程序网关指标的详细信息，请参阅[应用程序网关指标](https://docs.microsoft.com/azure/application-gateway/application-gateway-diagnostics#metrics)。 若要了解有关警报的详细信息，请参阅[接收警报通知](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)。

### <a name="how-do-i-analyze-traffic-statistics-for-application-gateway"></a>如何分析应用程序网关的流量统计信息？

可以通过几种机制（例如 Azure Monitor 日志、Excel、Power BI 等）查看和分析访问日志。

我们还发布了一个资源管理器模板，用于安装和运行应用程序网关访问日志的常用 [GoAccess](https://goaccess.io/) 日志分析器。 GoAccess 提供了宝贵的 HTTP 流量统计信息，例如唯一访问者、请求的文件、主机、操作系统、浏览器和 HTTP 状态代码等。 有关更多详细信息，请参阅 [GitHub 的资源管理器模板文件夹中的自述文件](https://aka.ms/appgwgoaccessreadme)。

### <a name="backend-health-returns-unknown-status-what-could-be-causing-this-status"></a>后端运行状况返回未知状态，什么原因导致此状态？

最常见原因是访问后端被 NSG，自定义 DNS 阻止或你在应用程序网关子网的 UDR。 有关详细信息，请参阅[应用程序网关的后端运行状况、诊断日志记录和指标](application-gateway-diagnostics.md)。

## <a name="next-steps"></a>后续步骤

若要了解有关应用程序网关的详细信息，请参阅[什么是 Azure 应用程序网关？](overview.md)
