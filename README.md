<h1 align="center">DotEnv</h1>

```php
# Create file .env

# Load Environment vars from file on root
DotEnv\Environment::load(__DIR__);

# Get Environment var
echo getenv('DB_HOST');

```



<h1 align="center">DatabaseManager</h1>

```php
# Start doc
use DatabaseManager\Database;

# Database credentials
$dbHost = 'localhost';
$dbName = 'database';
$dbUser = 'root';
$dbPass = 'pass';
$dbPort = 3306;

# Config database class
Database::config($dbHost,$dbName,$dbUser,$dbPass,$dbPort);

# Table instance
$obDatabase = new Database('table_name');

# SELECT (return a PDOStatement object)
$results = $obDatabase->select('id > 10','name ASC','1','*');

# INSERT (return inserted id)
$id = $obDatabase->insert([
  'name' => 'Lucas Giovanni'
]);

# UPDATE (return a bool)
$success = $obDatabase->update('id = 1',[
  'name' => 'Lucas Giovanni2'
]);

# DELETE (return a bool)
$success = $obDatabase->delete('id = 1');

```



<h1 align="center">Pagination</h1>

```php
# Start doc
use DatabaseManager\Database;
use DatabaseManager\Pagination;

# Count total results
$totalResults = $obDatabase->select('id > 10',null,null,'COUNT(*) as total')->fetchObject()->total;

# Current page
$currentPage  = $_GET['page'] ?? 1;
$itemsPerPage = 10;

# Pagination
$obPagination = new Pagination($totalResults,$currentPage,$itemsPerPage);

# SELECT (return a PDOStatement object)
$results = $obDatabase->select('id > 10',null,$obPagination->getLimit());

# PAGES (array)
$pages = $obPagination->getPages();

```
