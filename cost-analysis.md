# VPC Endpoint Cost Analysis

## Baseline NAT Gateway Metrics

| Metric | Before Endpoints | After Endpoints |
|--------|-----------------|-----------------|
| BytesOutToDestination | ~11 MB | ~13 KB |
| BytesOutToSource | ~88 MB | ~17 KB |

## Analysis

Before deploying VPC endpoints:
- All S3 and DynamoDB traffic flowed through the NAT Gateway
- Significant data processing occurred (~tens of MB)

After deploying Gateway endpoints:
- S3 and DynamoDB traffic bypassed the NAT Gateway
- NAT Gateway traffic dropped to near-zero levels
- Only minimal system traffic remained

## Monthly Cost Projection

| Traffic Type | Volume | Before (NAT GW) | After (Endpoint) | Savings |
|-------------|--------|------------------|-------------------|---------|
| S3          | 500 GB | $22.50           | $0.00             | $22.50  |
| DynamoDB    | 50 GB  | $2.25            | $0.00             | $2.25   |
| Other       | 10 GB  | $0.45            | $0.45             | $0.00   |

### NAT Gateway Hourly Cost
- $0.045/hr ≈ $32.85/month

## Total

- Before: $58.05/month
- After:  $33.30/month

## Savings

- Monthly: $24.75
- Annual:  $297

## Key Takeaways

1. Gateway endpoints for S3 and DynamoDB are free and eliminate NAT data processing costs
2. NAT Gateway costs can be significantly reduced for data-heavy workloads
3. CloudWatch metrics clearly show the reduction in traffic
4. Remaining NAT traffic can be optimized further using Interface endpoints
