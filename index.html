<?php
ini_set('display_errors', 1);
error_reporting(E_ALL);

function logline($t) {
    echo "<div class='line'>$t</div>";
}

$run = ($_SERVER['REQUEST_METHOD'] === 'POST');
?>
<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<title>Telegram Diagnostic Tool</title>
<style>
    body {
        font-family: Consolas, monospace;
        background: #f0f2f5;
        padding: 30px;
    }
    h2 {
        margin-bottom: 20px;
    }
    .btn {
        padding: 12px 25px;
        font-size: 16px;
        background: #0078ff;
        color: #fff;
        border: none;
        border-radius: 6px;
        cursor: pointer;
        margin-bottom: 20px;
    }
    .btn:hover {
        background: #005fcc;
    }
    .logbox {
        background: #fff;
        padding: 20px;
        border-radius: 8px;
        border: 1px solid #ccc;
        white-space: pre-wrap;
    }
    .line {
        margin-bottom: 6px;
    }
</style>
</head>
<body>

<h2>Проверка соединения с Telegram API</h2>

<form method="post">
    <button class="btn" type="submit">Запустить тест</button>
</form>

<?php if ($run): ?>
<div class="logbox">
<?php
echo "<pre>";

logline("=== TELEGRAM CONNECTION TEST ===\n");

logline("=== DNS CHECK ===");
$dns = dns_get_record("api.telegram.org", DNS_A);
if ($dns) {
    logline("DNS OK:");
    print_r($dns);
} else {
    logline("❌ DNS FAILED");
}

logline("\n=== IP CONNECTIVITY TEST ===");
$ip = $dns[0]['ip'] ?? null;

if ($ip) {
    $start = microtime(true);
    $fp = @fsockopen($ip, 443, $errno, $errstr, 5);
    $time = round((microtime(true) - $start) * 1000);

    if ($fp) {
        logline("✔ TCP OK ($time ms)");
        fclose($fp);
    } else {
        logline("❌ TCP FAIL ($errno: $errstr)");
    }
}

logline("\n=== SSL CERTIFICATE CHECK ===");

$start = microtime(true);
$stream = @stream_socket_client(
    "ssl://api.telegram.org:443",
    $errno, $errstr, 5,
    STREAM_CLIENT_CONNECT,
    stream_context_create(["ssl" => ["capture_peer_cert" => true]])
);
$time = round((microtime(true) - $start) * 1000);

if (!$stream) {
    logline("❌ SSL FAILED ($errstr) [$errno] ($time ms)");
} else {
    logline("✔ SSL OK ($time ms)");
}

logline("\n=== cURL HTTPS TEST ===");

$ch = curl_init("https://api.telegram.org");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_TIMEOUT, 10);

$start = microtime(true);
$response = curl_exec($ch);
$time = round((microtime(true) - $start) * 1000);

if (curl_errno($ch)) {
    logline("❌ cURL ERROR: " . curl_error($ch) . " ($time ms)");
} else {
    logline("✔ cURL OK ($time ms)");
    logline("Response length: " . strlen($response));
}

$http_code = curl_getinfo($ch, CURLINFO_HTTP_CODE);
logline("HTTP CODE: $http_code");

curl_close($ch);

logline("\n=== file_get_contents HTTPS TEST ===");

$start = microtime(true);
$result = @file_get_contents("https://api.telegram.org");
$time = round((microtime(true) - $start) * 1000);

if ($result === false) {
    logline("❌ file_get_contents ERROR ($time ms)");
    print_r(error_get_last());
} else {
    logline("✔ file_get_contents OK ($time ms)");
    logline("Response length: " . strlen($result));
}

logline("\n=== BLOCK DETECTION ===");

if ($http_code == 0) {
    logline("❌ Сервер НЕ МОЖЕТ установить HTTPS‑соединение с Telegram");
} elseif ($http_code == 200) {
    logline("✔ Telegram API доступен");
} else {
    logline("⚠ Необычный статус: $http_code");
}

echo "</pre>";
?>
</div>
<?php endif; ?>

</body>
</html>
