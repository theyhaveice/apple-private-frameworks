# MobileDevice.framework

`MobileDevice.framework` is a private, undocumented Apple framework on macOS that handles low-level communication between the Mac and iOS devices (iPhones, iPads, Apple TVs) over USB and Wi-Fi. It powers the underlying operations of Finder syncing, iTunes, Xcode deployment, and Apple Configurator by interfacing with the `usbmuxd` and `lockdownd` daemons.

## Table Of Contents
- [How to use this](#how-to-use-this)
- [Framework Location](#framework-location)
- [Static Functions](#static-functions)
- [Static Function Usages](#static-function-usages)
- [Code examples](#code-examples)
- [Known lockdownd Domains](#known-lockdownd-domains)

## How to use this

Because it is a private C-based framework, it does not come with public headers. You must declare the opaque structs and function prototypes yourself.

### 1. Link the Framework
When compiling, you must point your linker to the private frameworks directory.
**In Xcode**: Add `/Library/Apple/System/Library/PrivateFrameworks` to your Framework Search Paths, and link against `MobileDevice.framework`.
**CLI**: `-F /Library/Apple/System/Library/PrivateFrameworks -framework MobileDevice`

### 2. Header Declarations
Declare the following in your Objective-C `.m` file or your `.h` file:

```objc
#import <Foundation/Foundation.h>

// Opaque device struct
struct am_device;

// Callback info struct
struct am_device_notification_callback_info {
    struct am_device *dev;
    unsigned int msg; // 1 = Connected, 2 = Disconnected, 3 = Unknown
};

// Callback type
typedef void (*am_device_notification_callback)(struct am_device_notification_callback_info *info, void *callback_data);

// Static Functions
extern CFStringRef AMDeviceCopyDeviceIdentifier(struct am_device *device);
extern int AMDeviceConnect(struct am_device *device);
extern int AMDeviceDisconnect(struct am_device *device);
extern int AMDeviceIsPaired(struct am_device *device);
extern int AMDeviceValidatePairing(struct am_device *device);
extern int AMDeviceStartSession(struct am_device *device);
extern int AMDeviceStopSession(struct am_device *device);
extern CFTypeRef AMDeviceCopyValue(struct am_device *device, CFStringRef domain, CFStringRef key);
extern int AMDeviceSetValue(struct am_device *device, CFStringRef domain, CFStringRef key, CFTypeRef value);
extern void AMDeviceNotificationSubscribe(am_device_notification_callback callback, int unused0, int unused1, int unused2, void **notificationOut);
extern int AMDeviceNotificationSubscribeWithOptions(am_device_notification_callback callback, int unused0, int interfaceType, void *unused1, void **notificationOut, CFDictionaryRef options);
// etc...
```

## Framework Location
```text
/Library/Apple/System/Library/PrivateFrameworks/MobileDevice.framework
```

## Static Functions

| Function Name | Description |
| :--- | :--- |
| `AMDeviceActivate` | Activate. |
| `AMDeviceActivateWithOptions` | Activate with options. |
| `AMDeviceArchiveApplication` | Archive application. |
| `AMDeviceCheckCapabilitiesMatch` | Check capabilities match. |
| `AMDeviceConnect` | Establishes a raw connection to the device's multiplexer. |
| `AMDeviceCopyAuthInstallPreflightOptions` | Returns a copy of the auth install preflight options. |
| `AMDeviceCopyBonjourFullServiceName` | Returns a copy of the bonjour full service name. |
| `AMDeviceCopyCryptexNonce` | Returns a copy of the cryptex nonce. |
| `AMDeviceCopyDeveloperModeStatus` | Returns a copy of the developer mode status. |
| `AMDeviceCopyDeviceIdentifier` | Retrieves the unique identifier (UDID) of the connected device. |
| `AMDeviceCopyDeviceLocation` | Returns a copy of the device location. |
| `AMDeviceCopyDeviceUSBSerialNumber` | Returns a copy of the device USB serial number. |
| `AMDeviceCopyFDRPreflightOptions` | Returns a copy of the FDR preflight options. |
| `AMDeviceCopyMountedDevicesList` | Returns a copy of the mounted devices list. |
| `AMDeviceCopyMultipleValuesWithError` | Returns a copy of the multiple values with error. |
| `AMDeviceCopyPairedCompanion` | Returns a copy of the paired companion. |
| `AMDeviceCopyPairedWatch` | Returns a copy of the paired watch. |
| `AMDeviceCopyPersonalizationIdentifiersWithError` | Returns a copy of the personalization identifiers with error. |
| `AMDeviceCopyPersonalizationManifest` | Returns a copy of the personalization manifest. |
| `AMDeviceCopyPersonalizationNonce` | Returns a copy of the personalization nonce. |
| `AMDeviceCopyPersonalizationNonceWithOptions` | Returns a copy of the personalization nonce with options. |
| `AMDeviceCopyProvisioningProfiles` | Returns a copy of the provisioning profiles. |
| `AMDeviceCopyRemoteDevice` | Returns a copy of the remote device. |
| `AMDeviceCopyRemoteDeviceWithError` | Returns a copy of the remote device with error. |
| `AMDeviceCopyValue` | Queries the device for metadata values or entire dictionaries within specific domains. |
| `AMDeviceCopyValueWithError` | Returns a copy of the value with error. |
| `AMDeviceCopyWirelessDeviceValueWithError` | Returns a copy of the wireless device value with error. |
| `AMDeviceCreate` | Creates . |
| `AMDeviceCreateActivationInfo` | Creates activation info. |
| `AMDeviceCreateActivationInfoWithOptions` | Creates activation info with options. |
| `AMDeviceCreateActivationSessionInfo` | Creates activation session info. |
| `AMDeviceCreateCopy` | Creates copy. |
| `AMDeviceCreateFromProperties` | Creates from properties. |
| `AMDeviceCreateHouseArrestService` | Creates house arrest service. |
| `AMDeviceCreateSRPConnection` | Creates SRP connection. |
| `AMDeviceCreateWakeupToken` | Creates wakeup token. |
| `AMDeviceCreateWithRemoteDevice` | Creates with remote device. |
| `AMDeviceCreateWithRemoteDeviceWithError` | Creates with remote device with error. |
| `AMDeviceDeactivate` | Deactivate. |
| `AMDeviceDeleteHostPairingRecordForUDID` | Removes or deletes host pairing record for UDID. |
| `AMDeviceDisconnect` | Closes the raw connection to the device. |
| `AMDeviceEnterRecovery` | Enter recovery. |
| `AMDeviceExtendedPairWithOptions` | Extended pair with options. |
| `AMDeviceGetConnectionID` | Retrieves the connection ID. |
| `AMDeviceGetInterfaceSpeed` | Retrieves the interface speed. |
| `AMDeviceGetInterfaceType` | Retrieves the interface type. |
| `AMDeviceGetLocalOrRemoteOffsetToResume` | Retrieves the local or remote offset to resume. |
| `AMDeviceGetName` | Retrieves the name. |
| `AMDeviceGetTypeID` | Retrieves the type ID. |
| `AMDeviceGetUserInfo` | Retrieves the user info. |
| `AMDeviceGetWirelessBuddyFlags` | Retrieves the wireless buddy flags. |
| `AMDeviceImageMounted` | Image mounted. |
| `AMDeviceInstallApplication` | Installs application. |
| `AMDeviceInstallProvisioningProfile` | Installs provisioning profile. |
| `AMDeviceIsAtLeastVersionOnPlatform` | Checks if the device at least version on platform. |
| `AMDeviceIsBackedByRemotePairing` | Checks if the device backed by remote pairing. |
| `AMDeviceIsPaired` | Checks if the iOS device has been "Trusted" by this computer. |
| `AMDeviceIsValid` | Checks if the device valid. |
| `AMDeviceIsWiFiPairableRef` | Checks if the device Wi-Fi pairable ref. |
| `AMDeviceLookupApplicationArchives` | Lookup application archives. |
| `AMDeviceLookupApplications` | Lookup applications. |
| `AMDeviceMountImage` | Mount image. |
| `AMDeviceMountImageOnHost` | Mount image on host. |
| `AMDeviceMountPersonalizedBundle` | Mount personalized bundle. |
| `AMDeviceNotificationSubscribe` | Subscribes to basic USB device connection and disconnection events. |
| `AMDeviceNotificationSubscribeWithOptions` | Advanced subscription that accepts a dictionary to enable scanning for Wi-Fi devices. |
| `AMDeviceNotificationUnsubscribe` | Notification unsubscribe. |
| `AMDevicePair` | Pair. |
| `AMDevicePairWithCallback` | Pair with callback. |
| `AMDevicePairWithOptions` | Pair with options. |
| `AMDevicePowerAssertionCreate` | Power assertion create. |
| `AMDevicePowerAssertionGetTypeID` | Power assertion get type ID. |
| `AMDevicePreflightOperationCreate` | Preflight operation create. |
| `AMDevicePreflightOperationGetRunLoopSource` | Preflight operation get run loop source. |
| `AMDevicePreflightOperationGetTypeID` | Preflight operation get type ID. |
| `AMDevicePreflightOperationInvalidate` | Preflight operation invalidate. |
| `AMDeviceRegisterForCUNotificationsWithOptions` | Register for CU notifications with options. |
| `AMDeviceRegisterForCUStateNotificationsWithOptions` | Register for CU state notifications with options. |
| `AMDeviceRelayFile` | Relay file. |
| `AMDeviceRelease` | Release. |
| `AMDeviceRemoteCopyCryptexNonce` | Remotely copy cryptex nonce. |
| `AMDeviceRemoteCopyDeveloperModeStatus` | Remotely copy developer mode status. |
| `AMDeviceRemoteCopyMountedDevicesList` | Remotely copy mounted devices list. |
| `AMDeviceRemoteCopyPersonalizationIdentifiersWithError` | Remotely copy personalization identifiers with error. |
| `AMDeviceRemoteCopyPersonalizationManifest` | Remotely copy personalization manifest. |
| `AMDeviceRemoteCopyPersonalizationNonce` | Remotely copy personalization nonce. |
| `AMDeviceRemoteCopyPersonalizationNonceWithOptions` | Remotely copy personalization nonce with options. |
| `AMDeviceRemoteImageMounted` | Remotely image mounted. |
| `AMDeviceRemoteImageMountedMacOS` | Remotely image mounted macOS. |
| `AMDeviceRemoteMountImage` | Remotely mount image. |
| `AMDeviceRemoteMountImageMacOS` | Remotely mount image macOS. |
| `AMDeviceRemoteMountPersonalizedBundle` | Remotely mount personalized bundle. |
| `AMDeviceRemoteRollCryptexNonce` | Remotely roll cryptex nonce. |
| `AMDeviceRemoteRollPersonalizationNonce` | Remotely roll personalization nonce. |
| `AMDeviceRemoteUnmountImage` | Remotely unmount image. |
| `AMDeviceRemoteValidatePairingRecord` | Remotely validate pairing record. |
| `AMDeviceRemoveApplicationArchive` | Removes or deletes application archive. |
| `AMDeviceRemoveProvisioningProfile` | Removes or deletes provisioning profile. |
| `AMDeviceRemoveValue` | Removes or deletes value. |
| `AMDeviceRequestAbbreviatedSendSync` | Request abbreviated send sync. |
| `AMDeviceRestoreApplication` | Restore application. |
| `AMDeviceRetain` | Retain. |
| `AMDeviceRollCryptexNonce` | Roll cryptex nonce. |
| `AMDeviceRollPersonalizationNonce` | Roll personalization nonce. |
| `AMDeviceSecureArchiveApplication` | Securely archive application. |
| `AMDeviceSecureCheckCapabilitiesMatch` | Securely check capabilities match. |
| `AMDeviceSecureInstallApplication` | Securely install application. |
| `AMDeviceSecureInstallApplicationBundle` | Securely install application bundle. |
| `AMDeviceSecureRemoveApplicationArchive` | Securely remove application archive. |
| `AMDeviceSecureRestoreApplication` | Securely restore application. |
| `AMDeviceSecureStartService` | Securely start service. |
| `AMDeviceSecureTransferPath` | Securely transfer path. |
| `AMDeviceSecureUninstallApplication` | Securely uninstall application. |
| `AMDeviceSecureUpgradeApplication` | Securely upgrade application. |
| `AMDeviceSetUserInfo` | Sets the user info. |
| `AMDeviceSetValue` | Sets the value. |
| `AMDeviceSetWirelessBuddyFlags` | Sets the wireless buddy flags. |
| `AMDeviceStartHouseArrestService` | Starts the house arrest service. |
| `AMDeviceStartService` | Starts the service. |
| `AMDeviceStartServiceWithOptions` | Starts the service with options. |
| `AMDeviceStartSession` | Starts a secure `lockdownd` session to allow data querying and service mounting. |
| `AMDeviceStopSession` | Safely terminates the active `lockdownd` session. |
| `AMDeviceTransferApplication` | Transfer application. |
| `AMDeviceTransferPath` | Transfer path. |
| `AMDeviceUSBDeviceID` | Usb device ID. |
| `AMDeviceUSBLocationID` | Usb location ID. |
| `AMDeviceUSBProductID` | Usb product ID. |
| `AMDeviceUninstallApplication` | Removes or deletes all application. |
| `AMDeviceUnmountImage` | Unmount image. |
| `AMDeviceUnmountImageOnHost` | Unmount image on host. |
| `AMDeviceUnpair` | Unpair. |
| `AMDeviceUpgradeApplication` | Upgrade application. |
| `AMDeviceValidatePairing` | Validates the cryptographic pairing records before starting a session. |
| `AMDeviceVerifySRPConnection` | Verify srp connection. |
| `AMDeviceWakeupOperationCreateWithToken` | Wakeup operation create with token. |
| `AMDeviceWakeupOperationGetTypeID` | Wakeup operation get type ID. |
| `AMDeviceWakeupOperationInvalidate` | Wakeup operation invalidate. |
| `AMDeviceWakeupOperationSchedule` | Wakeup operation schedule. |
| `AMDeviceWakeupUsingToken` | Wakeup using token. |
| `AMDeviceWiFiPairableCopyRealUniqueDeviceID` | Wifi pairable copy real unique device ID. |

## Static Function Usages

### Subscribing to Events (`AMDeviceNotificationSubscribe` & `AMDeviceNotificationSubscribeWithOptions`)

**Swift:**
```swift
func deviceCallback(info: UnsafeMutablePointer<am_device_notification_callback_info>?, data: UnsafeMutableRawPointer?) {
    guard let info = info else { return }
    if info.pointee.msg == 1 { print("Connected") }
    else if info.pointee.msg == 2 { print("Disconnected") }
}

var notification: UnsafeMutableRawPointer? = nil

// Standard USB-only subscription
AMDeviceNotificationSubscribe(deviceCallback, 0, 0, 0, &notification)

// Wi-Fi + USB subscription using Options
let options: [String: Any] = ["NotificationOptionSearchForWiFiPairableDevices": true]
AMDeviceNotificationSubscribeWithOptions(deviceCallback, 0, 0, nil, &notification, options as CFDictionary)
```

**Objective-C:**
```objc
void deviceCallback(struct am_device_notification_callback_info *info, void *callback_data) {
    if (info->msg == 1) { NSLog(@"Connected"); }
    else if (info->msg == 2) { NSLog(@"Disconnected"); }
}

void *notification = NULL;

// Standard USB-only subscription
AMDeviceNotificationSubscribe(deviceCallback, 0, 0, 0, &notification);

// Wi-Fi + USB subscription using Options
NSDictionary *options = @{@"NotificationOptionSearchForWiFiPairableDevices": @YES};
AMDeviceNotificationSubscribeWithOptions(deviceCallback, 0, 0, NULL, &notification, (__bridge CFDictionaryRef)options);
```

### Retrieving UDID (`AMDeviceCopyDeviceIdentifier`)

**Swift:**
```swift
let udidRaw = AMDeviceCopyDeviceIdentifier(device)
if let udid = udidRaw?.takeRetainedValue() as? String {
    print("UDID: (udid)")
}
```

**Objective-C:**
```objc
CFStringRef udidRaw = AMDeviceCopyDeviceIdentifier(device);
NSString *udid = (__bridge_transfer NSString *)udidRaw;
NSLog(@"UDID: %@", udid);
```

### The Connection Lifecycle (`AMDeviceConnect`, `AMDeviceIsPaired`, `AMDeviceValidatePairing`, `AMDeviceStartSession`, `AMDeviceStopSession`, `AMDeviceDisconnect`)

You must authorize a session before reading any data.

**Swift:**
```swift
AMDeviceConnect(device)
if AMDeviceIsPaired(device) == 1 {
    AMDeviceValidatePairing(device)
    AMDeviceStartSession(device)
    
    // ... READ OR WRITE DATA ...
    
    AMDeviceStopSession(device)
}
AMDeviceDisconnect(device)
```

**Objective-C:**
```objc
AMDeviceConnect(device);
if (AMDeviceIsPaired(device) == 1) {
    AMDeviceValidatePairing(device);
    AMDeviceStartSession(device);
    
    // ... READ OR WRITE DATA ...
    
    AMDeviceStopSession(device);
}
AMDeviceDisconnect(device);
```

### Querying Metadata (`AMDeviceCopyValue`)

You can query specific keys or dump entire dictionaries by passing `nil` as the key.

**Swift:**
```swift
// Get a specific value (e.g. Battery Capacity)
let batteryDomain = "com.apple.mobile.battery" as CFString
let capacityRaw = AMDeviceCopyValue(device, batteryDomain, "BatteryCurrentCapacity" as CFString)
if let capacity = capacityRaw?.takeRetainedValue() as? NSNumber {
    print("Battery: (capacity)%")
}

// Dump an entire domain dictionary
let rawData = AMDeviceCopyValue(device, "com.apple.disk_usage" as CFString, nil)
if let dictionary = rawData?.takeRetainedValue() as? [String: Any] {
    print(dictionary) // Prints all disk usage metrics
}
```

**Objective-C:**
```objc
// Get a specific value (e.g. Battery Capacity)
CFStringRef batteryDomain = CFSTR("com.apple.mobile.battery");
CFTypeRef capacityRaw = AMDeviceCopyValue(device, batteryDomain, CFSTR("BatteryCurrentCapacity"));
NSNumber *capacity = (__bridge_transfer NSNumber *)capacityRaw;
NSLog(@"Battery: %@%%", capacity);

// Dump an entire domain dictionary
CFTypeRef rawData = AMDeviceCopyValue(device, CFSTR("com.apple.disk_usage"), NULL);
NSDictionary *dictionary = (__bridge_transfer NSDictionary *)rawData;
NSLog(@"%@", dictionary);
```

## Code examples

### Getting the Device Name
This example assumes you have already connected to the device and started a session. The `DeviceName` is stored in the Root domain, so we pass `nil`/`NULL` for the domain.

**Swift:**
```swift
let nameRaw = AMDeviceCopyValue(device, nil, "DeviceName" as CFString)
if let deviceName = nameRaw?.takeRetainedValue() as? String {
    print("Device Name: (deviceName)")
}
```

**Objective-C:**
```objc
CFTypeRef nameRaw = AMDeviceCopyValue(device, NULL, CFSTR("DeviceName"));
NSString *deviceName = (__bridge_transfer NSString *)nameRaw;
NSLog(@"Device Name: %@", deviceName);
```

### Getting the iOS Version
The current iOS software version installed on the device is stored in the Root domain under the `ProductVersion` key.

**Swift:**
```swift
let versionRaw = AMDeviceCopyValue(device, nil, "ProductVersion" as CFString)
if let iOSVersion = versionRaw?.takeRetainedValue() as? String {
    print("iOS Version: (iOSVersion)")
}
```

**Objective-C:**
```objc
CFTypeRef versionRaw = AMDeviceCopyValue(device, NULL, CFSTR("ProductVersion"));
NSString *iOSVersion = (__bridge_transfer NSString *)versionRaw;
NSLog(@"iOS Version: %@", iOSVersion);
```

### Getting the Wi-Fi MAC Address
The Wi-Fi MAC Address is stored in the Root domain under the `WiFiAddress` key.

**Swift:**
```swift
let wifiRaw = AMDeviceCopyValue(device, nil, "WiFiAddress" as CFString)
if let wifiAddress = wifiRaw?.takeRetainedValue() as? String {
    print("Wi-Fi MAC: (wifiAddress)")
}
```

**Objective-C:**
```objc
CFTypeRef wifiRaw = AMDeviceCopyValue(device, NULL, CFSTR("WiFiAddress"));
NSString *wifiAddress = (__bridge_transfer NSString *)wifiRaw;
NSLog(@"Wi-Fi MAC: %@", wifiAddress);
```

### Getting Total Disk Capacity (in GB)
To get storage metrics, you must query the `com.apple.disk_usage` domain. The values are returned in bytes, so we divide by `1,000,000,000` to get Gigabytes (Apple uses decimal GB, not GiB).

**Swift:**
```swift
let diskDomain = "com.apple.disk_usage" as CFString
let capacityRaw = AMDeviceCopyValue(device, diskDomain, "TotalDiskCapacity" as CFString)

if let capacityBytes = capacityRaw?.takeRetainedValue() as? NSNumber {
    let capacityGB = Double(truncating: capacityBytes) / 1_000_000_000.0
    print(String(format: "Total Disk: %.2f GB", capacityGB))
}
```

**Objective-C:**
```objc
CFStringRef diskDomain = CFSTR("com.apple.disk_usage");
CFTypeRef capacityRaw = AMDeviceCopyValue(device, diskDomain, CFSTR("TotalDiskCapacity"));

NSNumber *capacityBytes = (__bridge_transfer NSNumber *)capacityRaw;
if (capacityBytes) {
    double capacityGB = [capacityBytes doubleValue] / 1000000000.0;
    NSLog(@"Total Disk: %.2f GB", capacityGB);
}
```


### Forcing the Device into Recovery Mode
This will instantly kick the connected device into Recovery Mode (the 'Connect to iTunes' screen).

**Swift:**
```swift
let result = AMDeviceEnterRecovery(device)
if result == 0 {
    print("Device is rebooting into Recovery Mode!")
}
```

**Objective-C:**
```objc
int result = AMDeviceEnterRecovery(device);
if (result == 0) {
    NSLog(@"Device is rebooting into Recovery Mode!");
}
```

### Retrieving Paired Apple Watches
Returns a dictionary containing information about any Apple Watches actively paired to this iPhone.

**Swift:**
```swift
let watchRaw = AMDeviceCopyPairedWatch(device)
if let watchInfo = watchRaw?.takeRetainedValue() as? [String: Any] {
    print("Paired Watch Info: \(watchInfo)")
}
```

**Objective-C:**
```objc
CFTypeRef watchRaw = AMDeviceCopyPairedWatch(device);
NSDictionary *watchInfo = (__bridge_transfer NSDictionary *)watchRaw;
NSLog(@"Paired Watch Info: %@", watchInfo);
```

### Dumping Provisioning Profiles
Fetches all `.mobileprovision` profiles currently installed on the device (useful for checking sideloading signatures).

**Swift:**
```swift
let profilesRaw = AMDeviceCopyProvisioningProfiles(device)
if let profiles = profilesRaw?.takeRetainedValue() as? [Any] {
    print("Found \(profiles.count) provisioning profiles.")
}
```

**Objective-C:**
```objc
CFTypeRef profilesRaw = AMDeviceCopyProvisioningProfiles(device);
NSArray *profiles = (__bridge_transfer NSArray *)profilesRaw;
NSLog(@"Found %lu provisioning profiles.", (unsigned long)profiles.count);
```

### Deactivating the Device
This forcefully deactivates the iPhone, throwing it back to the "Hello" setup screen requiring Activation over Wi-Fi/Cellular.

**Swift:**
```swift
let result = AMDeviceDeactivate(device)
if result == 0 {
    print("Device successfully deactivated.")
}
```

**Objective-C:**
```objc
int result = AMDeviceDeactivate(device);
if (result == 0) {
    NSLog(@"Device successfully deactivated.");
}
```

### Unpairing the Device
Removes the cryptographic pairing record from the device, forcing the user to "Trust this Computer" again.

**Swift:**
```swift
let result = AMDeviceUnpair(device)
if result == 0 {
    print("Device pairing has been revoked.")
}
```

**Objective-C:**
```objc
int result = AMDeviceUnpair(device);
if (result == 0) {
    NSLog(@"Device pairing has been revoked.");
}
```

### Checking the Connection Interface (USB vs Wi-Fi)
Determines whether the device is currently communicating over a physical cable or over the network.

**Swift:**
```swift
let interfaceType = AMDeviceGetInterfaceType(device)
if interfaceType == 1 {
    print("Connected via USB")
} else if interfaceType == 2 {
    print("Connected via Wi-Fi")
}
```

**Objective-C:**
```objc
int interfaceType = AMDeviceGetInterfaceType(device);
if (interfaceType == 1) {
    NSLog(@"Connected via USB");
} else if (interfaceType == 2) {
    NSLog(@"Connected via Wi-Fi");
}
```

### Getting USB Interface Speed
Retrieves the negotiated connection speed (e.g. 480 Mbps for USB 2.0 Lightning, or higher for USB-C iPads/iPhones).

**Swift:**
```swift
let speed = AMDeviceGetInterfaceSpeed(device)
print("Interface speed: \(speed)")
```

**Objective-C:**
```objc
int speed = AMDeviceGetInterfaceSpeed(device);
NSLog(@"Interface speed: %d", speed);
```

### Tunneling into App Sandboxes (House Arrest)
This requests the lockdown daemon to spawn a `com.apple.mobile.house_arrest` service targeting a specific app bundle. Once successful, it returns a file descriptor you can use to browse the app's internal filesystem (Documents/Library).

**Swift:**
```swift
var fdOut: Int32 = 0
let bundleID = "com.apple.Pages" as CFString

let result = AMDeviceCreateHouseArrestService(device, bundleID, nil, &fdOut)
if result == 0 {
    print("Successfully mounted House Arrest! File descriptor: \(fdOut)")
    // You can now communicate with the fdOut socket using AFC (Apple File Conduit)
}
```

**Objective-C:**
```objc
int fdOut = 0;
CFStringRef bundleID = CFSTR("com.apple.Pages");

int result = AMDeviceCreateHouseArrestService(device, bundleID, NULL, &fdOut);
if (result == 0) {
    NSLog(@"Successfully mounted House Arrest! File descriptor: %d", fdOut);
    // You can now communicate with the fdOut socket using AFC
}
```

## Known lockdownd Domains

For specific subsystems, here is a list of known domains available on modern iOS devices:

*   `ROOT` *(Pass `nil` or `NULL` as the domain to get the root dictionary)*
*   `com.apple.mobile.battery`
*   `com.apple.disk_usage`
*   `com.apple.international`
*   `com.apple.mobile.iTunes`
*   `com.apple.mobile.developer`
*   `com.apple.mobile.restriction`
*   `com.apple.mobile.sync_data_class`
*   `com.apple.mobile.data_sync`
*   `com.apple.mobile.third_party_termination`
*   `com.apple.mobile.user_preferences`
*   `com.apple.mobile.accessibility`
*   `com.apple.xcode.developerdomain`
*   `com.apple.fairplay`
*   `com.apple.mobile.wireless_lockdown`
*   `com.apple.mobile.debug`
*   `com.apple.mobile.software_behavior`
*   `com.apple.mobile.security`
*   `com.apple.mobile.diagnostics`
*   `com.apple.mobile.diagnostics.mac_address`
*   `com.apple.mobile.chaperone`
*   `com.apple.mobile.internal` *(Usually restricted on retail devices)*

