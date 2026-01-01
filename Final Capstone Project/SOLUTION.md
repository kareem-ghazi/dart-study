# Solution: Real-Time Stock Trading Engine

```dart
import 'dart:async';
import 'dart:collection';
import 'dart:math';
import 'dart:isolate';

// ==========================================
// 1. Core Data Models & Typing
// ==========================================

// -- Extension Types (Topic 26) --
// Wraps double to ensure type safety for money.
extension type Money(double amount) {
  // Operator overloading (Topic 20)
  Money operator +(Money other) => Money(amount + other.amount);
  Money operator -(Money other) => Money(amount - other.amount);
  bool operator <(Money other) => amount < other.amount;
  bool operator >(Money other) => amount > other.amount;
  
  @override
  String toString() => '\$${amount.toStringAsFixed(2)}';
}

// -- Typedefs (Topic 8) --
typedef PriceUpdateCallback = void Function(String symbol, Money newPrice);

// -- Enums with Enhanced Features (Topic 23) --
enum OrderType {
  buy('Buying'),
  sell('Selling');

  final String actionName;
  const OrderType(this.actionName);
}

// -- Class Modifiers & Sealed Classes (Topic 28) --
sealed class TransactionResult {}

class Success extends TransactionResult {
  final Money executionPrice;
  final DateTime timestamp;
  Success(this.executionPrice, this.timestamp);
}

class Failure extends TransactionResult {
  final String reason;
  Failure(this.reason);
}

// -- Mixins (Topic 22) --
mixin Loggable {
  void log(String message) {
    final timestamp = DateTime.now().toIso8601String().split('T').last;
    print('[\$timestamp] [${this.runtimeType}] \$message');
  }
}

// -- Abstract Classes & Inheritance (Topic 18, 21) --
abstract class Asset {
  final String symbol;
  String name;
  
  Asset(this.symbol, this.name);
}

class Stock extends Asset {
  Money price;
  
  Stock(super.symbol, super.name, this.price);

  @override
  String toString() => '
$symbol ($name): $price';
}

// -- Generics & Collections (Topic 6, 7) --
class Portfolio<T extends Asset> with Loggable {
  final Map<String, T> _assets = {};
  final Map<String, int> _quantities = {};
  Money balance;

  Portfolio(this.balance);

  void addAsset(T asset, int quantity) {
    _assets[asset.symbol] = asset;
    _quantities[asset.symbol] = (_quantities[asset.symbol] ?? 0) + quantity;
  }

  void removeAsset(String symbol, int quantity) {
    if ((_quantities[symbol] ?? 0) < quantity) {
      throw Exception('Not enough shares to sell'); // Error Handling (Topic 14)
    }
    _quantities[symbol] = _quantities[symbol]! - quantity;
  }
  
  bool hasFunds(Money amount) => balance > amount || balance.amount == amount.amount; // Simple check
  
  void deduct(Money amount) => balance = balance - amount;
  void deposit(Money amount) => balance = balance + amount;
}

// -- Records (Topic 5) --
// Returns (Symbol, TotalValue)
(String, Money) calculateAssetValue(Stock stock, int qty) {
  return (stock.symbol, Money(stock.price.amount * qty));
}

// -- Callable Objects (Topic 27) --
class TradeExecutor with Loggable {
  // Callable method
  Future<TransactionResult> call(
      Portfolio<Stock> user, Stock stock, int quantity, OrderType type) async {
    
    log('Processing ${type.actionName} order for $quantity ${stock.symbol}...');
    
    // Simulate Network Delay (Topic 30)
    await Future.delayed(Duration(milliseconds: 500));

    try {
      if (type == OrderType.buy) {
        final cost = Money(stock.price.amount * quantity);
        if (!user.hasFunds(cost)) {
          return Failure('Insufficient funds. Required: $cost, Available: ${user.balance}');
        }
        user.deduct(cost);
        user.addAsset(stock, quantity);
        return Success(stock.price, DateTime.now());
      } else {
        // Sell logic could go here
        return Failure('Sell not implemented in this demo');
      }
    } catch (e) {
      return Failure(e.toString());
    }
  }
}

// ==========================================
// 2. Concurrency & Isolates (Topic 29, 31)
// ==========================================

// Static function for Isolate
double _calculateMovingAverage(List<double> prices) {
  if (prices.isEmpty) return 0.0;
  final sum = prices.reduce((a, b) => a + b);
  // Heavy computation simulation
  int count = 0;
  for(int i=0; i<10000000; i++) { count++; } 
  return sum / prices.length;
}

class MarketAnalyzer with Loggable {
  Future<void> analyzeMarketTrends() async {
    log('Starting heavy market analysis on background isolate...');
    
    // Generate large dataset
    final random = Random();
    final historicalPrices = List.generate(1000000, (_) => 100.0 + random.nextDouble() * 50);

    // Run on Isolate (Topic 31)
    final startTime = DateTime.now();
    final average = await Isolate.run(() => _calculateMovingAverage(historicalPrices));
    final endTime = DateTime.now();
    
    log('Analysis complete in ${endTime.difference(startTime).inMilliseconds}ms. Moving Average: ${average.toStringAsFixed(2)}');
  }
}

// ==========================================
// 3. The Market Stream (Topic 30)
// ==========================================

class StockMarket {
  final _controller = StreamController<Stock>.broadcast();
  final Random _random = Random();
  final Map<String, Stock> _listedStocks = {
    'AAPL': Stock('AAPL', 'Apple Inc.', Money(150.0)),
    'GOOG': Stock('GOOG', 'Alphabet Inc.', Money(2800.0)),
    'TSLA': Stock('TSLA', 'Tesla Inc.', Money(700.0)),
  };

  Stream<Stock> get priceUpdates => _controller.stream;

  Stock? getStock(String symbol) => _listedStocks[symbol];

  void openMarket() {
    print('🔔 Market is OPEN');
    // Simulate price ticks
    Timer.periodic(Duration(seconds: 1), (timer) {
      if (_controller.isClosed) {
        timer.cancel();
        return;
      }
      
      final stockKeys = _listedStocks.keys.toList();
      final randomKey = stockKeys[_random.nextInt(stockKeys.length)];
      final stock = _listedStocks[randomKey]!;
      
      // Fluctuate price by -2% to +2%
      final changePercent = (_random.nextDouble() * 0.04) - 0.02;
      final newPrice = stock.price.amount * (1 + changePercent);
      stock.price = Money(newPrice);
      
      _controller.add(stock);
    });
  }

  void closeMarket() {
    print('🔕 Market is CLOSED');
    _controller.close();
  }
}

// ==========================================
// 4. Main Application (Integration)
// ==========================================

void main() async {
  // Setup
  final market = StockMarket();
  final analyzer = MarketAnalyzer();
  final executor = TradeExecutor();
  final userPortfolio = Portfolio<Stock>(Money(10000.0)); // Starting with $10,000

  print('--- Welcome to Dart Simulation Engine ---');
  print('User Balance: ${userPortfolio.balance}');

  // Start Market
  market.openMarket();

  // Listen to Price Updates (Async Loop - Topic 12, 30)
  // We use a subscription to allow cancelling later
  final subscription = market.priceUpdates.listen((stock) {
    print('[Stream] 📈 ${stock.symbol} updated to ${stock.price}');
  });

  // Run heavy analysis without blocking
  // This runs in parallel with the stream updates
  analyzer.analyzeMarketTrends();

  // Simulate User Activity
  await Future.delayed(Duration(seconds: 2));
  
  // Scenario 1: Buy AAPL
  final aapl = market.getStock('AAPL')!;
  final result1 = await executor(userPortfolio, aapl, 10, OrderType.buy);
  
  // Pattern Matching on Result (Topic 10, 13)
  switch (result1) {
    case Success(executionPrice: var price, timestamp: var time):
      print('✅ Trade Executed: Bought at $price on $time');
    case Failure(reason: var r):
      print('❌ Trade Failed: $r');
  }

  await Future.delayed(Duration(seconds: 1));

  // Scenario 2: Try to buy expensive GOOG (Fail case)
  final goog = market.getStock('GOOG')!;
  final result2 = await executor(userPortfolio, goog, 10, OrderType.buy); // Cost > 20,000
  
  switch (result2) {
    case Success():
      print('✅ Bought GOOG');
    case Failure(reason: var r):
      print('❌ GOOG Trade Failed: $r');
  }

  // Final State
  await Future.delayed(Duration(seconds: 2));
  print('\n--- End of Session ---');
  print('Final Balance: ${userPortfolio.balance}');
  
  // Cleanup
  await subscription.cancel();
  market.closeMarket();
}
```