# nohup

```bash
#!/bin/bash
ps aux | grep java | grep -v grep | awk '{print $2}'| xargs kill -9
rm -rf log
nohup java -jar YOUR_JAR_NAME.jar > log 2>&1 &
tail -f log
```
