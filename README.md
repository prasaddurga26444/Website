# ShopSphere Local Demo Website

This folder is the standalone, static ShopSphere practice storefront. It is separate from the Python/Selenium automation framework in the repository root and is intended to be deployed as its own Vercel project.

The page uses only HTML, CSS, and browser JavaScript. It does not need Python, Node.js, build commands, environment variables, a database, or secrets. Its products and prices are synthetic. The cart and simulated order use browser storage; no real payment is processed.

## Deploy with Vercel

1. Push this repository to a Git provider that Vercel can access.
2. In Vercel, create a project from that repository.
3. Set the Vercel project's **Root Directory** to `mock_app`.
4. Select the **Other** framework preset. Leave the build command empty. If an output directory is required, use `.`.
5. Deploy and open the resulting `https://...vercel.app` URL. The home page should show the product catalog.

Only this folder is the Vercel website project. The root-level Python automation framework is not deployed to Vercel.

## Run the Selenium Framework Against the Deployment

In the root `.env` file, set `BASE_URL` to the deployed site's origin without a trailing slash:

```dotenv
BASE_URL=https://your-project.vercel.app
BROWSER=chrome
TIMEOUT=10
HEADLESS=false
```

Then run pytest from the repository root in PowerShell:

```powershell
.\.venv\Scripts\python.exe -m pytest -v --html=reports/report.html --self-contained-html
```

Selenium runs on your computer and opens the Vercel URL. Vercel only serves the website. The project tests expect the selectors and behavior in this mock; a different website needs its own inspected page objects and assertions.

To return to the built-in local mode, clear the `BASE_URL` value in the root `.env` file. Pytest will then start a temporary server for this folder automatically.