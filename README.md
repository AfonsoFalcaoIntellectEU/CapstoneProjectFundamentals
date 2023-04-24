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
