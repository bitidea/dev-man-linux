# JAR Restart

## `run.sh`

```bash
#!/usr/bin/env bash
BASE_PATH="YOUR_BASE_PATH"
JAR_FILENAME=$1
LOG_FILENAME="$JAR_FILENAME.$(date +%s).log"
JAR_PATH="$BASE_PATH/$JAR_FILENAME"
LOG_PATH="$BASE_PATH/$LOG_FILENAME"
CMD="java -jar $JAR_PATH"
KILL_CMD="ps aux | grep '$CMD' | grep -v grep | awk '{print \$2}' | xargs kill -9"
bash -c "$KILL_CMD"
bash -c "$CMD 1>$LOG_PATH 2>&1 &"
```

## Usage

```bash
bash -x run.sh YOUR_JAR.jar
```
