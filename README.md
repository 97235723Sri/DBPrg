Files at a glance
FilePurpose
pom.xml       Spring Boot 3.2 + Sybase jConnect + MSSQL JDBC + HikariCP
application.yml    Both DataSource configs, timeouts, thread pool size
queries.sql 100 Sybase IQ queries covering everything: window functions, CTEs, aggregates, date functions, 
        string ops, DECODE, LIST, NVL, etc.
DatabaseConfig.java  Two independent HikariCP pools — one per DB, both wired as separate 
JdbcTemplate beansSqlDialectConverterService.java30+ regex rewrite rules: NVL→ISNULL, LIST→STRING_AGG, ||→+, NOW()→GETDATE(), DATEFORMAT→FORMAT, MOD→%, TRIM→LTRIM(RTRIM()), DECODE→CASE WHEN, FETCH FIRST→TOP, and moreQueryExecutorService.javaExecutes SQL with timeout, normalises types (numeric tolerance, timestamp formatting), captures errors gracefullyResultComparatorService.java4-step comparison: error → schema → row count → cell-level diff with 1e-6 numeric toleranceMigrationOrchestrationService.javaLoads queries, runs all 100 pairs with ExecutorService thread pool, collects resultsHtmlReportGeneratorService.javaSelf-contained dark-theme HTML report — summary cards, search/filter bar, expandable per-query panels with side-by-side SQL and colour-coded cell diff tableMigrationController.javaPOST /api/migration/run (async), GET /api/migration/status, GET /api/migration/run/syncMigrationRunner.java--migration.auto-run=true for one-shot batch CI modesample-report.htmlRendered example — open it in a browser to see the exact UI
