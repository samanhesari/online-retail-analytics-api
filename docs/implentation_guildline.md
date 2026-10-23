# Online Retail Analytics API
## Complete Implementation Guide: From Zero to Production

**Project name:** `online-retail-analytics-api`  
**Language:** Python  
**Core technologies:** FastAPI, pandas, NumPy, scikit-learn, pytest, Ruff, Docker, GitHub Actions, AWS EC2  
**Document purpose:** A step-by-step implementation roadmap from project setup to production deployment.

---

# 1. Project Overview

## 1.1 Goal

Build a modular, tested, and deployable retail analytics API that can process transaction data, generate business insights, and eventually provide machine-learning predictions.

The project should demonstrate practical skills in:

- Python software engineering
- Data cleaning and validation
- Exploratory data analysis
- Business analytics
- Customer segmentation
- Time-series forecasting
- REST API development
- Automated testing
- Code quality and version control
- Docker containerization
- Continuous integration and deployment
- Cloud deployment and operational monitoring

## 1.2 Final expected capabilities

By the end of the project, the system should support:

1. Loading and validating retail transaction data.
2. Producing data-quality reports.
3. Calculating sales, customer, and product metrics.
4. Performing RFM customer analysis.
5. Measuring customer cohorts and retention.
6. Performing market-basket analysis when the data supports it.
7. Training and evaluating customer segmentation models.
8. Developing demand forecasting where sufficient time-series data is available.
9. Serving selected analytics and predictions through a REST API.
10. Running automated tests and code-quality checks.
11. Packaging the service in Docker.
12. Deploying a versioned release to AWS EC2.
13. Documenting installation, operation, limitations, and maintenance.

**Important:** These are target capabilities, not features that exist automatically because their files have been created. Mark features as planned, in progress, or implemented in the README.

## 1.3 Development philosophy

Build a small, working system first. Expand it only after its existing functionality is correct.

The recommended sequence is:

**Data → Data quality → Core analytics → Advanced analytics → API → Machine learning → Testing and hardening → Docker → CI/CD → AWS deployment.**

Do not begin by implementing every module at once.

---

# 2. Target Project Structure

Use the following structure as the intended architecture. Create modules when you are ready to implement them; empty files are not completed features.

```text
online-retail-analytics-api/
├── src/
│   └── retail_analytics/
│       ├── __init__.py
│       ├── domain/
│       │   ├── __init__.py
│       │   ├── entities.py
│       │   ├── value_objects.py
│       │   └── exceptions.py
│       ├── application/
│       │   ├── __init__.py
│       │   ├── services.py
│       │   └── schemas.py
│       ├── analytics/
│       │   ├── __init__.py
│       │   ├── data_quality.py
│       │   ├── sales_analytics.py
│       │   ├── customer_analytics.py
│       │   ├── product_analytics.py
│       │   ├── rfm_analysis.py
│       │   ├── cohort_analysis.py
│       │   └── market_basket.py
│       ├── ml/
│       │   ├── __init__.py
│       │   ├── preprocessing.py
│       │   ├── feature_engineering.py
│       │   ├── customer_segmentation.py
│       │   ├── demand_forecasting.py
│       │   ├── model_evaluation.py
│       │   └── model_registry.py
│       ├── infrastructure/
│       │   ├── __init__.py
│       │   ├── data_loader.py
│       │   ├── repositories.py
│       │   ├── model_loader.py
│       │   └── logging_config.py
│       └── api/
│           ├── __init__.py
│           ├── main.py
│           ├── dependencies.py
│           └── routes/
│               ├── __init__.py
│               ├── health.py
│               ├── analytics.py
│               ├── customers.py
│               ├── products.py
│               └── predictions.py
├── data/
│   ├── raw/
│   ├── processed/
│   └── external/
├── artifacts/
│   ├── models/
│   └── reports/
├── notebooks/
│   ├── 01_data_overview.ipynb
│   ├── 02_data_quality_and_cleaning.ipynb
│   ├── 03_exploratory_data_analysis.ipynb
│   ├── 04_sales_and_revenue_analysis.ipynb
│   ├── 05_customer_behavior_analysis.ipynb
│   ├── 06_rfm_customer_segmentation.ipynb
│   ├── 07_cohort_and_retention_analysis.ipynb
│   ├── 08_product_and_market_basket_analysis.ipynb
│   ├── 09_feature_engineering_experiments.ipynb
│   ├── 10_customer_clustering_experiments.ipynb
│   ├── 11_demand_forecasting_experiments.ipynb
│   └── 12_model_evaluation_and_comparison.ipynb
├── tests/
│   ├── unit/
│   ├── integration/
│   └── fixtures/
├── scripts/
├── deployment/
│   ├── docker/
│   └── ec2/
├── docs/
├── .github/
│   └── workflows/
├── pyproject.toml
├── requirements.txt
├── requirements-dev.txt
├── Makefile
├── .env.example
├── .gitignore
├── .dockerignore
├── .python-version
├── README.md
└── LICENSE
```

