# JAR Restart

## `run.sh`

```bash
#!/usr/bin/env bash
BASE_PATH="YOUR_BASE_PATH"
echo $BASE_PATH

JAR_FILENAME=$1
echo $JAR_FILENAME

LOG_FILENAME="$JAR_FILENAME.log"
echo $LOG_FILENAME

JAR_PATH="$BASE_PATH/$JAR_FILENAME"
echo $JAR_PATH

LOG_PATH="$BASE_PATH/$LOG_FILENAME"
echo $LOG_PATH

CMD="java -jar $JAR_PATH"
echo $CMD

KILL_CMD="ps aux | grep '$CMD' | grep -v grep | awk '{print \$2}' | xargs kill -9"
echo $KILL_CMD

bash -c "$KILL_CMD"

bash -c "$CMD 1>$LOG_PATH 2>&1 &"
```

## Usage

```bash
bash run.sh YOUR_JAR.jar
```
