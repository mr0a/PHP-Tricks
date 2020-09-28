```php
// the list of allowed field names
$allowed = ["name","surname","email"];

// initialize an array with values:
$params = [];

// initialize a string with `fieldname` = :placeholder pairs
$setStr = "";

// loop over source data array
foreach ($allowed as $key)
{
    if (isset($_POST[$key]) && $key != "id")
    {
        $setStr .= "`$key` = :$key,";
        $params[$key] = $_POST[$key];
    }
}
$setStr = rtrim($setStr, ",");

$params['id'] = $_POST['id'];
$pdo->prepare("UPDATE users SET $setStr WHERE id = :id")->execute($params);
```
