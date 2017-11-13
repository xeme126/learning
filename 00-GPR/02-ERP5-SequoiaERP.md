

Sequoia ERP是一个真正的企业级开源 ERP 解决方案。 Sequoia ERP 采用 Java 开发可部署在 Linux/Unix 与 Windows 平台上 , 并支持当前主流数据库如： MySQL, PostgreSQL, Orace, Microsoft SQL Server 等关系型数据库。

Sequoia ERP 的模块包

•  电子商务应用 (e-commerce)

•  POS 系统 (point of sales)

•  知识管理

•  存货与仓库管理

•  客户服务 ( customer service)

缺点

Sequoia ERP 的缺点是前后台都没有中文，在汉化的过程中带来了一定困难，即使装了汉化了。也是非常的不完全。这个企业的管理上带来了一定的困难，在后台的演示模块中， 没有人力资源这一模块，不是自带的必须的安装插件。

点评

Sequoia ERP 的前生是 opentaps, 其开发者是 ofbiz 项目中的一位 Si Chen ，财务出身在 ofbiz 中的任务主要是改造 ofbiz 的财务模块。对 ofbiz 中的一些业务模块进行了整合并加入了自己开发的 CRM 和财务模块。 ofbiz 作为以上两个 ERP 系统的应用框架，与其它的企业应用框架不同的是安装后即提供了许多可用的业务模块，但是要真正投入应用还是要做大量的定制工作。 ofbiz 的其中一个核心就是其实体引擎（ Entity engine), 就是 ofbiz 的数据持久层。它的作用大致与 Compiere/Adempiere 的 AD ， Tiny ERP 的 ORM 是类似的。但是也有人觉得 ofbiz 应该采用一个更加成熟，灵活的基于 java 的数据持久项目 hibernate. 另外， ofbiz2.0 后又引入了服务框架（ Service Framwork) ，这个应该就是现在被热炒的 SOA 。 ofbiz 的野心太大了它几乎想在这个框架下包罗万象，工作流引擎，规则引擎，消息引擎 … 它无疑是一个非常强大的 WEB 应用框架，但是正因为它无所不包的特点造成系统日益庞大，沉重，复杂，同时也限制了灵活性。所以很多人都在讨论 ofbiz 的简化，轻量级应用。

PS：Sequoia ERP的后台是基于ofbiz的，它也是属于一款ERP软件并自带CRM功能，在后台中有一款独立的SFA（销售自动化）模块。