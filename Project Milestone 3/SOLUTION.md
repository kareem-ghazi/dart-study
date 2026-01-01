# Solution: Smart Home Automation System

```dart
import 'dart:math';

// --- 1. Enums & Extension Types ---

// Topic 23: Enums
enum DeviceStatus { active, idle, offline, error }

// Topic 26: Extension Types
// Using 'implements double' to make it transparent for math,
// but distinct enough to signify "Power" in signatures if needed.
extension type Watts(double value) implements double {
  bool get isHighUsage => value > 1000;
}

// --- 2. Mixins for Capabilities ---

// Topic 22: Mixins
mixin BatteryOperated {
  int batteryLevel = 50;

  void charge() {
    batteryLevel = 100;
    print('🔋 Battery charged to 100%');
  }

  bool get needsCharging => batteryLevel < 20;
}

mixin Networked {
  String? ipAddress;

  void connect(String ip) {
    ipAddress = ip;
    print('🌐 Connected to network at $ipAddress');
  }
}

// --- 3. Base Class & Inheritance ---

// Topic 18: Classes (Abstract)
abstract class SmartDevice {
  final String id;
  // Topic 24: Dot Shorthands (can be used in assignments if context known)
  DeviceStatus status = DeviceStatus.idle;

  // Topic 19: Constructors
  SmartDevice(this.id);

  // Topic 5: Records (Return type)
  (bool success, String message) operate();
}

// --- 4. Concrete Classes ---

// Topic 21: Extend a class
class SmartLight extends SmartDevice with Networked {
  double brightness;

  // Topic 19: Named Constructors
  SmartLight.dimmable(String id) 
      : brightness = 0.5, 
        super(id);

  @override
  (bool, String) operate() {
    // Topic 10: Patterns (simple variable assignment logic)
    if (status == DeviceStatus.offline) {
      return (false, 'Light $id is offline');
    }
    return (true, 'Light $id brightness is ${(brightness * 100).toInt()}%');
  }
}

class SecurityCamera extends SmartDevice with BatteryOperated, Networked {
  bool isRecording = false;

  SecurityCamera(String id) : super(id);

  void toggleRecording() {
    isRecording = !isRecording;
    // Topic 24: Dot Shorthands
    status = isRecording ? .active : .idle;
    print('📷 Camera $id recording: $isRecording');
  }

  @override
  (bool, String) operate() {
    if (batteryLevel <= 0) {
      return (false, 'Battery dead');
    }
    return (true, 'Camera $id is ${isRecording ? "recording" : "standing by"}');
  }
}

// --- 5. Extension Methods ---

// Topic 25: Extension Methods
extension StatusChecker on SmartDevice {
  bool get isCritical => status == DeviceStatus.offline || status == DeviceStatus.error;
}

// --- 6. Callable Object ---

// Topic 27: Callable Objects
class AutomationRoutine {
  final String name;

  AutomationRoutine(this.name);

  // The 'call' method allows instances to be used like functions
  void call(SmartDevice device) {
    print('\n--- Running Routine: $name on ${device.id} ---\n');
    if (device is SmartLight) {
      device.brightness = 1.0;
      device.status = DeviceStatus.active;
      print('💡 Light set to max brightness.');
    } else if (device is SecurityCamera) {
      device.toggleRecording();
    }
  }
}

// --- 7. The Hub (Generics & Collections) ---

// Topic 7: Generics
class DeviceHub<T extends SmartDevice> {
  // Topic 6: Collections
  final List<T> devices = [];

  void addDevice(T device) {
    devices.add(device);
    print('➕ Added device: ${device.id}');
  }

  void runDiagnostics() {
    print('\n🔍 Running Diagnostics...\n');
    
    // Topic 12: Loops
    for (var device in devices) {
      // Topic 13: Branches (Switch Expression) & Topic 24: Dot Shorthands
      String statusMsg = switch (device.status) {
        .active => 'Running smoothly',
        .idle => 'Waiting for command',
        .offline => 'Check connection!',
        .error => 'Malfunction detected!',
      };

      print('[${device.id}] Status: $statusMsg');

      // Topic 10: Patterns (Destructuring)
      var (success, msg) = device.operate();
      if (!success) {
        // Topic 14: Error Handling (Simulated)
        print('    ⚠️ Issue: $msg');
      } else {
        print('    ✅ Info: $msg');
      }
      
      // Extension usage
      if (device.isCritical) {
        print('    🚨 CRITICAL ATTENTION NEEDED');
      }
      
      // Extension Type usage (safe power wrapper)
      var power = Watts(Random().nextDouble() * 1200);
      print('    ⚡ Current Usage: ${power.toStringAsFixed(1)}W ${power.isHighUsage ? "(High!)" : ""}');
    }
  }
}

// --- Main Execution ---

void main() {
  print('=== 🏠 Smart Home System Initializing ===\n');

  // 1. Hub
  var hub = DeviceHub<SmartDevice>();

  // 2. Devices
  var light = SmartLight.dimmable('LivingRoom_L1');
  var camera = SecurityCamera('FrontDoor_C1');

  // 3. Mixin usage
  light.connect('192.168.1.50');
  camera.connect('192.168.1.51');
  camera.charge();

  // 4. Add to Hub
  hub.addDevice(light);
  hub.addDevice(camera);

  // 5. Automation (Callable Object)
  var morningRoutine = AutomationRoutine('Morning Protocol');
  
  // Calling the object as a function!
  morningRoutine(light); 
  morningRoutine(camera);

  // 6. Diagnostics
  hub.runDiagnostics();
}
```