1..net core publish 之后找不到视图文件的问题
问题很是蛋疼，后来仔细想了一下，也没有动什么东西。查看了SKD 还是 2.0.0的，publish 的时候我用的是命令行，和VS没有关系。于是也没有仔细排查啊问题的根源，今天查看*.csproj文件发现了问题的根源：

 <PropertyGroup>
    <TargetFramework>netcoreapp2.0</TargetFramework>
    <MvcRazorCompileOnPublish>True</MvcRazorCompileOnPublish>
    <TypeScriptToolsVersion>2.5</TypeScriptToolsVersion>   
  </PropertyGroup>
原来这里不知道什么时候将<MvcRazorCompileOnPublish>True</MvcRazorCompileOnPublish> 设置为true了，于是手动改false。熟悉的视图文件又在项目的发布文件夹中出现了。
原文链接：https://blog.csdn.net/mingminglv1/article/details/81181790

2.
a.部署iis前需要安装DotNetCore.2.0.8-WindowsHosting.exe，在iis中模块中就会出现AspNetCoreModule,因为iis接收到请求会将请回转发给AspNetCoreModule，iis只会起到了反向代理的作用。
跟以前asp.net web不同，以前是iis 进程wswp.exe直接处理请求的。
b.部署asp.net core的应用程序池.NET CLR使用的是无托管代码。

3.ASP.NET Core WEB部署有3中方式：IIS、Kestrel、Docker
	a.Kestrel web部署：ASP.NET Core中内置了一个WEB服务器Kestrel，能够快速简单的部署WEB网站。
	Windows系统和Linux(CentOS)中都可以使用此方式，前提要先安装.net core运行环境。
	使用CMD命令行进入到网站发布目录，然后通过.net core运行时来启动网站
	dotnet MyCMS.Web.dll
	使用的端口配置在host.json文件中