## 2.1 Responsibilities of the main layers

| Layer | Responsibility |
|---|---|
| `domain/` | Core business concepts, value objects, and domain-specific exceptions |
| `application/` | Coordinates use cases and business workflows |
| `analytics/` | Calculates data-quality metrics and retail analytics |
| `ml/` | Preprocessing, feature engineering, training, evaluation, and inference |
| `infrastructure/` | Reads files, accesses resources, loads models, and configures logging |
| `api/` | Handles HTTP requests, validation, routing, and responses |
| `notebooks/` | Data exploration and model experiments |
| `tests/` | Verifies expected behavior |
| `artifacts/` | Stores locally generated reports and model artifacts |
| `deployment/` | Container and server deployment resources |
| `docs/` | Architecture, data definitions, metrics, models, and operational guidance |

Keep reusable production logic in the Python package, not exclusively in notebooks.

---

# 3. Phase 0 — Define the Scope

## Objective

Decide what the first release will do and understand the dataset before writing analytical code.

## Tasks

- [ ] Review the project README.
- [ ] Identify the target users and business questions.
- [ ] Confirm the dataset source and its terms of use.
- [ ] Confirm the dataset columns and date range.
- [ ] Write down the intended business definitions.
- [ ] Create project milestones or GitHub Issues.
- [ ] Separate planned features from implemented features.

## Questions to answer

- What does each column represent?
- What date range does the dataset cover?
- Are invoice identifiers repeated across multiple product rows?
- How are cancelled invoices represented?
- Do negative quantities represent returns?
- Are there missing customer identifiers?
- Can unit prices be zero or negative?
- Are there duplicate transaction rows?
- Is the currency documented?
- Does the data support the forecasting granularity you want?

Do not assume that all negative quantities are invalid or that every duplicate row should be deleted. Investigate the dataset and document decisions.

## Deliverables

- A defined first-release scope.
- A dataset source and license note.
- An initial list of business questions.
- A list of data assumptions and unresolved issues.

## Completion criteria

You can explain the purpose of the project, the initial feature set, and the limitations of the source data.

---

# 4. Phase 1 — Set Up the Development Environment

## Objective

Make the project reproducible and establish a reliable development workflow.

## Tasks

1. Confirm the Python version.
2. Create a virtual environment.
3. Configure runtime and development dependencies separately.
4. Configure the package layout in `pyproject.toml`.
5. Configure pytest.
6. Configure Ruff.
7. Add `.gitignore`, `.dockerignore`, and `.env.example`.
8. Initialize Git and commit the initial project setup.
9. Verify that the package can be imported and tests can run.

## Dependency plan

Likely runtime dependencies:

- FastAPI
- Uvicorn or another appropriate ASGI server
- pandas
- NumPy
- scikit-learn

Likely development dependencies:

- pytest
- Ruff
- Jupyter Notebook or JupyterLab

Add other libraries only when a real requirement exists, such as a chosen market-basket algorithm.

## Configuration rules

- Keep runtime settings configurable.
- Do not hard-code absolute paths throughout the codebase.
- Never commit real credentials or private `.env` files.
- Keep dataset files and large model artifacts out of Git unless there is a clear, justified reason.
- Record the Python version and dependency choices.

## Deliverables

- Working Python environment.
- Project configuration.
- Test and lint commands.
- Initial Git commit.
- Reproducible setup instructions in the README.

## Completion criteria

A fresh checkout can be set up by following the documentation, and the basic test and lint commands work.

---

# 5. Phase 2 — Obtain and Understand the Data

## Objective

Explore the raw data before implementing cleaning rules.

Begin with the first three notebooks.

## Notebook 01 — Data overview

File: `notebooks/01_data_overview.ipynb`

Investigate:

- File format and size.
- Number of rows and columns.
- Column names and data types.
- Date range.
- Number of invoices.
- Number of identified customers.
- Number of products and countries.
- Missing-value counts.
- Basic statistics for quantity and unit price.

Create a concise data dictionary describing every column.

## Notebook 02 — Data quality and cleaning

File: `notebooks/02_data_quality_and_cleaning.ipynb`

Investigate:

- Missing customer IDs.
- Missing product descriptions.
- Duplicate rows.
- Cancelled invoices.
- Negative quantities.
- Zero or negative prices.
- Invalid dates.
- Inconsistent product codes or descriptions.
- Implausible outliers.

Do not remove questionable records automatically. First understand their meaning and determine whether they should be excluded from a specific analysis.

For example, a returned item may reduce net sales while still being important to return-rate analysis.

## Notebook 03 — Exploratory data analysis

File: `notebooks/03_exploratory_data_analysis.ipynb`

Explore:

