## 商城研发部前端环境分支管理



##### 说环境就必须说大环境, 此环境又非彼环境,

细品研发部整个开发阶段的流程

![](https://img-crs-test.vchangyi.com/goods16076742896690.png)

so, 发布环境也就出现了多个. 以下是发布不同环境时的一些关键信息

| 环境   | 分支正则      | yaml文件命名         | 是否需要审核 | 不在使用的环境是否需要下架 |
| ---- | --------- | ---------------- | ------ | ------------- |
| 开发环境 | dev/*     | dev-xxx.yaml     | 否      | 否             |
| 测试环境 | test/*    | test-xxx.yaml    | 否      | 是             |
| 验收环境 | uat/*     | uat-xxx.yaml     | 否      | 是             |
| 灰度环境 | release/* | release-xxx.yaml | 是      | 是             |
| 线上   | tag       | tag-xxx.yaml     | 是      | 否             |



举例:  小王同学正在开发一个迭代 v2.2.2;  

开发时, master 切一个开发分支为: feature/v3.3.2

开发完成, 要提交测试了. 步骤如下:

1. 切分支, 切对应环境分支

   ```js
   从 master 切一个 test/v3.3.2 分支.
   ```

2. 修改 yarm 文件名.  文件名必须要和分支名对应!!!

   ```js
   // 注: test-xxx.yarm时master自带的模版
   修改 ci-cd/deployments/k8s-test 目录下的 test-xxx.yarm  为 test-v3.3.2

   // yarm 文件的查找.  在 ci-id/deployments 的目录下.
   // - k8s-dev (开发环境) 
   // - k8s-test (测试环境)
   // - k8s-uat (验收环境)
   // - k8s-prod (灰度环境 / 正式环境)
   ```

3. 修改 hash 值

   ```js
   // 大概在73 - 78行, 
   - Host: Host(`crs-test-h5-shop.vchangyi.com`) && PathPrefix(`/sass/hash`)

   hash 修改为要发的企业的hash:

   // 1f388045ab649d5e65cd10b9cabcc15a 畅鲟pro
   - Host: Host(`crs-test-h5-shop.vchangyi.com`) && PathPrefix(`/sass/1f388045ab649d5e65cd10b9cabcc15a`)

   ```

4. 推送到 gitlab 代码库, 会自动触发 jenkins发布. 

5. 查看 jenkins 网站([传送门点这里](http://ci.tools.vchangyi.com/view/CRS/job/k8s/job/crs-ci-test-dev/)), 跟踪发布进度, 到了Check deploy config 阶段, 需要开发点击确认

   ![](https://img-crs-test.vchangyi.com/goods16077676472570.png)

6. 发布完成, 登陆对应企业确认最新代码发布完成.















