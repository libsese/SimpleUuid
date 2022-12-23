# Simple Uuid

### uuid::TimestampHandler

| 函数名称                   | 返回值    | 能否处理时钟回拨 |
|------------------------|--------|----------|
| getCurrentTimestamp    | 毫秒级时间戳 | 否        |
| tryGetCurrentTimestamp | 毫秒级时间戳 | 是        |

tryGetCurrentTimestamp 几种返回值的含义

- 0 —— 发生时间回拨且回拨时间不超过 **五秒**；
- UINT64_MAX —— 发生时间回拨且回拨时间超过 **五秒**；
- 其它 —— 时间戳正常

### uuid::Uuid 内存布局

```
---------------------------------------------
| selfId(8) |   r(8)    |   timestamp(48)   |
---------------------------------------------
```

| 字段        | 位数  | 说明          |
|-----------|-----|-------------|
| selfId    | 8   | 一般用于表示机器 ID |
| r         | 8   | 保留位，可自定义    |
| timestamp | 48  | 毫秒级时间戳      |

timestamp 在毫秒级别下能表示约 8925.513 年