- Transaction volume over time.
- Quantity distributions.
- Unit-price distributions.
- Customer purchase patterns.
- Product popularity.
- Country-level activity.
- Potential seasonality.
- Unusual observations and outliers.

Record what you observe and distinguish facts from hypotheses.

## Deliverables

- Data dictionary.
- Initial quality report.
- Cleaning decisions.
- Exploratory analysis findings.
- List of known data limitations.

## Completion criteria

You understand the dataset well enough to implement repeatable validation and cleaning rules.

---

# 6. Phase 3 — Build the Data Foundation

## Objective

Move the reliable data-loading and cleaning logic out of notebooks and into tested modules.

Implement the following in order.

## 6.1 `infrastructure/data_loader.py`

Responsibilities:

- Load supported input formats.
- Validate required columns.
- Parse dates and numeric fields.
- Handle missing files with clear errors.
- Detect unsupported or malformed input.
- Preserve the raw dataset.
- Avoid silently swallowing exceptions.

Do not mix every analytical rule into the loader. Its primary responsibility is loading data and performing basic input validation.

## 6.2 `analytics/data_quality.py`

Responsibilities:

- Report missing values.
- Report duplicate rows.
- Detect invalid numeric values.
- Check date parsing.
- Identify suspicious quantities and prices.
- Return structured quality results.
- Keep reporting separate from decisions to remove or transform rows.

## 6.3 Define the cleaning policy

Document the difference between:

- **Raw data:** unchanged source records.
- **Validated data:** records that meet structural requirements.
- **Cleaned analytical data:** records prepared according to documented rules.
- **Analysis-specific data:** data filtered for a particular metric or model.

Different analyses may need different inclusion rules.

For example, gross sales, net sales, cancellations, and returns should not be mixed without an explicit definition.

## 6.4 Create test fixtures

Create a small file such as:

`tests/fixtures/sample_transactions.csv`

Include representative cases:

- Ordinary purchases.
- Multiple products in an invoice.
- Duplicate rows.
- Missing customer IDs.
- Returns or negative quantities.
- Zero or invalid prices.
- Missing or malformed dates.

Keep the fixture small enough to calculate expected outputs manually.

## 6.5 Write unit tests

Test:

- Required columns are present.
- Missing required columns cause a clear error.
- Dates parse correctly.
- Invalid dates are handled as documented.
- Missing values are detected.
- Duplicates are detected according to the chosen definition.
- Negative and zero values are reported.
- Empty datasets are handled.
- Missing files produce useful errors.
- Cleaning rules produce the expected results.
- Raw input is not unexpectedly modified.

## Deliverables

- Working data loader.
- Data-quality module.
- Explicit cleaning policy.
- Sample test fixture.
- Unit tests.

## Completion criteria

The data preparation process is repeatable, its assumptions are documented, and its behavior is verified by tests.

---

# 7. Phase 4 — Implement Core Analytics

## Objective

Implement reliable business calculations before exposing them through the API.

Build the modules in this order.

## 7.1 `analytics/sales_analytics.py`

Possible functionality:

- Revenue calculations.
- Daily, weekly, and monthly sales.
- Sales by country.
- Invoice counts.
- Average invoice value.
- Quantity sold.
- Period-over-period comparisons.

For every metric, define its calculation and the treatment of cancellations and returns.

## 7.2 `analytics/customer_analytics.py`

Possible functionality:

- Number of identified customers.
- Customer purchase frequency.
- Customer monetary value.
- Average order value.
- Repeat-customer rate.
- Last purchase date.
- Days since last purchase.

Document how missing customer IDs are treated. Do not infer customer identities that the dataset does not provide.

## 7.3 `analytics/product_analytics.py`

Possible functionality:

- Top products by revenue.
- Top products by quantity.
- Product-level sales trends.
- Product contribution to total sales.
- Product rankings by country or time period.

Use a consistent product identifier. Product descriptions can be inconsistent and should not automatically be treated as unique identifiers.

## 7.4 Define analytical contracts

For every public analytical function, document:

- Required input columns.
- Filters and business definitions.
- Output fields and data types.
- Sorting and ranking behavior.
- Handling of empty data.
- Handling of missing values.
- Expected behavior for ties and zero denominators.

## 7.5 Write unit tests

Use small, manually verifiable datasets.

Test:

- Normal calculations.
- Empty inputs.
- Boundary dates.
- Returns and cancellations.
- Missing customer IDs.
- Tied rankings.
- Invalid numeric values.
- Divide-by-zero cases.

## Deliverables

- Sales analytics.
- Customer analytics.
- Product analytics.
- Unit tests for public functions.
- Documented metric definitions.

## Completion criteria

The outputs are deterministic, documented, and verified against manually calculated expected results.

---

# 8. Phase 5 — Implement Advanced Analytics

## Objective

Build higher-level customer and product analyses on top of the trusted data foundation.

