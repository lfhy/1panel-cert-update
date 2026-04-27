# 1panel-cert-update

无第三方依赖的 1Panel 证书更新脚本，使用 `bash + curl + awk + md5sum` 调用 1Panel 开发 API。

## 默认路径

- 工作目录: `/opt/1panel-cert-update`
- 配置文件: `/opt/1panel-cert-update/config.env`
- 证书文件: `/opt/1panel-cert-update/cert.pem`
- 私钥文件: `/opt/1panel-cert-update/cert.key`
- 执行命令: `/usr/bin/1panel-cert-update`

## 功能

- `config`
  - 交互式录入 `endpoint`、`API key`、证书路径、私钥路径、描述。
  - `endpoint` 和 `API key` 需要显式输入，留空会直接报错。
  - 列出 1Panel 证书列表，支持选择一个或多个目标证书。
- `run`
  - 读取配置文件，把 `cert.pem` 和 `cert.key` 上传到已配置的一个或多个 `SSL_ID`。
- `list`
  - 列出 1Panel 当前证书记录。
- `bootstrap`
  - 新建一个专用证书记录。
  - 如果当前证书文件不存在，会临时生成一张自签证书用于占位。

## 用法

下载安装:

保存仓库的`1panel-cert-update`到 `/usr/bin` 下，赋予执行权限

```bash
chmod +x /usr/bin/1panel-cert-update
```

首次配置:

```bash
/usr/bin/1panel-cert-update config
```

默认更新:

```bash
/usr/bin/1panel-cert-update
```

查看当前配置:

```bash
/usr/bin/1panel-cert-update show-config
```

批量指定多个目标证书:

```bash
/usr/bin/1panel-cert-update config --ssl-ids 2,3,5
```

## 说明

- `1Panel-Token` 按文档规则生成:
  - `md5("1panel" + API_KEY + UnixTimestamp)`
- `config.env` 为 shell 格式，权限建议保持 `600`。
- 多站点更新是“同一份证书同时更新多个 1Panel 证书记录”。
