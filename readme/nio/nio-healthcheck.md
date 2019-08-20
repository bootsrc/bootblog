客户端健康检查(心跳检测)的实现

```java
ScheduledExecutorService scheduledExecutor = Executors.newSingleThreadScheduledExecutor();

=> scheduledExecutor赋值到下面的字断

private final ScheduledExecutorService scheduledExecutor;

scheduledExecutor.scheduleAtFixedRate(new Runnable() {
    @Override
    public void run() {
        client.healthCheck();
    }
}, 10, 10, TimeUnit.SECONDS);


```
healthCheck()如下

```java
@Override
public boolean healthCheck() {

    if (connection.isReadTimeout()) {
        hbTimeoutTimes++;
        logger.w("heartbeat timeout times=%s", hbTimeoutTimes);
    } else {
        hbTimeoutTimes = 0;
    }

    if (hbTimeoutTimes >= MAX_HB_TIMEOUT_COUNT) {
        logger.w("heartbeat timeout times=%d over limit=%d, client restart", hbTimeoutTimes, MAX_HB_TIMEOUT_COUNT);
        hbTimeoutTimes = 0;
        connection.reconnect();
        return false;
    }

    if (connection.isWriteTimeout()) {
        logger.d("<<< send heartbeat ping...");
        connection.send(Packet.HB_PACKET);
    }

    return true;
}
```