## 8.1 RFM analysis

File: `analytics/rfm_analysis.py`

RFM stands for:

- **Recency:** time since a customer's most recent qualifying purchase.
- **Frequency:** number of qualifying purchases in a defined observation window.
- **Monetary:** customer spending over the defined observation window.

Tasks:

- Define the observation window.
- Select a reference date.
- Define the purchase-counting rule.
- Define how returns and cancellations are handled.
- Define how missing customer IDs are treated.
- Establish scoring boundaries.
- Create and document segment labels.
- Validate results on a small known example.

Do not use unexplained scoring rules or assume every dataset needs the same segment definitions.

## 8.2 Cohort and retention analysis

File: `analytics/cohort_analysis.py`

Tasks:

- Define a cohort, often based on the customer's first qualifying purchase period.
- Assign customers to cohorts.
- Calculate periods since cohort entry.
- Calculate retention counts and percentages.
- Use a consistent denominator.
- Handle incomplete recent cohorts.
- Verify calculations on a small manually calculated example.

Clearly document whether retention means a customer made any qualifying purchase in a later period.

## 8.3 Market-basket analysis

File: `analytics/market_basket.py`

Tasks:

- Build baskets from invoice lines.
- Decide how duplicate product lines are handled.
- Define the treatment of returns and cancellations.
- Select an appropriate association-rule method.
- Calculate support, confidence, and lift if using association rules.
- Define thresholds based on the dataset and use case.
- Handle insufficient basket data.
- Explain that association does not establish causation.

## 8.4 Validate advanced analytics in notebooks

Use:

- `06_rfm_customer_segmentation.ipynb`
- `07_cohort_and_retention_analysis.ipynb`
- `08_product_and_market_basket_analysis.ipynb`

Use notebooks to explore the concepts. Move stable calculations into tested Python modules.

## Deliverables

- RFM analysis.
- Cohort and retention analysis.
- Market-basket analysis, if supported.
- Unit tests and documentation.
- Notes describing analytical limitations.

## Completion criteria

Each analysis has explicit assumptions, verified results, and a clear explanation of what the results do and do not mean.

---

# 9. Phase 6 — Design and Implement the FastAPI

## Objective

Expose selected analytics through a validated REST API.

Do this only after the underlying analytical functions are reliable.

## 9.1 Define endpoint contracts

Before writing each route, specify:

- HTTP method.
- URL path.
- Query parameters.
- Required and optional values.
- Response schema.
- Error behavior.
- Pagination or result limits.
- Expected performance constraints.

Use Pydantic models to define stable request and response contracts.

Avoid exposing pandas DataFrames or internal implementation details directly in API responses.

## 9.2 Suggested first endpoints

Start with a small useful set:

| Method | Endpoint | Purpose |
|---|---|---|
| GET | `/health` | Confirm the process is running |
| GET | `/ready` | Confirm required resources are ready |
| GET | `/analytics/sales` | Return a sales summary or time series |
| GET | `/analytics/products/top` | Return ranked products |
| GET | `/analytics/customers/summary` | Return customer summary metrics |
| GET | `/customers/{customer_id}/summary` | Return one customer's summary |

Add RFM, cohort, market-basket, and prediction endpoints only after their underlying functionality has been implemented and tested.

## 9.3 Implement the API modules

### `api/main.py`

Responsibilities:

- Create the FastAPI application.
- Register routers.
- Configure startup and shutdown behavior where needed.
- Configure application-level exception handling.

### `api/dependencies.py`

Responsibilities:

- Provide shared services and repositories.
- Manage dependencies used by routes.
- Avoid duplicating resource initialization.

### `api/routes/`

Responsibilities:

- Receive and validate HTTP requests.
- Delegate work to application services.
- Return documented responses.
- Translate expected application errors into appropriate HTTP errors.

### `application/services.py`

Responsibilities:

- Coordinate data access and analytics.
- Apply use-case-specific rules.
- Return results independently of HTTP.

### `application/schemas.py`

Responsibilities:

- Define request and response models where appropriate.
- Keep external API contracts separate from internal dataframe representations.

### `infrastructure/repositories.py`

Responsibilities:

- Provide a clear boundary for retrieving the data needed by the application.
- Encapsulate data-access details.

## 9.4 Error handling and security

- Validate date ranges and query limits.
- Return clear, non-sensitive error messages.
- Do not expose stack traces or filesystem paths to clients.
- Avoid loading a large dataset for every request.
- Do not return unnecessary customer-level data.
- Define authentication and authorization requirements before public production access.
- Configure CORS only for the client origins that require it.

## 9.5 Test the API

Use FastAPI's testing facilities and pytest.

Test:

- Health endpoints.
- Valid requests.
- Invalid parameters.
- Missing data or resources.
- Response schema and types.
- Expected status codes.
- Integration between routes and application services.

