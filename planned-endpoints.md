Below is the cleaned-up v1 surface for our Loyalty API. All routes are prefixed with `/api/v1`.

---

## 🔐 Authentication

| Method | Endpoint         | Description                              |
| ------ | ---------------- | ---------------------------------------- |
| POST   | `/auth/register` | Create a new user account                |
| POST   | `/auth/login`    | Log in (returns access & refresh tokens) |
| POST   | `/auth/refresh`  | Refresh access token                     |
| POST   | `/auth/logout`   | Logout (revoke token)                    |
| GET    | `/auth/me`       | Get current user profile                 |

---

## 👤 Users (Admin)

| Method | Endpoint          | Description                    |
| ------ | ----------------- | ------------------------------ |
| GET    | `/users`          | List all users                 |
| GET    | `/users/{userId}` | Get user details               |
| PATCH  | `/users/{userId}` | Update user profile/attributes |
| DELETE | `/users/{userId}` | Deactivate or delete a user    |

---

## ⭐ Points

| Method | Endpoint                       | Description               |
| ------ | ------------------------------ | ------------------------- |
| GET    | `/users/{userId}/points`       | Get current point balance |
| POST   | `/users/{userId}/points/earn`  | Award points              |
| POST   | `/users/{userId}/points/spend` | Spend/deduct points       |

---

## 📜 Points History

| Method | Endpoint                            | Description                      |
| ------ | ----------------------------------- | -------------------------------- |
| GET    | `/users/{userId}/points/history`    | User’s point events (earn/spend) |
| GET    | `/points/history?start=&end=&type=` | Global history view (admin)      |

---

## 🎯 Objectives & User Objectives

### Objectives

| Method | Endpoint                    | Description                                   |
| ------ | --------------------------- | --------------------------------------------- |
| GET    | `/objectives`               | List active objectives (supports `?segment=`) |
| GET    | `/objectives/{objectiveId}` | Get objective details                         |

### User Objectives

| Method | Endpoint                                            | Description                        |
| ------ | --------------------------------------------------- | ---------------------------------- |
| GET    | `/users/{userId}/objectives`                        | List objectives assigned to a user |
| POST   | `/users/{userId}/objectives/{objectiveId}/complete` | Mark objective as completed        |
| PATCH  | `/user-objectives/{id}`                             | Update progress or deadline        |

---

## 🎁 Prizes & Redemptions

| Method | Endpoint                      | Description                               |
| ------ | ----------------------------- | ----------------------------------------- | 
| GET    | \`/prizes?isDigital=true      | List prize catalog                        |
| GET    | `/prizes/{prizeId}`           | Get prize details                         |
| POST   | `/prizes/{prizeId}/redeem`    | Redeem a prize (creates redemption entry) |
| GET    | `/users/{userId}/redemptions` | User’s redemption history                 |
| GET    | `/redemptions`                | All redemptions (admin view)              |
| PATCH  | `/redemptions/{redemptionId}` | Approve/reject/cancel redemption          |

---

## 📺 Videos & Quizzes

| Method | Endpoint                             | Description                         |
| ------ | ------------------------------------ | ----------------------------------- |
| GET    | `/videos?segment=`                   | List training videos                |
| GET    | `/videos/{videoId}`                  | Get video metadata & URL            |
| GET    | `/videos/{videoId}/quiz`             | Get quiz questions for a video      |
| POST   | `/videos/{videoId}/quiz/submissions` | Submit quiz answers                 |
| GET    | `/users/{userId}/quiz-submissions`   | List user quiz submissions          |
| GET    | `/quiz-submissions/{submissionId}`   | Get quiz submission details & score |

---

## 🔮 Future Extensions

* **Custom Objectives**

  * POST   `/objectives/custom`
  * GET/PATCH/DELETE `/objectives/custom/{id}`

* **Tenancy Management**

  * GET   `/tenants`
  * POST  `/tenants`
  * GET/PATCH/DELETE `/tenants/{tenantId}`
  * GET/PATCH `/tenants/{tenantId}/settings`

* **KPIs & Reporting**

  * GET   `/kpis`
  * GET   `/kpis/{kpiId}`
  * GET   `/kpis/{kpiId}/values?start=&end=`
  * POST  `/kpis/{kpiId}/values`

---

**Notes:**

* Versioning: All routes are under `/api/v1`.
* Pagination & Filtering: Use `?page=&limit=&sort=&segment=` uniformly.
* Error Handling: Return standardized problem JSON (`code`, `detail`, `fields`).
* Security: Protect via JWT/OAuth scopes;
