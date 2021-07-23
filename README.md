
# Substrate Calculator

 A simple calculator built with substrate.

## Why use it? 
Its useful for simple calculations like addition, subtraction, multiplication, division and modulus. The program reads data from the standard input and prints to standard output.


 


## Installation

Simply go through [substrate.dev](https://substrate.dev/) and follow the installation steps. Also try tutorials like add pallet in its own crate etc.

Install the Node Template:
You should already have version v3.0.0 of the Substrate Node Template compiled on your computer and completed the Create Your First Substrate Chain Tutorial.

### Adding Calculator pallet
```bash
cd pallets
git clone -b v3.0.0 --depth 1 https://github.com/substrate-developer-hub/substrate-pallet-template calculator
```
### Renaming your crate

``` pallets/calculator/Cargo.toml ```

```bash
[package]
authors = ['Substrate DevHub <https://github.com/substrate-developer-hub>']
description = 'FRAME pallet template for defining custom runtime logic.'
edition = '2018'
homepage = 'https://substrate.dev'
license = 'Unlicense'
name = 'pallet-calculator'
readme = 'README.md'
repository = 'https://github.com/substrate-developer-hub/substrate-node-template/'
version = '3.0.0'
```
### Compile the calculator pallet
```bash
cd calculator
SKIP_WASM_BUILD=1 cargo check
SKIP_WASM_BUILD=1 cargo test
```
### Implementing trait
 For runtime, implementation will look like

 ``` runtime/Cargo.toml  ```

```bash
[dependencies]
#--snip--
pallet-calculator = {default-features = false, version = '3.0.0', path = '../pallets/calculator'}
```
As with other pallets, the calculations pallet has an std feature. We should build its std feature.
``` runtime/Cargo.toml  ```
```bash
[features]
default = ["std"]
std = [
	#--snip--
	'pallet-calculator/std',
	#--snip--
]
```
### Import the calculator pallet in ``` runtime/src/lib.rs  ```
```bash
pub use pallet_calculator;
```
Configure the pallet-calculator in pallets/calculator.
```bash
impl pallet_calculator::Config for Runtime {
	type Event = Event;
}
```
### Construct runtime in ``` runtime/src/lib.rs  ```
```bash
construct_runtime!(
    pub enum Runtime where
	Block = Block,
	NodeBlock = opaque::Block,
	UncheckedExtrinsic = UncheckedExtrinsic
	{
		/* --snip-- */

		/*** Add This Line ***/
		Calculator: pallet_calculator::{Pallet, Call, Storage, Event<T>},
	}
);
```
### Interact with the calculator pallet
```bash
cargo build --release
```
After the build succeeds, you can start the node
```bash
./target/release/node-template --dev --tmp
```





    





 Once your node is running, At that time go to [polkadot.js](https://polkadot.js.org/apps/)
 ### Addition operation
 ![add](https://user-images.githubusercontent.com/85221851/126440572-8fb1d4e9-5021-4fce-b42c-1cb47c7f4df1.png)

### Result of addtion operation
![result (2)](https://user-images.githubusercontent.com/85221851/126441272-b9aff69f-5bd3-47a7-88c8-b3d952432041.png)