Use small fixtures instead of relying on the entire production dataset in routine tests.

## Deliverables

- Working FastAPI application.
- Documented API contracts.
- Health and readiness endpoints.
- Core analytics endpoints.
- API integration tests.

## Completion criteria

The application starts, valid requests return the expected schema, invalid requests fail predictably, and core business logic is not embedded in route functions.

---

# 10. Phase 7 — Machine Learning

## Objective

Develop models that solve a defined problem and demonstrate measurable value.

**Do not start ML until data quality and core analytics are reliable.**

Machine learning is a later milestone. The API can have a useful first release without it.

## 10.1 Define the problem and baseline

For each model, document:

- The business question.
- The target or clustering objective.
- Available input features.
- Prediction time and horizon, if applicable.
- Evaluation metrics.
- A simple baseline.
- The minimum result that would justify using the model.

Do not train a model simply to have a model in the project.

## 10.2 `ml/preprocessing.py`

Responsibilities:

- Handle missing values.
- Transform numeric features.
- Encode categorical features when needed.
- Scale features when required.
- Keep preprocessing consistent between training and inference.
- Prevent information from the validation or test data leaking into training.

## 10.3 `ml/feature_engineering.py`

Responsibilities:

- Create meaningful features from transaction data.
- Define feature names and data types.
- Record the observation window.
- Ensure every feature uses information available at prediction time.
- Keep feature generation reproducible.

## 10.4 Customer segmentation

File: `ml/customer_segmentation.py`

Tasks:

1. Build customer-level features.
2. Investigate skewed distributions and missing values.
3. Select an appropriate clustering approach.
4. Scale features when appropriate.
5. Compare candidate approaches with a reasonable baseline.
6. Evaluate cluster quality and stability.
7. Profile the resulting segments.
8. Assess whether the segments are interpretable and useful.
9. Document limitations.

Possible methods include K-means or other clustering approaches when justified by the feature structure.

Clustering does not automatically provide ground-truth customer categories. Treat cluster IDs as model outputs, not objective labels.

## 10.5 Demand forecasting

File: `ml/demand_forecasting.py`

Tasks:

1. Define what is being forecast: daily sales, total quantity, product demand, or another target.
2. Choose the forecast granularity.
3. Examine missing periods and historical coverage.
4. Establish a simple baseline.
5. Split the data chronologically.
6. Train candidate models.
7. Evaluate predictions over an appropriate forecast horizon.
8. Compare results with the baseline.
9. Document sparse products and limitations.
10. Decide whether the model is useful enough to release.

Never randomly split time-series observations in a way that allows future information to leak into training.

If the dataset does not support reliable product-level forecasting, reduce the scope or document that limitation.

## 10.6 Model evaluation

File: `ml/model_evaluation.py`

Responsibilities:

- Calculate appropriate evaluation metrics.
- Compare candidate models with baselines.
- Produce reproducible evaluation reports.
- Document the evaluation data and assumptions.

Select metrics according to the problem. For forecasting, possible metrics include MAE or RMSE; percentage-based metrics require care when actual values can be zero or close to zero.

## 10.7 Model artifacts and loading

Potential modules:

- `ml/model_registry.py`
- `infrastructure/model_loader.py`

Responsibilities:

- Identify model versions.
- Store relevant model metadata.
- Load the expected model artifact.
- Validate required features and schema.
- Make inference reproducible.

Record the model version, feature schema, training assumptions, dependency versions, and evaluation results.

Do not load untrusted serialized model files such as arbitrary pickle or joblib artifacts.

## 10.8 ML notebooks

Use:

- `09_feature_engineering_experiments.ipynb`
- `10_customer_clustering_experiments.ipynb`
- `11_demand_forecasting_experiments.ipynb`
- `12_model_evaluation_and_comparison.ipynb`

Use notebooks for experiments, then move successful reusable logic into the tested package.

## Deliverables

- Reusable preprocessing and feature engineering.
- Customer segmentation, if justified.
- Demand forecasting, if supported.
- Evaluation reports.
- Versioned model artifacts.
- Tests for inference and schema validation.

## Completion criteria

Models have reproducible evaluation, compare favorably with a meaningful baseline, avoid leakage, and have documented limitations.

---

# 11. Phase 8 — Connect Application Services and Infrastructure

## Objective

Keep business behavior separate from HTTP handling and external resources.

Follow these boundaries:

- **Domain:** core business concepts and rules.
- **Application:** use cases and orchestration.
- **Analytics:** deterministic analytical calculations.
- **ML:** model preparation, evaluation, and inference.
- **Infrastructure:** files, repositories, model loading, configuration, and logging.
- **API:** HTTP routing, request validation, and response formatting.

Do not introduce abstractions solely to make the architecture look sophisticated. Add classes and interfaces when they clarify a real responsibility or improve testing.

## Completion criteria

