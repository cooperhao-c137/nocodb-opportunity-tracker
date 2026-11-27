# nocodb-opportunity-tracker

## NocoDB 商机跟进试用

本仓库用 NocoDB 官方容器和 SQLite 试跑。配置只监听本机，容器数据保存在 Docker 卷中。仓库内的客户、日期和金额均为虚构示例。

## 启动

安装并启动 Docker Desktop 后，在本目录执行：

```sh
docker compose up -d --wait --wait-timeout 180
curl.exe -fsS http://localhost:8080/api/v1/health
```

浏览器打开 http://localhost:8080，按界面提示创建本机管理员。停止试用用 `docker compose down`，数据卷会保留。

## 配置商机表

1. 将 `demo/` 下的四个 CSV 分别导入同一 Base。按商机 ID 将行动、预测和里程碑的记录关联到商机。CSV 中的 ID 是匹配键，导入后需建立关联字段。
2. 在预测表加公式字段：数量或单价缺失时留空，否则为预计供货量乘预计单价。商机表对关联预测金额求和，一次性费用有依据时单列加入。按币种查看金额，待估项目保留「待估算」状态，已确认订单额单独记录。
3. 商机按阶段建立看板，行动按截止日建立本周与逾期筛选，里程碑按日期建立日历。可用时间线的版本也可从里程碑表配置时间线。
4. 验收时把样例 A 的 2027 年数量从 120 改到 121，确认总额由 10,140 EUR 更新到 10,175 EUR，样例 B 仍为待估算。修改行动状态后确认本周视图同步变化。

部署配置参考 [NocoDB 官方仓库](https://github.com/nocodb/nocodb) 的 Docker with SQLite 方式。
