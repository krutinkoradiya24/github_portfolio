<?php
// index.php  (form + handler in same file)
// Run this on a PHP-enabled server (XAMPP/WAMP/MAMP/LAMP or hosting that supports PHP).

// Simple helper
function h($s){ return htmlspecialchars($s, ENT_QUOTES|ENT_SUBSTITUTE, 'UTF-8'); }

$message = '';
if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    // Basic sanitization and minimal validation
    $customerName  = trim($_POST['customerName'] ?? '');
    $customerPhone = trim($_POST['customerPhone'] ?? '');
    $notes         = trim($_POST['notes'] ?? '');

    $itemNames  = $_POST['itemName']  ?? array();
    $itemQtys   = $_POST['itemQty']   ?? array();
    $itemPrices = $_POST['itemPrice'] ?? array();

    if ($customerName === '' || $customerPhone === '') {
        $message = '<div class="error">Customer name and phone are required.</div>';
    } else {
        $lines = [];
        $grandTotal = 0.0;
        for ($i = 0; $i < count($itemNames); $i++) {
            $iname = trim(strip_tags($itemNames[$i] ?? ''));
            $iqty  = floatval($itemQtys[$i] ?? 0);
            $iprice= floatval($itemPrices[$i] ?? 0);
            if ($iname === '' || $iqty <= 0) continue;
            $lineTotal = $iqty * $iprice;
            $grandTotal += $lineTotal;
            $lines[] = ['name'=>$iname,'qty'=>$iqty,'price'=>$iprice,'lineTotal'=>$lineTotal];
        }

        if (count($lines) === 0) {
            $message = '<div class="error">No valid items provided.</div>';
        } else {
            // save CSV in same folder (ensure webserver has write permission)
            $csv_file = __DIR__ . '/orders.csv';
            $timestamp = date('Y-m-d H:i:s');
            $items_json = json_encode($lines, JSON_UNESCAPED_UNICODE);
            $csv_row = [$timestamp, $customerName, $customerPhone, number_format($grandTotal,2), $items_json, $notes];
            if ($fp = @fopen($csv_file, 'a')) {
                fputcsv($fp, $csv_row);
                fclose($fp);
            }

            // TODO: configure these for your SMTP / or remove mail if not configured
            // For local testing without SMTP you can skip sending email.
            $to_email = 'krutinkoradiya24@gamil.com'; // your target
            // Build simple HTML body
            $body = "<h2>New Order</h2><p><strong>Customer:</strong> " . h($customerName) . "<br>";
            $body .= "<strong>Phone:</strong> " . h($customerPhone) . "</p>";
            $body .= "<table border='1' cellpadding='6'><tr><th>Item</th><th>Qty</th><th>Unit</th><th>Line</th></tr>";
            foreach ($lines as $ln) {
                $body .= "<tr><td>" . h($ln['name']) . "</td><td style='text-align:right'>" . h(number_format($ln['qty'],0)) . "</td><td style='text-align:right'>" . h(number_format($ln['price'],2)) . "</td><td style='text-align:right'>" . h(number_format($ln['lineTotal'],2)) . "</td></tr>";
            }
            $body .= "</table><p><strong>Grand total: ₹ " . number_format($grandTotal,2) . "</strong></p>";

            // If you have PHPMailer + SMTP configured, you can integrate sending here.
            // For now just show success:
            $message = "<div class='success'>Order saved. Grand total: ₹ " . number_format($grandTotal,2) . "</div>";
        }
    }
}
?>
<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>GANESH MARKETING — Place Order</title>
<style>
/* (keep your CSS from before, shortened for brevity) */
:root{font-family:system-ui,-apple-system,Segoe UI,Roboto,"Helvetica Neue",Arial;--accent:#0b5ed7}
body{margin:0;background:#f3f6fb;color:#111;padding:18px}
.container{max-width:980px;margin:20px auto;background:#fff;padding:18px;border-radius:12px;box-shadow:0 6px 18px rgba(10,20,40,0.05)}
label{display:block;margin:8px 0 6px;font-weight:600}
input[type="text"], input[type="number"], textarea{width:100%;padding:9px;border:1px solid #e0e4ea;border-radius:8px;font-size:0.95rem}
.small{width:120px}
.btn{background:var(--accent);color:#fff;padding:10px 14px;border-radius:10px;border:0;font-weight:700;cursor:pointer}
.linklike{background:none;border:0;color:var(--accent);text-decoration:underline;cursor:pointer;padding:6px}
.success{background:#e8fff0;border:1px solid #c6efdb;color:#0a6b3f;padding:12px;border-radius:8px}
.error{background:#fff0f0;border:1px solid #f1c6c6;color:#8a2b2b;padding:12px;border-radius:8px}
</style>
</head>
<body>
<div class="container">
  <h1>GANESH MARKETING — Place Order</h1>
  <?php if ($message) echo $message; ?>
  <form id="orderForm" method="post" action="">
    <label for="customerName">Customer name *</label>
    <input id="customerName" name="customerName" type="text" required placeholder="Customer full name" value="<?php echo isset($_POST['customerName']) ? h($_POST['customerName']) : ''; ?>" />

    <label for="customerPhone">Customer phone *</label>
    <input id="customerPhone" name="customerPhone" type="text" required placeholder="7777777777" value="<?php echo isset($_POST['customerPhone']) ? h($_POST['customerPhone']) : ''; ?>" />

    <label for="notes">Notes (optional)</label>
    <textarea id="notes" name="notes" placeholder="Delivery instructions..."><?php echo isset($_POST['notes']) ? h($_POST['notes']) : ''; ?></textarea>

    <h3>Items</h3>
    <table id="itemsTable">
      <thead><tr><th>Item</th><th>Qty</th><th>Price</th><th></th></tr></thead>
      <tbody id="itemsBody">
        <tr>
          <td><input name="itemName[]" type="text" required placeholder="e.g. Engine Oil SAE 20W-50" /></td>
          <td><input name="itemQty[]" type="number" min="1" step="1" required value="1" class="small" /></td>
          <td><input name="itemPrice[]" type="number" min="0" step="0.01" required value="0.00" class="small" /></td>
          <td><button type="button" class="removeBtn linklike">Remove</button></td>
        </tr>
      </tbody>
    </table>
    <div style="margin-top:10px">
      <button type="button" id="addRow" class="btn">+ Add item</button>
    </div>

    <div style="margin-top:14px">
      <button type="submit" class="btn">Send Order</button>
    </div>
  </form>
</div>

<script>
(function(){
  const itemsBody = document.getElementById('itemsBody');
  document.getElementById('addRow').addEventListener('click', () => {
    const tr = document.createElement('tr');
    tr.innerHTML = `<td><input name="itemName[]" type="text" required placeholder="Item name" /></td>
      <td><input name="itemQty[]" type="number" min="1" step="1" required value="1" class="small" /></td>
      <td><input name="itemPrice[]" type="number" min="0" step="0.01" required value="0.00" class="small" /></td>
      <td><button type="button" class="removeBtn linklike">Remove</button></td>`;
    itemsBody.appendChild(tr);
    tr.querySelector('.removeBtn').addEventListener('click', () => tr.remove());
  });
  document.querySelectorAll('.removeBtn').forEach(btn => btn.addEventListener('click', e => e.target.closest('tr').remove()));
})();
</script>
</body>
</html>
