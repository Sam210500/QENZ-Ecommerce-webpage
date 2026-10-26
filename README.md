# QENZ Ecommerce Platform

A beginner-friendly **modular monolith** for learning ecommerce SDLC. The initial working slice is a customer storefront plus Flask API and SQLite database. The folder structure reserves space for later mobile, staff, inventory, payment and delivery features without pretending those features already exist.

## Structure

```text
ecommerce-platform/
├── docs/                       # SDLC, requirements, design, test, deployment
├── apps/
│   ├── customer-web/            # Working storefront (HTML/CSS/JS)
│   ├── customer-mobile/         # Future React Native + Expo app
│   ├── delivery-mobile/         # Future delivery app
│   └── staff-web/               # Staff portal starter, not yet secured
├── backend/
│   ├── app/api/                 # HTTP routes
│   ├── app/core/                # Configuration
│   ├── app/modules/             # Domain service boundaries
│   ├── app/db/                  # SQLite connection/schema/seeds
│   ├── migrations/              # Migration plan
│   └── tests/                   # API tests
├── infra/                       # Future deployment config
├── scripts/                     # Developer helper scripts
├── .env.example
└── .gitignore
```

## Run on Windows / VS Code

Open this entire `ecommerce-platform` folder in VS Code. In the terminal, from the repository root:

```powershell
py -m venv .venv
.venv\Scripts\activate
pip install -r backend/requirements.txt
$env:PYTHONPATH = "backend"
python -m app.main
```

Then visit `http://127.0.0.1:5000`. Do not use Live Server on port 5500 for this project; Flask serves the frontend and API together.

## API endpoints

- `GET /api/health`
- `GET /api/products`
- `GET /api/products?category=Graphic`
- `GET /api/products?q=classic`
- `GET /api/products/<product_id>`
- `POST /api/orders`
- `GET /api/orders/<order_id>`

Example order body:

```json
{
  "customer_name": "Demo Customer",
  "email": "demo@example.com",
  "address": "Indore, Madhya Pradesh",
  "items": [{"product_id": 1, "quantity": 2}]
}
```

## Tests

```powershell
$env:PYTHONPATH = "backend"
python -m unittest discover -s backend/tests -p "test_*.py"
```

## Important boundaries

- The cart is stored in browser local storage.
- Orders are **demo orders**; no payment gateway is integrated.
- The staff page is not protected and must not be used for real administration.
- Mobile folders are planning placeholders, not implemented apps.
- SQLite is suitable for learning/local demo use; production deployment needs a security, privacy, concurrency and database review.
- Product photos were not included in the supplied assets. Add `tee-01.jpg` through `tee-12.jpg` to `apps/customer-web/public/images/` to use your own photos.

## Troubleshooting

- **Browser shows a directory listing or Live Server page:** stop Live Server and use `http://127.0.0.1:5000` after starting Flask with the commands above.
- **`ModuleNotFoundError: No module named 'flask'`:** activate `.venv`, then run `python -m pip install -r backend/requirements.txt` again. If installation fails, check your internet connection or configure your approved Python package mirror.
- **Catalogue says it cannot connect:** check that the terminal still shows Flask running and that the browser URL uses port `5000`.
- **Product photos do not appear:** the project contains no licensed product photos by default. The generated tee illustration is the expected fallback until you add the documented image files.

Never use this demo to collect real customer information or take real payments without implementing authentication, security controls, privacy safeguards and a payment provider.
