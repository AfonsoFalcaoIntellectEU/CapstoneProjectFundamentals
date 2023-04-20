# Daml Fundamentals Certificate Sample App

✨ Welcome to the Daml Fundamentals Certification Sample App! ✨

As part of the certification process, you will be required to complete a backend-only capstone project that demonstrates your understanding of the material covered throughout the Daml Fundamentals Certification Path. You have the freedom to choose the topic of your project as long as it fulfills the criteria specified below.

The project must include the following components that are fully operational:

+ A signatory with the authority to create and archive contracts
+ A controller with the authority to exercise choices on contracts
+ An observer with the authority to view contracts
+ Test scripts that verify the functionalities of the above mentioned parties

Bonus points will be awarded if you implement the following features:

+ Use the propose / accept design pattern
+ Use the try / catch block for error handling

We will score all required and bonus features (6 in total) by the following:

+ The feature is free of bugs
+ Only authorized users have access to the feature
+ The feature can be tested appropriately
+ TX is not unexpectedly aborted

To help you prepare for your capstone project, we provide this sample app as a guide for the kind of app you should aim to build. The sample app has been designed to showcase the key concepts and skills that you will need to apply in your own project.

We recommend that you examine this app closely, paying attention to the code structure, functionality, and the test script. We believe that this sample app will be an invaluable resource for you as you work towards your certification. Happy coding!

---

# Project Marketplace App
Daml templates designed for a platform for listing items, users making proposals for those items and the owner reject/approve the proposals.

### I. Overview 
This project was created by using the `empty-skeleton` template. The project adopts and exemplifies the `proposal-accept` design pattern. A signatory can create a ItemPurchaseProposal contract. A user can create a ItemPurchaseProposal template then the seller exercises the AcceptProposal, RejectProposal, WithdrawProposal choice as a controller. If the seller rejects, the proposal gets archived; if they accept an ItemPurchase is created and if the original buyer decides to withdraw, the proposal is archived.
Custom exceptions where also used.

### II. Workflow
1. A seller party creates a ListedMarketplaceItem contract. Observers can be specified, in particular the regulators and the public party (used to fetch public info) should be added.
    1. The template provides two choices: `nonconsuming ConsultItemDetails` that lets users with visibility get information about the item and `RemoveListing` that the original seller may exercise to remove the listing.
2. A buyer party may create a ItemPurchaseProposal specifying all necessary details including: the item id, an amount and currency to purchase the item, the buyer and seller party (buyer is a signatory of the contract and seller an observer), the regulator party (observer).
    1. The buyer may withdraw the ItemPurchaseProposal if they desire to do so, archiving it
3. The seller party can either approve or reject the offer by exercising:
    1. AcceptProposal: consuming choice that looks up the original item, and if all verifications succeed, creates a new `ItemPurchase` contract that is registered on the ledger; the original `ListedMarketplaceItem` gets archived (as it no longer makes sense to be listed).
    2. RejectProposal: archives the proposal and everything else remains the same


### III. Challenge(s)

* The project was created by using `empty-skeleton` and the following was removed from `daml.yaml`.
The `init-script` value was updated to:
```yaml
init-script: Test:test
```

Furthermore, this option was added:
```yaml
navigator-options:
 - --feature-user-management=false
```


### IV. Building
To compile the project
```bash
$ daml build
```

### V. Testing
To test all scripts:
Either run the pre-written `test` script in `Test.daml`

### VI. Running
To load the project into the sandbox and start navigator:
```bash
$ daml start
```
