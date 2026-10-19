# media-bridge-plugins（个人插件包）

给 [MediaBridge（媒体桥）](https://github.com/dlushu/MediaBridge) 用的第三方插件包。官方仓库是
[dlushu/media-bridge-plugins](https://github.com/dlushu/media-bridge-plugins)，本仓库只放自己写的插件。

## 插件

| id | 名称 | 类型 | 版本 | 说明 |
|---|---|---|---|---|
| `guoyu` | 我的片库 | home | 2.2.0 | 客户端首页那几排媒体库由它生成，每行可配（标题/影剧/语言/类型/国家/排序/年份窗口/条数） |

## 安装

1. 面板 → 插件 → 上传 `.tar.gz`，选 `packages/guoyu/guoyu-2.2.0.tar.gz`
2. 打开「我的片库」设置页，填自己的 **TMDB v4 Read Access Token**（`eyJ…` 那串；v3 的 32 位 key 不能用）
3. 客户端退出重进一次，首页就是这 10 行：
   国语剧 / 国语综艺 / 国语短剧 / 国漫 / 国语电影 / 欧美剧 / 欧美电影 / 日韩剧 / 日韩电影 / 日漫

## 更新

包内 `plugin.json` 声明了 `updateUrl`：

```
https://raw.githubusercontent.com/utterliar1/media-bridge-plugins/main/packages/guoyu/update.json
```

面板会读这份清单（`{version, url, md5, changelog}`），发现版本更新就在插件管理页出现「可更新」，
一键更新走的校验与手动安装完全相同。**覆盖安装会保留插件自己的 `data/`**，所以行配置和 Token 不会丢。

## 目录结构（沿用官方仓库的格式）

```
index.json                        # 清单（schema 2），面板若把它当插件库源时可读
packages/<id>/<id>-<版本>.tar.gz  # 包本身（tar 顶层即包内容，不套目录）
packages/<id>/update.json         # 自更新清单：version / url(同目录文件名) / md5 / changelog
```

想把它当成面板的插件库源（`PLUGIN_REPO` 环境变量）可以填 `utterliar1/media-bridge-plugins`，
注意面板的插件库只有一个源，换掉就看不到官方仓库的包了。

## 包里有什么

- 只有插件代码：`index.js`、`plugin.json`、`ui/app.js`、`ui/index.html`
- **不含任何人的配置与凭证**（插件数据目录 `data/` 不进包，Token 由使用者自己填）
- 只调用 TMDB 公开接口取元数据行；片源由面板的聚合/源插件负责，与版权资源无关