Core analytics and use cases can be tested without starting the HTTP server, and data-access details do not leak into every module.

---

# 12. Phase 9 — Logging and Operational Readiness

## Objective

Make the service diagnosable and safer to operate.

Implement `infrastructure/logging_config.py` and define configuration behavior.

Tasks:

- [ ] Configure consistent log levels.
- [ ] Record startup and shutdown events.
- [ ] Record data-loading and model-loading failures.
- [ ] Record unexpected request failures without leaking sensitive information.
- [ ] Validate required configuration at startup.
- [ ] Make data and model paths configurable.
- [ ] Define what happens when data or models are unavailable.
- [ ] Keep health checks lightweight.
- [ ] Document how to inspect logs.

Do not log secrets, full customer records, or sensitive request bodies unnecessarily.

## Completion criteria

Common failures can be diagnosed, configuration problems are clear, and logs do not unnecessarily expose private information.

---

# 13. Phase 10 — Testing and Code Quality

## Objective

Make correctness a routine part of development.

## 13.1 Unit tests

Test individual functions and modules:

- Data validation.
- Cleaning rules.
- Sales calculations.
- Customer calculations.
- Product calculations.
- RFM calculations.
- Cohort calculations.
- Market-basket calculations.
- Feature engineering.
- Model evaluation.

## 13.2 Integration tests

Test interactions between:

- Data loader and analytics.
- Application services and repositories.
- FastAPI routes and application services.
- Model loading and inference.

## 13.3 End-to-end tests

Where useful, start the packaged application and test representative endpoints through the same interface a client would use.

## 13.4 Code-quality checks

Use Ruff for linting and formatting checks, and pytest for automated tests.

Add other checks only when useful, such as static typing or dependency vulnerability scanning.

Keep tests deterministic. Avoid dependence on network access, uncontrolled current time, or large external files unless the test specifically requires those conditions.

## Completion criteria

A clean checkout can run the documented checks, and failures are reproducible and actionable.

---

# 14. Phase 11 — Docker Packaging

## Objective

Package the API so it runs consistently outside the development environment.

## Tasks

1. Create the Dockerfile in the agreed location.
2. Use an appropriate Python base image.
3. Install only the dependencies required at runtime.
4. Configure the application to listen on the container network interface.
5. Run as a non-root user where practical.
6. Add `.dockerignore`.
7. Keep secrets and large local datasets out of the image.
8. Define how runtime configuration is supplied.
9. Define how data and model artifacts are made available.
10. Build the image locally.
11. Run the container.
12. Test health and analytics endpoints.
13. Document the process.

Do not bake credentials into image layers. Do not assume the container filesystem provides durable storage for data or models.

## Completion criteria

Another developer can build and run the container by following the documentation, without manually modifying the image.

---

# 15. Phase 12 — GitHub Actions CI/CD

## Objective

Automate quality checks and make releases reproducible.

## 15.1 Continuous integration

File: `.github/workflows/ci.yml`

The workflow should:

1. Check out the repository.
2. Set up the selected Python version.
3. Install dependencies.
4. Run Ruff lint checks.
5. Run Ruff formatting checks.
6. Run pytest.
7. Optionally verify package building or container building.

Use small, non-sensitive fixtures. CI should not depend on manually downloaded private files or production credentials.

## 15.2 Continuous deployment

File: `.github/workflows/cd.yml`

Add deployment automation only after a manual deployment has been tested.

Tasks:

- Define a release trigger.
- Build a versioned artifact or container image.
- Store credentials in GitHub's secret-management settings.
- Restrict workflow permissions.
- Deploy to the intended environment.
- Run a post-deployment health check.
- Document rollback steps.

Do not store deployment secrets in the repository or automatically deploy every change to production without appropriate safeguards.

## Completion criteria

Pull requests receive automated feedback, releases are identifiable by version, and deployments do not require secrets in source control.

---

# 16. Phase 13 — AWS EC2 Deployment

## Objective

Deploy the containerized API to a controlled server and make it maintainable.

## 16.1 Pre-deployment checks

- [ ] Tests and lint checks pass.
- [ ] Docker build succeeds.
- [ ] The container runs locally.
- [ ] Health endpoints work.
- [ ] Runtime configuration is documented.
- [ ] Required data and model artifacts are available.
- [ ] No secrets are committed.
- [ ] A rollback procedure exists.

## 16.2 Deployment steps

1. Select an EC2 instance suitable for the workload.
2. Select and update a supported operating system.
3. Configure a security group with only the required ports.
4. Restrict administrative access to trusted sources or use a managed access method.
5. Install Docker using current official instructions for the selected operating system.
6. Pull or transfer the versioned container image.
7. Supply runtime configuration securely.
8. Start the container with a suitable restart policy.
9. Check the application health endpoints.
10. Test a representative analytics request.
11. Configure HTTPS through an appropriate reverse proxy or managed TLS/load-balancing solution before public production use.
12. Configure logs and basic monitoring.
13. Document how to deploy an update.
14. Test the rollback procedure.
15. Review costs, storage, access permissions, backups, and patching.

