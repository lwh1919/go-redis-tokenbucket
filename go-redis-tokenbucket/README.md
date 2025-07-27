# go-redis-tokenbucket

基于Redis和Lua脚本实现的分布式令牌桶限流库，支持高并发场景下的流量控制。

## 功能特点
- 分布式限流：基于Redis实现，支持多服务实例共享限流状态
- 令牌桶算法：平滑流量控制，支持突发流量处理
- 原子操作：使用Lua脚本保证限流操作的原子性
- 并发安全：支持多协程并发请求

## 使用方法
```go
// 初始化限流器（令牌桶容量90，每秒生成30个令牌）
limiter := NewTokenBucketLimiter(redisClient, 90, 30, time.Minute)

// 检查是否允许请求
allowed, err := limiter.Allow(ctx, "user123")
if allowed {
    // 处理请求
} else {
    // 请求被限流
}
```

## 安装依赖
```bash
go get github.com/go-redis/redis/v9
```

## 测试
```bash
go test -v
```
[参考连接](https://www.liwenzhou.com/posts/Go/go-redis-lua/)

## 项目架构


├── scripts/                  # Lua脚本目录
│   └── token_bucket.lua      # Redis Lua脚本
├── go.mod                    # Go模块定义文件
├── go.sum                    # Go模块依赖校验文件
├── ratelimit.go              # 令牌桶限流器主实现
├── ratelimit_test.go         # 测试代码
└── README.md                 # 项目文档