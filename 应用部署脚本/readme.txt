## nohup java -jar jodconverter-web-1.5.8.RELEASE.war >fileOnlineLog.txt &  

分别启动：
startFileOnlineServer.bat
startEurekaServer.bat
startAdminServer.bat
startZuulServer.bat

#多媒体资源在线预览服务
java -jar jodconverter-web-1.5.8.RELEASE.war

#启动注册中心
java -jar mycloud-eureka-1.0.0.war

#启动后台服务
java -jar mycloud-admin.war

#启动网关
java -jar mycloud-zuul-1.0.0.war