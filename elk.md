# ELK 日志收集系统

## Create elk user

```bash
useradd -m -s /bin/bash elk
```

## Elasticsearch

```bash
bin/elasticsearch -d
```

```bash
curl 127.0.0.1:9200
```

## Kibana

```bash
bin/kibana \
    1>log 2>&1 &
```

```bash
ssh -L 5601:127.0.0.1:5601 -N -T SSH_USERNAME@YOUR_SERVER_IP
```

## Logstash

```bash
vim logstash.conf
```

```text
input {
    tcp {
        mode => "server"
        host => "0.0.0.0"
        port => 4560
        codec => json_lines
    }
}

output {
    elasticsearch {
        hosts => "127.0.0.1:9200"
        index => "springboot-logstash-%{+YYYY.MM.dd}"
    }
}
```

```bash
bin/logstash -f logstash.conf \
    1>log 2>&1 &
```

```bash
ssh -L 4560:127.0.0.1:4560 -N -T SSH_USERNAME@YOUR_SERVER_IP
```

## Spring Boot

### POM

https://github.com/logstash/logstash-logback-encoder

```xml
<dependency>
    <groupId>net.logstash.logback</groupId>
    <artifactId>logstash-logback-encoder</artifactId>
    <version>6.6</version>
</dependency>
```

### application.properties

```text
spring.application.name=YOUR_APPLICATION_NAME
logstash.address=YOUR_SERVER_IP:4560
```

### logback-spring.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration debug="false">
    <!-- app name -->
    <springProperty scope="context" name="APPLICATION_NAME" source="spring.application.name"/>

    <!-- logstash 地址 -->
    <springProperty scope="context" name="LOGSTASH_ADDRESS" source="logstash.address"/>

    <!-- 日志文件的存储地址 -->
    <property name="LOG_HOME" value="log"/>

    <!-- 控制台输出 -->
    <appender name="STDOUT" class="ch.qos.logback.core.ConsoleAppender">
        <encoder class="ch.qos.logback.classic.encoder.PatternLayoutEncoder">
            <!-- 格式化输出：%d 表示日期，%thread 表示线程名，%-5level 表示从左显示 5 个字符宽度的日志级别，%msg 表示日志消息，%n 表示换行符 -->
            <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} [%thread] %highlight(%-5level) %cyan(%logger{50}:%L) - %msg%n</pattern>
        </encoder>
    </appender>

    <!-- logstash 输出 -->
    <appender name="LOGSTASH" class="net.logstash.logback.appender.LogstashTcpSocketAppender">
        <destination>${LOGSTASH_ADDRESS}</destination>
        <encoder class="net.logstash.logback.encoder.LoggingEventCompositeJsonEncoder">
            <providers>
                <timestamp>
                    <timeZone>UTC</timeZone>
                </timestamp>
                <pattern>
                    <pattern>
                        {
                        "app": "${APPLICATION_NAME}",
                        "thread": "%thread",
                        "level": "%-5level",
                        "logger": "%logger{50} %M %L",
                        "message": "%msg"
                        }
                    </pattern>
                </pattern>
            </providers>
        </encoder>
    </appender>

    <!-- 每天生成日志文件 -->
    <appender name="ROLLING" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <rollingPolicy class="ch.qos.logback.core.rolling.SizeAndTimeBasedRollingPolicy">
            <!-- 日志文件输出的文件名 -->
            <FileNamePattern>${LOG_HOME}/%d{yyyy-MM-dd}.%i.log</FileNamePattern>
            <!-- 日志文件保留天数 -->
            <MaxHistory>30</MaxHistory>
            <maxFileSize>10MB</maxFileSize>
        </rollingPolicy>
        <encoder class="ch.qos.logback.classic.encoder.PatternLayoutEncoder">
            <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} [%thread] %-5level %logger{50}:%L - %msg%n</pattern>
        </encoder>
    </appender>

    <!-- 生成 error html 日志文件 -->
    <appender name="HTML_ERROR" class="ch.qos.logback.core.FileAppender">
        <filter class="ch.qos.logback.classic.filter.ThresholdFilter">
            <!-- 设置日志级别，过滤掉 info 日志，只输出 error 日志-->
            <level>ERROR</level>
        </filter>
        <encoder class="ch.qos.logback.core.encoder.LayoutWrappingEncoder">
            <layout class="ch.qos.logback.classic.html.HTMLLayout">
                <pattern>%p%d%msg%M%F{32}%L</pattern>
            </layout>
        </encoder>
        <file>${LOG_HOME}/error-log.html</file>
    </appender>

    <!-- 每天生成 html 日志文件 -->
    <appender name="HTML_ROLLING" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <rollingPolicy class="ch.qos.logback.core.rolling.SizeAndTimeBasedRollingPolicy">
            <!-- 日志文件输出的文件名 -->
            <FileNamePattern>${LOG_HOME}/%d{yyyy-MM-dd}.%i.html</FileNamePattern>
            <!-- 日志文件保留天数 -->
            <MaxHistory>30</MaxHistory>
            <MaxFileSize>10MB</MaxFileSize>
        </rollingPolicy>
        <encoder class="ch.qos.logback.core.encoder.LayoutWrappingEncoder">
            <layout class="ch.qos.logback.classic.html.HTMLLayout">
                <pattern>%p%d%msg%M%F{32}%L</pattern>
            </layout>
        </encoder>
    </appender>

    <!-- mybatis log config -->
    <logger name="com.apache.ibatis" level="TRACE"/>
    <logger name="java.sql.Connection" level="DEBUG"/>
    <logger name="java.sql.Statement" level="DEBUG"/>
    <logger name="java.sql.PreparedStatement" level="DEBUG"/>

    <!-- 日志输出级别 -->
    <root level="INFO">
        <appender-ref ref="STDOUT"/>
        <appender-ref ref="LOGSTASH"/>
        <appender-ref ref="ROLLING"/>
        <appender-ref ref="HTML_ERROR"/>
        <appender-ref ref="HTML_ROLLING"/>
    </root>

</configuration>
```
