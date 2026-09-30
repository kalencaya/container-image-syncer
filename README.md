# container-image-syncer

**主要功能：**

*   **安全认证**: 通过 GitHub Secrets 存储你的 Aliyun ACR 登录凭据，确保敏感信息不被泄露。
*   **自动化构建**: 每次代码提交都会触发 Docker 镜像的自动构建。
*   **无缝集成**: 直接将构建好的 Docker 镜像推送到你指定的 Aliyun ACR 仓库。

## 📋 先决条件

在开始使用本模板之前，请确保你已拥有以下条件：

*   一个 GitHub 账号。
*   一个阿里云账号，并已开通 [容器镜像服务 (Container Registry, ACR)](https://cr.console.aliyun.com/cn-hangzhou/instances)。
*   在 ACR 中已创建至少一个**命名空间**。
*   拥有推送到该 ACR 仓库的权限（通常是子账号的 AccessKey 或为 ACR 设置的固定密码）。

## 🔑 配置 GitHub Secrets (核心步骤)

**在使用本模板前，你必须先 Fork 本仓库，然后在你 Fork 后的个人仓库中设置以下 GitHub Secrets。**

GitHub Secrets 允许你安全地存储敏感信息，如 API 密钥或密码。它们在工作流运行日志中永远不会被暴露。

### 设置步骤

1.  **第一步：Fork 本仓库**
    点击本页右上角的 "**Fork**" 按钮，将本仓库复制到你自己的 GitHub 账号下。

2.  **第二步：进入你 Fork 后的仓库设置**
    导航到 **你 Fork 后的仓库页面** (例如：`github.com/你的用户名/本仓库名`)。
    点击顶部的 "**Settings**" (设置)。

3.  **第三步：进入 Secrets 和 Variables 配置页面**
    在左侧导航栏中，找到并点击 "**Secrets and variables**"。
    点击其下的子菜单 "**Actions**"。

4.  **第四步：添加 Repository Secrets**

    点击右上角的 "**New repository secret**" (新建仓库秘钥)。

    你需要添加以下四个 Secrets。请根据你在 Aliyun ACR 中的实际信息进行填写：

    *   **`ACR_USERNAME`**
        *   **描述**: Aliyun ACR 的登录用户名。通常是你的阿里云主账号名或拥有 ACR 操作权限的子账号名。
        *   **值**: 你的 Aliyun ACR 用户名，例如 `your_aliyun_account_name`。

    *   **`ACR_PASSWORD`**
        *   **描述**: Aliyun ACR 的登录密码。这通常是你为 ACR 设置的固定密码，而不是你的阿里云登录密码。你可以在 ACR 控制台的 "访问凭证" 或 "实例概览" 中找到并设置。
        *   **值**: 你的 Aliyun ACR 密码。

    *   **`ACR_REGISTRY`**
        *   **描述**: Aliyun ACR 的注册表地址。这取决于你的地域。例如：
            *   华东1/杭州: `registry.cn-hangzhou.aliyuncs.com`
            *   华东2/上海: `registry.cn-shanghai.aliyuncs.com`
            *   华南1/深圳: `registry.cn-shenzhen.aliyuncs.com`
            *   ...更多请参考阿里云官方文档。
        *   **值**: 你的 Aliyun ACR Registry URL，例如 `registry.cn-hangzhou.aliyuncs.com`。

    *   **`ACR_NAMESPACE`**
        *   **描述**: 你在 Aliyun ACR 中创建的命名空间名称。所有推送到 ACR 的镜像都会归属到某个命名空间下。
        *   **值**: 你的 Aliyun ACR 命名空间名称，例如 `my-project-namespace`。

### 关于 GitHub Variables (可选)

虽然本工作流的核心是 Secrets，但你也可以在 "Secrets and variables" -> "Actions" 页面下点击 "**Variables**" 标签页，并点击 "**New repository variable**" 来添加非敏感配置信息。

