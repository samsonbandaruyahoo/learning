# Playwright Python Web Project

This project demonstrates how to automate browser-based web testing and web interactions using Python and Playwright.

## Overview

Playwright is a modern browser automation framework that supports Chromium, Firefox, and WebKit. With Python, it can be used for:

- End-to-end testing
- UI validation
- Browser automation
- Regression testing
- Web scraping and form interaction

## Prerequisites

Before running this project, ensure you have the following installed:

- Python 3.9 or later
- pip package manager
- A modern browser runtime (Playwright installs its own browser binaries)

## Installation

1. Create and activate a virtual environment:

```bash
python -m venv .venv
```

On Windows:

```bash
.venv\Scripts\activate
```

On macOS/Linux:

```bash
source .venv/bin/activate
```

2. Install dependencies:

```bash
pip install -r requirements.txt
```

If you do not yet have a requirements file, install Playwright directly:

```bash
pip install playwright pytest
playwright install
```

## Project Structure

```text
project-root/
├── tests/
│   └── test_example.py
├── pages/
│   └── login_page.py
├── utils/
│   └── helpers.py
├── requirements.txt
├── pytest.ini
├── README.md
└── .env
```

## Example Test

```python
from playwright.sync_api import sync_playwright


def test_example():
    with sync_playwright() as p:
        browser = p.chromium.launch(headless=False)
        page = browser.new_page()
        page.goto("https://example.com")

        assert "Example Domain" in page.title()

        browser.close()
```

## Running Tests

Run the full test suite:

```bash
pytest
```

Run a specific test file:

```bash
pytest tests/test_example.py
```

Run Playwright in headed mode for debugging:

```bash
pytest --headed
```

## Common Playwright Commands

- Install browsers:

```bash
playwright install
```

- Install browsers with OS dependencies:

```bash
playwright install --with-deps
```

- Run with verbose output:

```bash
pytest -v
```

## Best Practices

- Use explicit waits instead of fixed sleep times.
- Keep selectors stable and readable.
- Separate page logic into page object classes.
- Store environment variables in a `.env` file or CI secrets.
- Run tests in headless mode for CI and headed mode for debugging.

## Environment Variables

Example `.env` file:

```env
BASE_URL=https://example.com
USERNAME=testuser
PASSWORD=secretpassword
```

Use `python-dotenv` or configuration files to load these values safely.

## CI/CD Considerations

For continuous integration, ensure the environment includes:

- Python installed
- Browser binaries installed via Playwright
- A browser-compatible headless environment
- Secure handling of secrets and environment variables

## Troubleshooting

If Playwright fails to launch browsers:

```bash
playwright install --with-deps
```

If tests fail due to timing issues, prefer:

```python
page.wait_for_load_state("networkidle")
page.wait_for_selector("text=Submit")
```

## License

This project is intended for educational and automation use. Add your preferred license if you plan to distribute it.

## Contributing

1. Create a feature branch.
2. Add or update tests.
3. Run the Playwright suite locally.
4. Submit a pull request with a clear summary.
