# Consumer-Provider Handshake

## Thong tin chung

- Lab: FIT4110 Lab 03
- Ngay: 2026-06-14
- Provider team: Core Business
- Consumer team: Access Gate
- Provider service: core-business-policy
- Consumer service: access-gate

## Contract

- Contract file: `contracts/core-business-policy.openapi.yaml`
- Mock base URL: `http://localhost:4010`
- Auth method: Bearer token via `Authorization: Bearer {{authToken}}`
- Endpoint duoc test: `POST /access/check`, `GET /policies/access`, `GET /policies/access/{policyId}`, `GET /decisions`, `GET /health`

## Smoke test

### Request

```http
POST /access/check
Authorization: Bearer <token>
Content-Type: application/json
Idempotency-Key: idem-20260614-0001
X-Correlation-Id: fit4110-lab03-core-policy-0001
```

```json
{
  "gateId": "GATE-02",
  "direction": "EXIT",
  "occurredAt": "2026-06-14T13:03:00Z",
  "credential": {
    "credentialType": "PLATE",
    "plateNumber": "30F-88888"
  },
  "vehiclePlate": "30F-88888",
  "requestedByDeviceId": "DEVICE-GATE-02"
}
```

### Expected response

```json
{
  "decisionId": "0196fb3d-4ad7-7d1e-9f49-5d5148d2babc",
  "allow": false,
  "reasonCode": "OUTSIDE_ALLOWED_WINDOW",
  "policyId": "POL-VISITOR-DAYTIME",
  "gateId": "GATE-02",
  "expiresAt": "2026-06-14T13:01:10Z",
  "evaluatedAt": "2026-06-14T13:01:00Z",
  "correlationId": "req-20260614-0002"
}
```

## Ket qua

- [x] Consumer goi mock thanh cong.
- [x] Consumer parse duoc field can dung: `allow`, `reasonCode`, `expiresAt`.
- [x] Consumer hieu loi 4xx/5xx provider tra ve qua `Problem`.
- [x] Co Newman report trong `reports/`.

## Ghi chu thay doi hop dong

| Noi dung | Truoc | Sau | Nguoi dong y |
|---|---|---|---|
| Lab 03 artifact | IoT sample contract/collection | Pair 10 Core Business Access Policy contract/collection | Access Gate, Core Business |
| Auth tren Prism | Mock khong validate token that | Auth tests cho phep mock limitation, local bat buoc 401/403 | Access Gate, Core Business |
| Idempotency | Chua co evidence trong collection Lab 3 | Them `Idempotency-Key` va conflict scenario | Access Gate, Core Business |

## Xac nhan

- Provider representative: Core Business representative
- Consumer representative: Access Gate representative