Exact deployment commands depend on the operating system and hosting design. Verify the commands against current official AWS and Docker documentation.

Do not expose internal service ports to the entire internet. Do not use development server settings as a substitute for a production deployment plan.

## Completion criteria

The service is accessible through its intended secure route, health checks pass, logs can be inspected, and deployment and rollback procedures are documented and tested.

---

# 17. Phase 14 — Documentation and Final Release

## Objective

Make the project understandable and maintainable by someone who did not build it.

## 17.1 README requirements

The README should include:

- Project purpose and current feature status.
- Architecture overview.
- Dataset source and usage terms.
- Data limitations.
- Environment setup.
- Configuration variables.
- Commands for running tests and lint checks.
- Instructions for starting the API.
- Endpoint descriptions and example requests.
- Docker usage.
- Model training and evaluation instructions, if applicable.
- Deployment overview.
- Known limitations.
- Future work.

## 17.2 Supporting documents

Recommended files:

| File | Purpose |
|---|---|
| `docs/architecture.md` | Module responsibilities and system data flow |
| `docs/data_dictionary.md` | Dataset columns, types, and meanings |
| `docs/metric_definitions.md` | Revenue, returns, retention, and other metric definitions |
| `docs/model_card.md` | Model purpose, evaluation, version, and limitations |
| `docs/deployment.md` | Deployment, configuration, monitoring, and rollback |
| `docs/implementation-guide.md` | This implementation roadmap |

Keep documentation aligned with actual behavior. Label examples as planned if the corresponding endpoint or feature does not yet exist.

## 17.3 Final release checklist

- [ ] Fresh environment setup works.
- [ ] Dataset source and terms are documented.
- [ ] Data-loading behavior is tested.
- [ ] Cleaning rules are explicit and tested.
- [ ] Core metrics are documented and tested.
- [ ] Advanced analytics are tested where implemented.
- [ ] API schemas and error responses are documented.
- [ ] API integration tests pass.
- [ ] Models, if included, have honest baseline comparisons.
- [ ] Ruff checks pass.
- [ ] pytest passes.
- [ ] CI passes.
- [ ] Docker build and smoke test pass.
- [ ] Configuration and secrets are handled safely.
- [ ] Deployment and rollback are documented.
- [ ] README feature status is accurate.
- [ ] A versioned release is created.

## Completion criteria

A new developer can set up, test, run, understand, and deploy the project using the documentation.

---

# 18. Notebook Implementation Plan

Keep notebooks focused on exploration and experiments.

| Notebook | Purpose | Expected output |
|---|---|---|
| `01_data_overview.ipynb` | Understand the dataset | Data overview |
| `02_data_quality_and_cleaning.ipynb` | Investigate data issues | Quality report and cleaning policy |
| `03_exploratory_data_analysis.ipynb` | Explore distributions and patterns | EDA findings |
| `04_sales_and_revenue_analysis.ipynb` | Investigate sales metrics | Sales report |
| `05_customer_behavior_analysis.ipynb` | Understand customer behavior | Customer insights |
| `06_rfm_customer_segmentation.ipynb` | Explore RFM features and segments | RFM analysis |
| `07_cohort_and_retention_analysis.ipynb` | Measure cohort behavior | Retention analysis |
| `08_product_and_market_basket_analysis.ipynb` | Analyze products and baskets | Product and association insights |
| `09_feature_engineering_experiments.ipynb` | Test ML features | Feature decisions |
| `10_customer_clustering_experiments.ipynb` | Compare segmentation methods | Cluster evaluation |
| `11_demand_forecasting_experiments.ipynb` | Evaluate forecasting baselines | Forecast evaluation |
| `12_model_evaluation_and_comparison.ipynb` | Compare candidate models | Model selection report |

Restart and run notebooks from top to bottom before relying on their results. Do not depend on variables left over from previous interactive sessions.

---

# 19. Recommended Milestones

Use these milestones to track progress.

## Milestone A — Repository ready

- Environment and dependencies are configured.
- Git is initialized.
- Tests and linting are configured.

## Milestone B — Data understood

- Dataset is obtained.
- Data overview is complete.
- Data dictionary exists.
- Data-quality decisions are documented.

## Milestone C — Data foundation reliable

- Loader is implemented.
- Quality checks are implemented.
- Cleaning policy is documented.
- Fixtures and tests pass.

## Milestone D — Core analytics reliable

- Sales metrics are implemented and tested.
- Customer metrics are implemented and tested.
- Product metrics are implemented and tested.

## Milestone E — Advanced analysis complete

