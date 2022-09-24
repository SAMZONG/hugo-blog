# Tomcat 优化设定


- 设置JVM空间大小，Xms和Xmx一样大：JVM初始分配的内存由-Xms指定，默认是物理内存的1/64；JVM最大分配的内存由-Xmx指定，默认是物理内存的1/4。默认空余堆内存小于 40%时，JVM就会增大堆直到-Xmx的最大限制；空余堆内存大于70%时，JVM会减少堆直到-Xms的最小限制。因此服务器一般设置-Xms、 -Xmx相等以避免在每次GC 后调整堆的大小。
- 关闭dns查询
- 增加线程数量
- maxThreads、acceptCount ： 增加并发，同时增加这两个的数量
- 内存优化 ： /tomcatbin/catalina.sh

- JAVA_OPTS="-XX:PermSize=64M -XX:MaxPermSize=128m -Xms512m -Xmx1024m -Duser.timezone=Asia/Shanghai"
- 缓存优化
- 并发优化，线程优化
- <Connector port="80" protocol="HTTP/1.1" maxThreads="600" minSpareThreads="100" maxSpareThreads="500" acceptCount="700"
- connectionTimeout="20000" redirectPort="8443" />
- 关闭DNS查询 :修改server.xml文件中的Connector元素，修改属性enableLookups参数值: enableLookups="false"
- 使用apr插件，提高tomcat响应时间 <br>
```
  (1)安装APR tomcat-native
    apr-1.3.8.tar.gz   安装在/usr/local/apr
    #tar zxvf apr-1.3.8.tar.gz
    #cd apr-1.3.8
    #./configure;make;make install

    apr-util-1.3.9.tar.gz  安装在/usr/local/apr/lib
    #tar zxvf apr-util-1.3.9.tar.gz
    #cd apr-util-1.3.9
    #./configure --with-apr=/usr/local/apr ----with-java-home=JDK;make;make install

    #cd apache-tomcat-6.0.20/bin
    #tar zxvf tomcat-native.tar.gz
    #cd tomcat-native/jni/native
    #./configure --with-apr=/usr/local/apr;make;make install

  (2)设置 Tomcat 整合 APR
    修改 tomcat 的启动 shell （startup.sh），在该文件中加入启动参数：
      CATALINA_OPTS="$CATALINA_OPTS -Djava.library.path=/usr/local/apr/lib" 。

  (3)判断安装成功:
    如果看到下面的启动日志，表示成功。
      2007-4-26 15:34:32 org.apache.coyote.http11.Http11AprProtocol init
```
- 开启manager 管理
- 使用http://visualvm.Java.net/download.html 工具监控tomcat的性能
- JAVA_OPTS='-Dcom.sun.management.jmxremote.port=8999 -Dcom.sun.management.jmxremote.ssl=false -Dcom.sun.management.jmxremote.authenticate=false'
- 设置自动更新autodeploy＝false

