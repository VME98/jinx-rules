# Jinx 远程规则仓库模板

这是 Jinx DNS 过滤器的远程规则仓库模板。

## 目录结构

```
rules/
├── version.json           # 版本信息
├── blacklist.txt          # 黑名单域名（精确匹配，每行一个）
├── blacklist_wildcard.txt # 黑名单通配符规则
├── whitelist.txt          # 白名单域名（精确匹配）
└── whitelist_wildcard.txt # 白名单通配符规则
```

## 使用方法

### 1. 创建 GitHub 仓库

1. 在 GitHub 创建一个新的公开仓库，例如 `jinx-rules`
2. 将 `rules/` 目录上传到仓库

### 2. 配置 jsDelivr CDN

jsDelivr 会自动为 GitHub 仓库提供 CDN 加速。URL 格式：

```
https://cdn.jsdelivr.net/gh/用户名/仓库名@分支/路径
```

例如：
- 版本信息：`https://cdn.jsdelivr.net/gh/yourname/jinx-rules@main/rules/version.json`
- 黑名单：`https://cdn.jsdelivr.net/gh/yourname/jinx-rules@main/rules/blacklist.txt`

### 3. 修改 App 配置

在 `RemoteRuleManager.swift` 中修改 `baseURL`：

```swift
private let baseURL = "https://cdn.jsdelivr.net/gh/你的用户名/jinx-rules@main/rules"
```

## 规则格式

### blacklist.txt / whitelist.txt

每行一个域名，支持注释：

```
# 这是注释
ad.example.com
tracker.example.com
```

### blacklist_wildcard.txt / whitelist_wildcard.txt

每行一个通配符规则：

```
# 匹配所有子域名
*.ad.example.com

# 匹配包含特定字符串的域名
*-ad.example.com*
```

## 更新规则

1. 修改对应的规则文件
2. 更新 `version.json` 中的版本号（递增）
3. 提交并推送到 GitHub

App 会自动检测版本变化并下载更新。

## 注意事项

- jsDelivr 有缓存，更新后可能需要等待几分钟才能生效
- 如需立即生效，可以在 URL 中添加版本号：`@main` → `@v1.0.1`
- 规则文件使用 UTF-8 编码

