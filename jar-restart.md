# Jar Restart

```bash
#!/bin/bash
JAR='YOUR_JAR.jar'
CMD="java -jar $JAR"
ps aux | grep $CMD | grep -v grep | awk '{print $2}'| xargs kill -9
rm -rf log
java -jar YOUR_JAR.jar 1>log 2>&1 &
tail -f log
```
