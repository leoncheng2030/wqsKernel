# WQS (Web Quick Start) - 微内核架构框架

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Java](https://img.shields.io/badge/Java-17+-orange.svg)](https://www.oracle.com/java/)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.2+-green.svg)](https://spring.io/projects/spring-boot)
[![Version](https://img.shields.io/badge/version-1.0.0-brightgreen.svg)](https://github.com/wqs-project/wqs)

WQS是一个基于微内核架构的企业级开发框架，采用Java 17和Spring Boot 3.2+构建，提供热插拔插件系统、事件驱动通信和扩展点机制，旨在为企业应用开发提供灵活、可扩展的解决方案。

## ✨ 核心特性

### 🏗️ 微内核架构
- **插件化设计**: 基于微内核架构，核心功能最小化，业务功能插件化
- **热插拔支持**: 支持运行时动态加载、卸载和更新插件
- **松耦合设计**: 插件间通过接口和事件进行通信，降低耦合度

### 🔌 插件系统
- **生命周期管理**: 完整的插件生命周期管理（发现、加载、启动、停止、卸载）
- **依赖管理**: 智能的插件依赖解析和加载顺序管理
- **健康监控**: 实时插件健康状态监控和故障恢复

### 🌟 扩展机制
- **扩展点框架**: 灵活的扩展点定义和实现机制
- **服务注册**: 分布式服务注册与发现
- **事件总线**: 高性能事件发布订阅机制

### 🛡️ 企业级特性
- **安全框架**: 集成Spring Security，支持JWT认证
- **监控体系**: 完整的应用和插件监控方案
- **测试框架**: 专门的插件测试框架和工具

## 🏛️ 架构设计

```
┌─────────────────────────────────────────────────────────────┐
│                    WQS Web Application                     │
├─────────────────────────────────────────────────────────────┤
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────────────┐  │
│  │ Auth Plugin │  │ Sys Plugin  │  │   Custom Plugins    │  │
│  └─────────────┘  └─────────────┘  └─────────────────────┘  │
├─────────────────────────────────────────────────────────────┤
│                    Plugin APIs & SPIs                      │
├─────────────────────────────────────────────────────────────┤
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────────────┐  │
│  │   Starters  │  │  Framework  │  │       Kernel        │  │
│  │             │  │             │  │                     │  │
│  │ - Web       │  │ - Security  │  │ - Plugin Manager    │  │
│  │ - Data      │  │ - Cache     │  │ - Event Bus         │  │
│  │ - Security  │  │ - Response  │  │ - Extension Points  │  │
│  │ - Cache     │  │ - Exception │  │ - Service Registry  │  │
│  └─────────────┘  └─────────────┘  └─────────────────────┘  │
├─────────────────────────────────────────────────────────────┤
│                   Spring Boot 3.2+                         │
└─────────────────────────────────────────────────────────────┘
```

## 🚀 快速开始

### 环境要求

- **Java 17+**
- **Maven 3.8+**
- **MySQL 8.0+**
- **Redis 6.0+** (可选)

### 1. 克隆项目

```bash
git clone https://github.com/wqs-project/wqs.git
cd wqs
```

### 2. 数据库配置

创建MySQL数据库：
```sql
CREATE DATABASE wqs CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

导入数据库脚本：
```bash
mysql -u root -p wqs < docs/sql/wqs_schema.sql
```

### 3. 配置文件

修改 `wqs-web-app/src/main/resources/application.yml`：

```yaml
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/wqs
    username: your_username
    password: your_password
```

### 4. 构建和运行

```bash
# 构建项目
mvn clean install

# 启动应用
cd wqs-web-app
mvn spring-boot:run
```

### 5. 访问应用

- **应用地址**: http://localhost:8080
- **管理端点**: http://localhost:8080/actuator
- **健康检查**: http://localhost:8080/actuator/health

## 📁 项目结构

```
wqs/
├── wqs-kernel/                 # 微内核核心
│   ├── core/                   # 内核核心组件
│   ├── plugin/                 # 插件管理器
│   ├── event/                  # 事件总线
│   ├── extension/              # 扩展点框架
│   └── service/                # 服务注册中心
├── wqs-framework/              # 框架基础设施
│   ├── config/                 # 配置管理
│   ├── security/               # 安全框架
│   ├── web/                    # Web框架
│   ├── cache/                  # 缓存抽象
│   ├── response/               # 响应封装
│   ├── exception/              # 异常处理
│   └── monitoring/             # 监控体系
├── wqs-plugin-apis/            # 插件API定义
│   ├── core/                   # 核心接口
│   ├── extension/              # 扩展接口
│   └── event/                  # 事件接口
├── wqs-starters/               # 自动配置启动器
│   ├── wqs-starter-web/        # Web启动器
│   ├── wqs-starter-data/       # 数据启动器
│   ├── wqs-starter-security/   # 安全启动器
│   ├── wqs-starter-cache/      # 缓存启动器
│   └── wqs-starter-plugin/     # 插件启动器
├── wqs-plugins/                # 内置插件
│   ├── wqs-plugin-sys/         # 系统管理插件
│   └── wqs-plugin-auth/        # 认证授权插件
├── wqs-web-app/                # Web应用主程序
├── wqs-admin-web/              # 管理后台前端
├── wqs-examples/               # 示例和文档
│   ├── wqs-example-plugin/     # 示例插件
│   └── docs/                   # 开发文档
└── docs/                       # 项目文档
```

## 🔌 插件开发

### 创建插件

1. **实现插件接口**：

```java
@Component
public class MyPlugin implements WqsPlugin {
    
    @Override
    public String getPluginId() {
        return "my-plugin";
    }
    
    @Override
    public void start(PluginContext context) throws PluginException {
        // 插件启动逻辑
    }
    
    @Override
    public void stop() throws PluginException {
        // 插件停止逻辑
    }
}
```

2. **定义扩展点**：

```java
@ExtensionPoint("data-processor")
public interface DataProcessor {
    String process(String data);
}
```

3. **实现扩展**：

```java
@Extension("data-processor")
@Component
public class JsonDataProcessor implements DataProcessor {
    @Override
    public String process(String data) {
        // 处理逻辑
        return processedData;
    }
}
```

### 插件配置

在 `application.yml` 中配置插件：

```yaml
wqs:
  plugin:
    enabled: true
    hot-swap: true
    scan-packages:
      - com.example.plugins
    load-timeout: 30000
```

## 🛠️ 开发指南

### API开发

使用统一响应格式：

```java
@RestController
public class UserController {
    
    @GetMapping("/users/{id}")
    public WqsResponse<User> getUser(@PathVariable Long id) {
        User user = userService.findById(id);
        return WqsResponse.success(user);
    }
}
```

### 异常处理

使用业务异常：

```java
if (user == null) {
    throw WqsBusinessException.notFound("用户不存在");
}
```

### 缓存使用

```java
@Cacheable(value = "users", key = "#id")
public User findById(Long id) {
    return userRepository.findById(id);
}
```

## 📊 监控和运维

### 健康检查

```bash
curl http://localhost:8080/actuator/health
```

### 指标监控

```bash
curl http://localhost:8080/actuator/metrics
```

### 插件管理

```bash
# 查看所有插件
GET /api/plugins

# 停止插件
POST /api/plugins/{pluginId}/stop

# 启动插件
POST /api/plugins/{pluginId}/start
```

## 🧪 测试

### 运行测试

```bash
# 运行所有测试
mvn test

# 运行集成测试
mvn integration-test

# 生成测试报告
mvn site
```

### 插件测试

使用WQS测试框架：

```java
@WqsTestFramework(plugins = {MyPlugin.class})
class MyPluginTest {
    
    @Test
    void testPluginFunctionality() {
        // 测试逻辑
    }
}
```

## 🔧 配置参考

### 核心配置

```yaml
wqs:
  enabled: true
  version: 1.0.0
  
  # 内核配置
  kernel:
    enabled: true
    
  # 插件配置
  plugin:
    enabled: true
    hot-swap: true
    scan-packages: []
    load-timeout: 30000
    
  # Web配置
  web:
    enabled: true
    cors:
      enabled: true
      allowed-origins: "*"
      
  # 安全配置
  security:
    enabled: true
    jwt:
      secret: your-secret-key
      expiration: 3600000
      
  # 监控配置
  monitoring:
    enabled: true
```

## 📚 文档

- [架构设计](docs/architecture.md)
- [插件开发指南](docs/plugin-development.md)
- [API文档](docs/api-reference.md)
- [部署指南](docs/deployment.md)
- [最佳实践](docs/best-practices.md)
- [常见问题](docs/faq.md)

## 🤝 贡献

我们欢迎任何形式的贡献！

1. Fork 项目
2. 创建功能分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 创建 Pull Request

请阅读 [CONTRIBUTING.md](CONTRIBUTING.md) 了解详细的贡献指南。

## 📄 许可证

本项目采用 MIT 许可证 - 查看 [LICENSE](LICENSE) 文件了解详情。

## 🙏 致谢

- [Spring Boot](https://spring.io/projects/spring-boot) - 应用框架
- [Spring Security](https://spring.io/projects/spring-security) - 安全框架
- [MyBatis Plus](https://baomidou.com/) - 数据访问框架
- [Element Plus](https://element-plus.org/) - UI组件库

## 📞 联系我们

- **项目主页**: https://github.com/wqs-project/wqs
- **文档网站**: https://wqs-project.github.io/docs
- **问题反馈**: https://github.com/wqs-project/wqs/issues

---

**WQS** - 让企业应用开发更简单、更灵活！ 
