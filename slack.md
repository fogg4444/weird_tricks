# Slack Tricks
---

### Shell script integration


```
name_of_script.sh "Call with this argument"
```

```
TEXT="Message: "$1

SLACK_URL="https://hooks.slack.com/services/yourDataHere/yourDataHere"

curl -X POST --data-urlencode "payload={\"text\": \"$TEXT\", \"icon_emoji\": \":ghost:\"}" $SLACK_URL
```
---
