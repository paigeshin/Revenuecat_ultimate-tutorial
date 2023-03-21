# Revenuecat_ultimate-tutorial

https://www.notion.so/Revenuecat-Tutorial-4e831350a15245798a4b94c16c5c3b1c
https://www.revenuecat.com/docs/getting-started#4-using-revenuecats-purchases-sdk 
https://www.revenuecat.com/docs/user-ids

```swift
import SwiftUI
import RevenueCat

@main
struct Revenucat_TutorialApp: App {
    
    init() {
        Purchases.logLevel = .debug
        Purchases.configure(withAPIKey: "appl_FNrVGibDKrKdlWlDuuvVelpBLsi")
    }
    
    var body: some Scene {
        WindowGroup {
            ContentView()
        }
    }
    
    func fetchProducts() {
        /// Fetch Products
        Purchases.shared.getOfferings { offerings, error in
            guard error == nil, let offer = offerings else { return }
            /// Get Information of Products
            for package in offer.current!.availablePackages {
                print(package.storeProduct.subscriptionPeriod!.unit)
                print(package.storeProduct.localizedPriceString)
            }
        }
    }
    
    func buy(package: Package) {
        
        Purchases.shared.purchase(package: package) { transaction, customerInfo, error, userCancelled in
            
            if !userCancelled, error == nil {
                // dismiss
            } else if let error = error {
                // show error
            }
            
            /// Bought State
            if customerInfo?.entitlements.all["your_entitlement"]?.isActive ?? false {
                
            }
        }
        
    }
    
    func getSubscriptionStatus() {
        
        Purchases.shared.getCustomerInfo { customerInfo, error in
            
            if customerInfo?.entitlements["your_entitlement"]?.isActive == true {
                // User is Premium
            }
            
            if customerInfo?.entitlements.active.isEmpty == false {
                // User is premium
            }
            
        }
        
    }
    
    func restore() {
        
        Purchases.shared.restorePurchases { (customerInfo, error) in
            if customerInfo?.entitlements["your_entitlement"]?.isActive == true {
                // User is Premium
            }
            
            if customerInfo?.entitlements.active.isEmpty == false {
                // User is premium
            }
        }
        
    }
    
}

/* React to Subscription Status
 // Additional configure setup
 func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {
   
     Purchases.logLevel = .debug
     Purchases.configure(withAPIKey: <public_sdk_key>)
     Purchases.shared.delegate = self // make sure to set this after calling configure
 }

 extension AppDelegate: PurchasesDelegate {
     func purchases(_ purchases: Purchases, receivedUpdated customerInfo: Purchases.CustomerInfo) {
         // handle any changes to customerInfo
     }
 }
 */

```
