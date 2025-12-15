# 青锋 (QingFeng)

�️ 一个观美观、强大的 Swagger UI 替代方案，专为 Go Gin 框架设计。

> 青出于蓝，锋芒毕露 —— 为 Go 开发者提供更好的 API 文档体验。

## ✨ 特性

- 🎨 **美观的界面** - 现代化 UI 设计，支持深色/浅色主题
- 🔍 **快速搜索** - 实时搜索接口，快速定位
- 🐛 **在线调试** - 内置 API 调试工具，类似 Postman
- 📦 **零依赖前端** - 使用 embed.FS 内嵌，无需额外部署
- 🚀 **简单集成** - 一行代码接入现有项目
- 📱 **响应式设计** - 支持移动端访问

## 📦 安装

```bash
go get github.com/delfDog/QingFeng
```

## 🚀 快速开始

```go
package main

import (
    "github.com/gin-gonic/gin"
    qingfeng "github.com/delfDog/QingFeng"
)

func main() {
    r := gin.Default()

    // 注册青锋文档 UI
    r.GET("/doc/*any", qingfeng.Handler(qingfeng.Config{
        Title:       "我的 API",
        Description: "API 文档描述",
        Version:     "1.0.0",
        BasePath:    "/doc",
        DocPath:     "./docs/swagger.json", // swag init 生成的文件
        EnableDebug: true,
        DarkMode:    false,
    }))

    // 你的业务路由...
    r.GET("/api/users", getUsers)

    r.Run(":8080")
}
```

访问 `http://localhost:8080/doc/` 查看文档。

## ⚙️ 配置项

| 参数 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| Title | string | "API Documentation" | 文档标题 |
| Description | string | "" | 文档描述 |
| Version | string | "1.0.0" | API 版本 |
| BasePath | string | "/doc" | 文档路由前缀 |
| DocPath | string | "./docs/swagger.json" | swagger.json 文件路径 |
| DocJSON | []byte | nil | 直接传入 swagger JSON 内容 |
| EnableDebug | bool | true | 是否启用在线调试 |
| DarkMode | bool | false | 是否默认深色模式 |

## 🔧 与 swag 配合使用

1. 安装 swag:
```bash
go install github.com/swaggo/swag/cmd/swag@latest
```

2. 在代码中添加注释:
```go
// @Summary 获取用户列表
// @Description 分页获取用户
// @Tags 用户管理
// @Accept json
// @Produce json
// @Param page query int false "页码"
// @Success 200 {object} Response
// @Router /users [get]
func getUsers(c *gin.Context) {
    // ...
}
```

3. 生成文档:
```bash
swag init
```

4. 集成青锋 (见快速开始)

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

## 📄 License

MIT License
