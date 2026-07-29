---
title: "Monitoring và kiểm soát chi phí"
date: 2026-07-29
weight: 10
chapter: false
pre: " <b> 5.10. </b> "
---

## Endpoint Data Capture

Sau khi endpoint `InService`, bật capture:

```powershell
python scripts/enable_data_capture.py
Get-Content report/monitoring_setup.json
```

Script đọc endpoint config hiện tại, tạo endpoint config mới có `InitialSamplingPercentage=100`, capture Input/Output JSON vào `s3://agent-risk-scoring/monitoring/data-capture`, rồi update endpoint. Gọi API lại sau khi update hoàn tất để có capture record.

## CloudWatch metrics và dashboard

Lambda publish:

```text
Namespace: AgentRiskScorer
Metrics: RiskScore, BlockedDecisions
```

Dashboard definition nằm trong `monitoring/cloudwatch_dashboard.json`; nó có widget endpoint invocation/latency/errors, Lambda invocation/error/duration và policy metrics. Trong CloudWatch Console mở Metrics → All metrics → `AgentRiskScorer` sau khi gọi safe/risky API.

Tạo dashboard từ chính definition trong repository:

```powershell
aws cloudwatch put-dashboard `
  --dashboard-name agent-risk-scorer-dashboard `
  --dashboard-body file://monitoring/cloudwatch_dashboard.json `
  --region ap-southeast-1
```

## Optional alert demo

Source project có custom metrics và dashboard definition nhưng **không có CloudWatch Alarm historical**. Nếu rubric cần chứng minh alert trong một lần rerun, tạo alarm demo không có notification action sau khi đã gọi risky request ở 5.8:

```powershell
aws cloudwatch put-metric-alarm `
  --alarm-name agent-risk-scorer-blocked-decisions-demo `
  --alarm-description "Demo alarm when a blocked decision is recorded" `
  --namespace AgentRiskScorer `
  --metric-name BlockedDecisions `
  --statistic Sum `
  --period 300 `
  --evaluation-periods 1 `
  --threshold 1 `
  --comparison-operator GreaterThanOrEqualToThreshold `
  --treat-missing-data notBreaching `
  --region ap-southeast-1
```

Chờ tối đa 5 phút, rồi kiểm tra `CloudWatch → Alarms`. Alarm sẽ vào `ALARM` khi một `BlockedDecisions=1` nằm trong period. Đây là enhancement của lần rerun, không được trình bày là evidence historical của project. Xóa nó ở 5.11.

## Model Monitor boundary

`monitoring/model_monitor_config.py` chỉ là configuration draft. `REQUIRES_FLATTENED_MONITOR_INPUT = True`; project không tạo baseline hay schedule DefaultModelMonitor vì endpoint input là nested trajectory JSON. Không chụp/chứng minh một Model Monitor execution như thể nó đã tồn tại.

## Cost controls

- Processing, Training/HPO và endpoint `ml.m5.large` là resource tính phí.
- HPO demo được giới hạn `max-jobs=2`, `max-parallel-jobs=1`.
- Endpoint/API chỉ bật trong window chụp demo; cleanup ngay sau đó.
- Registry/Pipeline/S3 artifacts được giữ làm evidence; không giữ serving stack không cần thiết.

> **[ẢNH PLACEHOLDER — inference data capture]** S3 Console → bucket của bạn → `monitoring/data-capture/` sau khi gọi API. Ảnh phải thấy object capture mới; nó chỉ chứng minh endpoint capture, không phải CloudWatch metric.

> **[ẢNH PLACEHOLDER — CloudWatch decision metrics]** CloudWatch → Metrics → `AgentRiskScorer`. Chụp graph có `RiskScore` và `BlockedDecisions` datapoints sau safe/risky request. Đây là ảnh metrics/dashboard.

> **[ẢNH PLACEHOLDER — optional blocked-decision alarm]** Chỉ khi đã chạy optional alert command: CloudWatch → Alarms → `agent-risk-scorer-blocked-decisions-demo` có state `ALARM`. Chú thích rõ đây là rerun enhancement, không phải historical project evidence.

