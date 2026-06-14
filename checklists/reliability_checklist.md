# Reliability Checklist - FIT4110 Lab 03

## 1. Functional tests

- [x] Co test cho endpoint health.
- [x] Co test happy path cho endpoint chinh `/access/check`.
- [x] Co kiem tra status code 2xx.
- [x] Co kiem tra field quan trong trong response: `decisionId`, `allow`, `reasonCode`, `gateId`.
- [x] Co test doc du lieu danh sach: `/policies/access` va `/decisions`.

## 2. Auth tests

- [x] Co test thieu token.
- [x] Co test sai token.
- [x] Endpoint public `/health` duoc khai bao `security: []` trong contract.
- [x] Test the hien expected status 401/403 tren local service; voi Prism mock co ghi chu limitation vi mock khong validate auth that.

## 3. Negative tests

- [x] Co test thieu field bat buoc `gateId`.
- [x] Co test sai mien du lieu `direction=SIDEWAYS`.
- [x] Co test sai enum hoac gia tri ngoai mien.
- [x] Loi tra ve theo cung error model `Problem`.

## 4. Boundary tests

- [x] Co test max pagination `limit=100`.
- [x] Co test limit/pagination cho endpoint danh sach.
- [x] Co test idempotency/retry conflict bang fixed `Idempotency-Key`.
- [x] Co ghi chu ky vong xu ly du lieu bien trong test-case matrix.

## 5. Reliability tests co ban

- [x] Co kiem tra response time cho local-only nonfunctional test.
- [x] Timeout mong muon: Access Gate can nhan decision truoc khi `expiresAt`; local health response duoi 1000ms.
- [x] Co test va ghi chu retry/idempotency bang `Idempotency-Key`.
- [x] Co consumer-side smoke test: Access Gate goi Core Business policy mock.

## 6. Evidence

- [x] Collection export JSON.
- [x] Environment mock export JSON.
- [x] Environment local export JSON.
- [x] Newman report XML/HTML.
- [x] Test-case matrix da dien.
- [x] Bien ban handshake da dien.
