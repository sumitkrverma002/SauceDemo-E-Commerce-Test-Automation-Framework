# SauceDemo-E-Commerce-Test-Automation-Framework
A Hybrid Automation Framework (Page Object Model + Data-Driven Testing)
built with Selenium WebDriver, Python, and PyTest, targeting the
SauceDemo e-commerce demo application.
Why "Hybrid"?
This framework combines two design approaches:
Page Object Model (POM) — every page (Login, Inventory, Cart,
Checkout) has its own class holding locators and actions, keeping
test logic separate from UI element details.
Data-Driven Testing — test inputs (login credentials, checkout
details, product names) are stored externally in
`data/test_data.xlsx` and read at runtime via `openpyxl`, instead
of being hardcoded. Adding a new scenario means adding an Excel
row, not touching Python code.
Tech Stack
Category	Tools
Language	Python 3.11
Automation	Selenium WebDriver
Test Runner	PyTest (fixtures, markers, parametrization)
Test Data	Excel (openpyxl)
Reporting	pytest-html
CI/CD	GitHub Actions
Project Structure
```
saucedemo-hybrid-framework/
├── pages/                  # Page Object classes
│   ├── base_page.py        # Common reusable Selenium actions
│   ├── login_page.py
│   ├── inventory_page.py
│   ├── cart_page.py
│   └── checkout_page.py
├── tests/                  # PyTest test cases
│   ├── test_login.py       # Data-driven login scenarios
│   ├── test_cart.py        # Add/remove/sort cart tests
│   └── test_checkout.py    # End-to-end checkout flow
├── utils/
│   └── excel_reader.py     # Reads test data from Excel
├── data/
│   └── test_data.xlsx      # Login, checkout & product test data
├── conftest.py             # PyTest fixtures (WebDriver setup/teardown)
├── pytest.ini               # Markers config (smoke / regression)
├── requirements.txt
└── .github/workflows/ci.yml # Runs smoke suite on every push
```
Test Coverage
Login — valid user, locked-out user, problem user, performance
glitch user, invalid password (data-driven scenarios)
Cart — add single/multiple items, remove item, price sorting
Checkout — end-to-end order flow, form validation
17 test cases total across smoke and regression suites.
Setup & Run Locally
```bash
# 1. Clone the repo
git clone <your-repo-url>
cd saucedemo-hybrid-framework

# 2. Create a virtual environment
python -m venv venv
venv\Scripts\activate      # Windows
source venv/bin/activate   # macOS/Linux

# 3. Install dependencies
pip install -r requirements.txt

# 4. Run all tests
pytest

# 5. Run only smoke tests
pytest -m smoke

# 6. Run only regression tests
pytest -m regression

# 7. Generate an HTML report
pytest --html=reports/report.html --self-contained-html
```
> Requires Google Chrome installed. Selenium 4.6+ auto-manages the
> matching ChromeDriver, so no manual driver download is needed.
CI/CD
Every push to `main` triggers `.github/workflows/ci.yml`, which
installs dependencies, runs the smoke suite headlessly on GitHub's
Ubuntu runner, and uploads the HTML report as a build artifact.
Adding a New Test Scenario
No code change needed for new data — just open
`data/test_data.xlsx` and add a row to the relevant sheet
(`login_data`, `checkout_data`, or `product_data`). The test
functions pick it up automatically via `pytest.mark.parametrize`.
Author
Sumit Kumar — Software Test Engineer
