Here's a professional package documentation (README) for your Pesapal PHP SDK:

```markdown
# Pesapal PHP SDK

[![Latest Version](https://img.shields.io/packagist/v/emleons/pesapal-php.svg?style=flat-square)](https://packagist.org/packages/emleons/pesapal-php)
[![License](https://img.shields.io/badge/license-MIT-blue.svg?style=flat-square)](LICENSE.md)
[![PHP Version](https://img.shields.io/packagist/php-v/emleons/pesapal-php.svg?style=flat-square)](https://php.net)

A simple unofficial PHP SDK for integration with the Pesapal API (v3). This package provides a class for all major Pesapal operations.

## Features

- ✅ **Complete API Coverage**: Supports all essential Pesapal v3 endpoints
- 🔐 **Secure Authentication**: Handles token generation automatically
- 🧪 **Sandbox Ready**: Built-in support for testing environments
- 🚀 **Simple Interface**: Intuitive methods for common operations
- 💡 **Type Safety**: PHP 7.4+ type hints for better code reliability
- 📦 **PSR Compliant**: Follows PHP standards for easy integration

## Installation

Install via Composer:

```bash
composer require emleons/pesapal-php
```

## Quick Start

```php
<?php

require 'vendor/autoload.php';

use Emleons\PesapalPhp\Pesa;

// Initialize the SDK
$pesa = new Pesa([
    'consumer_key'    => 'your_consumer_key',
    'consumer_secret' => 'your_consumer_secret',
    'is_sandbox'      => true, // Set false for production
]);

// Example: Submit a payment
try {
    $orderDetails = [
        "id" => uniqid(),
        "currency" => "KES",
        "amount" => 1500.00,
        "description" => "Online Store Purchase",
        "callback_url" => "https://yourdomain.com/callback",
        "notification_id" => "your_ipn_id",
        "billing_address" => [
            "email_address" => "customer@example.com",
            "phone_number" => "254712345678",
            "country_code" => "KE",
            "first_name" => "John",
            "last_name" => "Doe"
        ]
    ];

    $response = $pesa->makeThePayment($orderDetails);
    print_r($response);
    
} catch (\Exception $e) {
    echo "Error: " . $e->getMessage();
}
```

## API Reference

### Configuration Options

| Parameter         | Type   | Required | Default | Description                          |
|-------------------|--------|----------|---------|--------------------------------------|
| `consumer_key`    | string | Yes      | -       | Your Pesapal API consumer key        |
| `consumer_secret` | string | Yes      | -       | Your Pesapal API consumer secret     |
| `is_sandbox`      | bool   | No       | true    | Set to false for production environment |

### Core Methods

#### Authentication
- `getToken()` - Retrieves authentication token (automatically used by other methods)

#### IPN Management
- `registerIpnUrl(string $ipnUrl, string $notificationType)` - Register a new IPN URL
- `getRegisteredIpnUrl()` - Retrieve currently registered IPN URL

#### Payments
- `makeThePayment(array $orderDetails)` - Submit a new payment order
- `getTransactionStatus(string $orderTrackingId)` - Check payment status

#### Order Management
- `cancelOrderRequest(string $orderTrackingId)` - Cancel an existing order

#### Refunds
- `sendRefundRequest(array $refundDetails)` - Initiate a refund

## Error Handling

All methods throw exceptions for error conditions. Always wrap calls in try-catch blocks:

```php
try {
    $response = $pesa->makeThePayment($orderDetails);
} catch (\InvalidArgumentException $e) {
    // Invalid parameters
} catch (\GuzzleHttp\Exception\GuzzleException $e) {
    // Network/API errors
} catch (\Exception $e) {
    // Other errors
}
```

## Testing

For sandbox testing, set `is_sandbox` to true and use test credentials from Pesapal.

## Requirements

- PHP 7.4 or higher
- GuzzleHTTP (automatically installed via Composer)
- Pesapal API credentials

## Security

Always:
- Keep your consumer secret secure
- Validate all user inputs before passing to the SDK
- Use HTTPS for all callbacks and IPN URLs
- Store sensitive data securely

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss proposed changes.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

**Disclaimer**: This is an unofficial SDK and is not affiliated with or endorsed by Pesapal Limited.
```# pesapal-php
