
# Debug与Release模式
```
#if DEBUG
          <debug code>;
#else
          <release code>;
#endif
```
以此处设置为Debug或Release为准
![[CSharp_Debug与Release模式.png]]
# override 与new
override是用来重写父类虚方法，对基类方法的引用也会被覆盖
new 是将子类方法代替父类方法，对基类的引用不会被覆盖。
```c#
 class Program
 {
 	static void Main(string[] args)
 	{
 		Base b1 = new DerivedOverride();

 		b1.DoIt();//call DerivedOverride.DoIt(); print "Derived"

 		Base b2 = new DerivedNew();

 		b2.DoIt();//call Base.DoIt; print nothing because virtual	

 		DerivedNew b3 = new DerivedNew();

 		b3.DoIt();//call DerivedNew.DoIt(); print "Derived2"
 	}
 }
class Base
{
      public virtual void DoIt() { }
}

class DerivedOverride : Base
{
      public override void DoIt()
      {
           base.DoIt();
           System.Console.WriteLine("Derived");
      }
}

class DerivedNew : Base
{
      public new void DoIt()
      {
          System.Console.WriteLine("Derived2");
      }
}
```
# C#中的log4net插件
## 配置文件说明
```xml
 <?xml version="1.0" encoding="utf-8"?>
<log4net>
	<!-- 控制台日志配置 -->
	<appender name="Console" type="log4net.Appender.ConsoleAppender">
		<!-- 日志输出格式 -->
		<layout type="log4net.Layout.PatternLayout">
			<conversionPattern value="[%thread]#:%logger %-5level:  %message%newline" />
		</layout>
	</appender>

	<!-- 文件存储日志配置 -->
	<appender name="RollingFile" type="log4net.Appender.RollingFileAppender">
		<!-- <lockingModel type="log4net.Appender.FileAppender+MinimalLock"/> -->
		<!-- 保存文件的名称  路径在bin文件夹下-->
		<file value="logs\" />
		<!-- 是否追加到文件 -->
		<appendToFile value="true" />
		<!-- 文件的编码方式 -->
		<encoding value="UTF-8" />
		<!-- <param name="Encoding" value="UTF-8"/> -->
		<!--按照何种方式产生多个日志文件(日期[Date],文件大小[Size],混合[Composite])-->
		<RollingStyle value="Composite" />
		<!-- <param name="RollingStyle" value="Composite" /> -->
		<!--按日期产生文件夹和文件名［在日期方式与混合方式下使用］-->
		<!--此处按日期产生文件夹，文件名固定。注意&quot; 的位置-->
		<!-- <param name="DatePattern" value="yyyy-MM-dd/&quot;ReflectionLayout.log&quot;"  /> -->
		<!--这是按日期产生文件夹，并在文件名前也加上日期-->
		<!--<param name="DatePattern" value="yyyyMMdd/yyyyMMdd&quot;-TimerServer.log&quot;"  />-->
		<!--这是先按日期产生文件夹，再形成下一级固定的文件夹-->
		<!-- <param name="DatePattern" value="yyyyMMdd/&quot;TimerServer/TimerServer.log&quot;"  /> -->
		<DatePattern value="yyyyMMdd/&quot;Log.log&quot;" />
		<!-- <DatePattern value="dd.MM.yyyy'.log'" /> -->
		<!-- 注意若设置文件名更改则此字段需改为false -->
  		<StaticLogFileName value="false" />
		<!-- 每个文件的大小:只在混合方式与文件大小方式下使用。超出大小后在所有文件名后自动增加正整数重新命名，数字最大的最早写入。可用的单位:KB|MB|GB。不要使用小数,否则会一直写入当前日志 -->
		<maximumFileSize value="1KB" />
		<!--最多产生的日志文件数，超过则只保留最新的n个。设定值value="－1"为不限文件数-->
		<maxSizeRollBackups value="2" />
		<!-- 日志输出格式 -->
		<layout type="log4net.Layout.PatternLayout,log4net">
			<!-- 记录时间：%date 线程ID:[%thread] 日志级别：%-5level 记录类：%logger     
				操作者ID：%property{Operator} 操作类型：%property{Action}%n             
				当前机器名:%property%n当前机器名及登录用户：%username %n               
				记录位置：%location%n 消息描述：%property{Message}%n                    
				异常：%exception%n 消息：%message%newline%n%n -->
			<conversionPattern value="%thread[%date] [%logger]#:%-5level:  %message%newline" />
		</layout>
		<!--过滤设置，LevelRangeFilter为使用的过滤器-->
		<filter type="log4net.Filter.LevelRangeFilter">
			<!-- 过滤起始等级（不包含） -->
			<param name="LevelMin" value="DEBUG" />
			<!-- 过滤终止等级（包含） -->
			<param name="LevelMax" value="WARN" />
		</filter>
	</appender>

	<root>
	<!-- 控制级别,由低到高:ALL|DEBUG|INFO|WARN|ERROR|FATAL|OFF -->
		<level value="INFO" />
		<appender-ref ref="Console" />
		<appender-ref ref="RollingFile" />
	</root>
	<logger name="HttpUtillib">
		<level value="OFF" />
		<appender-ref ref="Console" />
	</logger>
</log4net>
```

Appenders用来定义日志的输出方式，即日志要写到那种介质上去。较常用的Log4net已经实现好了，直接在配置文件中调用即可，可参见上面配置文件例子；当然也可以自己写一个，需要从log4net.Appender.AppenderSkeleton类继承。它还可以通过配置Filters和Layout来实现日志的过滤和输出格式。
已经实现的输出方式有：
- AdoNetAppender 将日志记录到数据库中。可以采用SQL和存储过程两种方式。
- AnsiColorTerminalAppender 将日志高亮输出到ANSI终端。
- AspNetTraceAppender  能用asp.net中Trace的方式查看记录的日志。
- BufferingForwardingAppender 在输出到子Appenders之前先缓存日志事件。
- ConsoleAppender 将日志输出到应用程序控制台。
- EventLogAppender 将日志写到Windows Event Log。
- FileAppender 将日志输出到文件。
- ForwardingAppender 发送日志事件到子Appenders。
- LocalSyslogAppender 将日志写到local syslog service (仅用于UNIX环境下)。
- MemoryAppender 将日志存到内存缓冲区。
- NetSendAppender 将日志输出到Windows Messenger service.这些日志信息将在用户终端的对话框中显示。
- OutputDebugStringAppender 将日志输出到Debuger，如果程序没有Debuger，就输出到系统Debuger。如果系统Debuger也不可用，将忽略消息。
- RemoteSyslogAppender 通过UDP网络协议将日志写到Remote syslog service。
- RemotingAppender 通过.NET Remoting将日志写到远程接收端。
- RollingFileAppender 将日志以回滚文件的形式写到文件中。
- SmtpAppender 将日志写到邮件中。
- SmtpPickupDirAppender 将消息以文件的方式放入一个目录中，像IIS SMTP agent这样的SMTP代理就可以阅读或发送它们。
- TelnetAppender 客户端通过Telnet来接受日志事件。
- TraceAppender 将日志写到.NET trace 系统。
- UdpAppender 将日志以无连接UDP数据报的形式送到远程宿主或用UdpClient的形式广播。