- RFM analysis is implemented and tested.
- Cohort analysis is implemented and tested.
- Market-basket analysis is implemented if the data supports it.

## Milestone F — First API release

- FastAPI app starts.
- Health checks work.
- Initial analytics endpoints work.
- API tests pass.

**This is a valid first release.** You do not need to wait for machine learning to deliver a useful API.

## Milestone G — ML validated

- Baselines are defined.
- Feature engineering is reproducible.
- Leakage is avoided.
- Evaluation is documented.
- Model artifacts and inference are tested.

## Milestone H — Production readiness

- Logging and configuration are reliable.
- Integration tests pass.
- Security requirements are reviewed.

## Milestone I — Docker and CI

- Docker image builds and runs.
- CI executes quality checks.
- Build and smoke tests pass.

## Milestone J — Deployment

- Service is deployed to EC2.
- Health checks pass.
- Logs and basic monitoring are available.
- Rollback steps are documented.

## Milestone K — Final release

- Documentation is complete.
- Known limitations are documented.
- Release is versioned.

---

# 20. Daily Development Workflow

For each task:

1. Select one small outcome.
2. Read the relevant module and its expected contract.
3. Implement the smallest complete behavior.
4. Write or update tests.
5. Run focused tests.
6. Run the relevant full checks.
7. Review the Git diff.
8. Check for secrets, datasets, generated files, and unrelated changes.
9. Update documentation if behavior or assumptions changed.
10. Commit the changes.
11. Record the next task and any unresolved questions.

Prefer a complete vertical slice over several unfinished layers.

For example:

1. Define one sales metric.
2. Implement the analytical function.
3. Verify it with a unit test.
4. Add an application service.
5. Expose it through an API route.
6. Add an integration test.
7. Document the endpoint.

---

# 21. Common Mistakes to Avoid

## Starting machine learning too early

Reliable data and business metrics are prerequisites for meaningful models.

## Cleaning data without understanding it

Negative quantities, duplicates, cancellations, and missing identifiers may carry business meaning.

## Keeping all production logic in notebooks

Move stable calculations into tested Python modules.

## Data leakage in forecasting

Use chronological evaluation and ensure training features only contain information available at prediction time.

## Reloading data on every request

Design the data lifecycle and resource initialization deliberately.

## Returning raw DataFrames from API routes

Define stable response schemas and convert internal data to those schemas.

## Overengineering before the first release

Build a small, tested, useful system before adding abstractions and optional features.

## Committing sensitive or large files

Check ignore rules and repository contents before committing.

## Deploying without a recovery plan

Test the container, health checks, logs, and rollback procedure before production use.

## Claiming unverified results

Document actual test results, model performance, limitations, and implemented features honestly.

---

# 22. Your First Week: Practical Starting Plan

Use this as an example schedule. Adjust it to your experience and available time.

## Step 1 — Understand the repository

- Read the README.
- Review the folder structure.
- Mark planned versus implemented features.
- Confirm the project's Python version.

## Step 2 — Set up the environment

- Create the virtual environment.
- Install the selected dependencies.
- Configure pytest and Ruff.
- Verify the basic checks.

## Step 3 — Obtain and inspect the data

- Confirm the source and terms.
- Place the original data under `data/raw/`.
- Run `01_data_overview.ipynb`.
- Record columns, row count, data types, and date range.

## Step 4 — Investigate quality

- Run `02_data_quality_and_cleaning.ipynb`.
- Investigate missing IDs, duplicates, returns, and invalid values.
- Record cleaning decisions before implementing them.

## Step 5 — Explore the business questions

- Run `03_exploratory_data_analysis.ipynb`.
- Identify the first few useful metrics.
- Document limitations and questions.

## Step 6 — Implement the first data pipeline

- Implement `infrastructure/data_loader.py`.
- Implement `analytics/data_quality.py`.
- Create a small test fixture.
- Write unit tests.
- Run the tests and inspect the results.

## Step 7 — Build one complete analytical feature

- Implement one sales metric.
- Verify it manually against a small fixture.
- Add a unit test.
- Document its business definition.

**Do not start by implementing every file in the project tree.** Start with one reliable path from raw data to a tested result.

---

# 23. Final Definition of Success

The project is complete when:

- A new developer can set it up using the documentation.
- The data source and data limitations are understood.
- Data preparation is repeatable and tested.
- Business metrics have explicit definitions.
- Advanced analyses are reproducible.
- The API has stable contracts and predictable error handling.
- Machine-learning features, if included, have been evaluated honestly.
- Automated quality checks pass.
- The container builds and runs.
- A versioned release can be deployed securely.
- Logs and health checks support basic operations.
- Deployment and rollback procedures are documented.
- The README accurately describes the current state of the project.

**The goal is not to create the largest number of files, notebooks, endpoints, or models. The goal is to deliver a correct, maintainable, tested, explainable, and deployable retail analytics service.**
