# Quick Start Doc

> 快速开始

```
全局安装 docsify-cli工具，方便创建以及在本地生成的文档
npm i docsify-cli -p
```



> 初始化项目

```
docsify init xyz
```



> 启动服务器

```
docsify serve xyz
```



> 显示多页文档

```
.
└── docs
    ├── README.md
    ├── guide.md
    └── zh-cn
        ├── README.md
        └── guide.md
        
docs/README.md        => http://domain.com
docs/guide.md         => http://domain.com/guide
docs/zh-cn/README.md  => http://domain.com/zh-cn/
docs/zh-cn/guide.md   => http://domain.com/zh-cn/guide
```



> 定制侧边栏

```
<!-- index.html -->
<script>
  window.$docsify = {
    loadSidebar: true
  }
</script>
<script src="//cdn.jsdelivr.net/npm/docsify/lib/docsify.min.js"></script>
```



> 创建_sidebar.md文件

```
<!-- docs/_sidebar.md -->

* [首页](zh-cn/)
* [指南](zh-cn/guide)
```

