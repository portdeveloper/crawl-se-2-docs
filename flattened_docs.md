

# disable-type-linting-error-checks.md

---
sidebar_position: 8
---

## ✅ Disabling Type and Linting Error Checks

:::tip Hint
TypeScript helps you catch errors at compile time, which can save time and improve code quality, but can be challenging for those who are new to the language or who are used to the more dynamic nature of JavaScript. These sections show the steps required to disable type & lint checks on different levels.
:::tip Hint

### Disabling Commit Checks

We run the `pre-commit` [git hook](https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks) which lints the staged files and doesn't let you commit if there is an linting error.

To disable this, go to the `.husky/pre-commit` file and comment out `yarn lint-staged --verbose`

```diff
- yarn lint-staged --verbose
+ # yarn lint-staged --verbose
```

### Deploying to Vercel Without Any Checks

By default, Vercel runs type and lint checks before building your app. The deployment will fail if there are any type or lint errors.

To ignore these checks while deploying from the CLI, use:

```shell
yarn vercel:yolo
```

If your repo is connected to Vercel, you can set `NEXT_PUBLIC_IGNORE_BUILD_ERROR` to `true` in an [environment variable](https://vercel.com/docs/concepts/projects/environment-variables).

### Disabling GitHub Workflow

We have a GitHub workflow setup checkout `.github/workflows/lint.yaml` which runs type and lint error checks every time code is **pushed** to `main` branch or **pull request** is made to `main` branch.

To disable it, **delete `.github` directory**.


---



# intro.md

---
sidebar_position: 1
slug: /
---

## 🏗 Welcome to Scaffold-ETH 2

[Scaffold-ETH](https://github.com/scaffold-eth/scaffold-eth-2) is everything you need to get started building decentralized applications on Ethereum! 🚀

⚙️ Built using NextJS, RainbowKit, Hardhat, Foundry, Wagmi, and TypeScript.

### About Scaffold-ETH 2

Scaffold-ETH is an open-source, up-to-date toolkit for building decentralized applications (dapps) on the Ethereum blockchain. It's designed to make it easier for developers to create and deploy smart contracts and build user interfaces that interact with those contracts.

- ✅ **Contract Hot Reload**: Your frontend auto-adapts to your smart contract as you edit it.
- 🔥 **Burner Wallet & Local Faucet**: Quickly test your application with a burner wallet and local faucet.
- 🔐 **Integration with Wallet Providers**: Connect to different wallet providers and interact with the Ethereum network.

### Scaffold-ETH 2 Tech Stack

Scaffold-ETH is not a product itself but more of a combination or stack of other great tools. It allows you to quickly build and iterate over your smart contracts and frontends.

Here are the main components:

- [**Hardhat**](https://hardhat.org/docs) or [**Foundry**](https://book.getfoundry.sh/) (user's choice) for running local networks, deploying and testing smart contracts.
- [**Wagmi**](https://wagmi.sh/react/getting-started) for React Hooks to start working with Ethereum.
- [**Viem**](https://viem.sh/docs/getting-started.html) as low-level interface that provides primitives to interact with Ethereum. The alternative to ethers.js and web3.js.
- [**NextJS**](https://nextjs.org/docs) for building a frontend, using many useful pre-made hooks.
- [**RainbowKit**](https://www.rainbowkit.com/docs/) for adding wallet connection.
- [**DaisyUI**](https://daisyui.com/docs/) for pre-built [Tailwind CSS](https://tailwindui.com/components) components.


---



# components/Address.md

---
sidebar_position: 1
---

## Address

Display an address (or ENS) along with a utility icon to copy the address. If the address is associated with an ENS that has an avatar, this avatar will be displayed. If not, a blockie image representation of the address will be shown.

By default, clicking on the address redirects to the connected wallet's network block explorer. If the wallet is not connected, it redirects to the block explorer of [`targetNetworks[0]`](/deploying/deploy-nextjs-app#--targetnetworks).

![Address Example](/img/Address.png)

### Import

```tsx
import { Address } from "~~/components/scaffold-eth";
```

### Usage

```tsx

```

### Props

| Prop                              | Type      | Default Value | Description                                                                                                                   |
| --------------------------------- | --------- | ------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| **address**                       | `string`  | `undefined`   | Address in `0x___` format, it will resolve its ENS if it has one associated.                                                  |
| **disableAddressLink** (optional) | `boolean` | `false`       | Set it to `true` to disable the blockexplorer link behaviour when clicking on the address.                                    |
| **format** (optional)             | `string`  | `"short"`     | By default, only the first five characters of the address are displayed. Set this to `"long"` to display the entire address.  |
| **size** (optional)               | `string`  | `"base"`      | Size for the displayed Address component. `base` by default but you can pass in `xs`, `sm`, `base`, `lg`, `xl`, `2xl`, `3xl`. |


---



# components/AddressInput.md

---
sidebar_position: 3
---

## AddressInput

Display an Ethereum address input that validates the address format, resolves ENS domains, and shows their avatars.

Also shows a blockie image for each address.

![AddressInput Example](/img/addressInput.gif)

### Import

```tsx
import { AddressInput } from "~~/components/scaffold-eth";
```

### Usage

```tsx
const [address, setAddress] = useState("");

;
```

### Props

| Prop                       | Type       | Default Value | Description                                                                  |
| -------------------------- | ---------- | ------------- | ---------------------------------------------------------------------------- |
| **value**                  | `string`   | `undefined`   | An Ethereum address in (`0x___` format) or an ENS domain.                    |
| **onChange**               | `function` | `undefined`   | A callback invoked when the data in the address input changes.               |
| **placeholder** (optional) | `string`   | `undefined`   | The string that will be rendered before address input has been entered.      |
| **name** (optional)        | `string`   | `undefined`   | Helps identify the data being sent if AddressInput is submitted into a form. |
| **disabled** (optional)    | `boolean`  | `false`       | If `true`, sets the address input un-clickable and unusable.                 |


---



# components/Balance.md

---
sidebar_position: 2
---

## Balance

Displays the balance of a given address in both ether (ETH) and US dollars (USD).

![Balance Example](/img/Balance.gif)

### Import

```tsx
import { Balance } from "~~/components/scaffold-eth";
```

### Usage

```tsx

```

### Props

| Prop                     | Type     | Default Value | Description                                                                                                               |
| ------------------------ | -------- | ------------- | ------------------------------------------------------------------------------------------------------------------------- |
| **address**              | `string` | `undefined`   | Address in `0x___` format, it will resolve its ENS if it has one associated.                                              |
| **className** (optional) | `string` | `""`          | Prop to pass additional CSS styling to the component. You can use Tailwind / daisyUI classes like `text-3xl` for styling. |


---



# components/BlockieAvatar.md

---
sidebar_position: 8
---

## BlockieAvatar

Show a blockie (bar code profile icon) component for a given public address.

The autogenerated blockie can be manually replaced by another image that we pass through the `ensImage` prop.

![BlockieAvatar Example](/img/BlockieAvatar.png)

If you want more control over styling the blockie, you can directly use [blo](https://github.com/bpierre/blo) (pre-installed in Scaffold-ETH 2) and internally used by `BlockieAvatar` component to get the image URL.

### Import

```tsx
import { BlockieAvatar } from "~~/components/scaffold-eth";
```

### Usage

```tsx

```

### Props

| Prop                  | Type     | Default Value | Description                                                                               |
| --------------------- | -------- | ------------- | ----------------------------------------------------------------------------------------- |
| `address`             | `string` | `undefined`   | The address for which you want to display its blockie. Ensure it's in the `0x___` format. |
| `size`                | `number` | `undefined`   | Width and Height in pixels (square).                                                      |
| `ensImage` (optional) | `string` | `undefined`   | An arbitrary image url to render instead of the blockie.                                  |


---



# components/EtherInput.md

---
sidebar_position: 4
---

## EtherInput

Displays an input field for ETH/USD amount, with an option to convert between ETH and USD.

![EtherInput Example](/img/EtherInput.gif)

### Import

```tsx
import { EtherInput } from "~~/components/scaffold-eth";
```

### Usage

```tsx
const [ethAmount, setEthAmount] = useState("");

 setEthAmount(amount)} />;
```

### Props

| Prop                       | Type       | Default Value | Description                                                                             |
| -------------------------- | ---------- | ------------- | --------------------------------------------------------------------------------------- |
| **value**                  | `string`   | `undefined`   | You can enter ether quantity or USD quantity, but value will always be stored in ETH.   |
| **onChange**               | `function` | `undefined`   | A callback invoked when the amount in the EtherInput changes.                           |
| **placeholder** (optional) | `string`   | `undefined`   | The string that will be rendered when there is no input value.                          |
| **name** (optional)        | `string`   | `undefined`   | Helps identify the data being sent if EtherInput is submitted into a form.              |
| **disabled** (optional)    | `boolean`  | `false`       | When set to `true`, changes input background color and border to have disabled styling. |


---



# components/InputBase.md

---
sidebar_position: 5
---

## InputBase

Simple building block for creating an input which comes with basic default styles (colors, rounded borders).

![InputBase Example](/img/inputBase.png)

### Import

```tsx
import { InputBase } from "~~/components/scaffold-eth";
```

### Usage

```tsx
const [url, setUrl] = useState();

;
```

### Props

| Prop                       | Type       | Default Value | Description                                                                             |
| -------------------------- | ---------- | ------------- | --------------------------------------------------------------------------------------- |
| **value**                  | `string`   | `undefined`   | The data that your input will show.                                                     |
| **onChange**               | `function` | `undefined`   | A callback invoked when the data in the input changes.                                  |
| **placeholder** (optional) | `string`   | `undefined`   | The string that will be rendered before input data has been entered.                    |
| **name** (optional)        | `string`   | `undefined`   | Helps identify the data being sent if InputBase is submitted into a form.               |
| **error** (optional)       | `boolean`  | `false`       | When set to `true`, changes input border to have error styling.                         |
| **disabled** (optional)    | `boolean`  | `false`       | When set to `true`, changes input background color and border to have disabled styling. |


---



# components/IntergerInput.md

---
sidebar_position: 6
---

## IntegerInput

Provides an input field for integer values, validating that user input is a valid integer, and showing error if not.  
Shows by default a small button to multiply input's value \* 10^18 to transform to wei.

![IntegerInput Example](/img/integerInput.png)

### Import

```tsx
import { IntegerInput } from "~~/components/scaffold-eth";
```

### Usage

```tsx
const [txValue, setTxValue] = useState("");

 {
    setTxValue(updatedTxValue);
  }}
  placeholder="value (wei)"
/>;
```

### Props

| Prop                       | Type       | Default Value | Description                                                                             |
| -------------------------- | ---------- | ------------- | --------------------------------------------------------------------------------------- |
| **value**                  | `string`   | `undefined`   | The data that your input will show.                                                     |
| **onChange**               | `function` | `undefined`   | A callback invoked when the amount in the input changes.                                |
| **placeholder** (optional) | `string`   | `undefined`   | The string that will be rendered before input data has been entered.                    |
| **name** (optional)        | `string`   | `undefined`   | Helps identify the data being sent if InputBase is submitted into a form.               |
| **error** (optional)       | `boolean`  | `false`       | When set to `true`, changes input border to have error styling.                         |
| **disabled** (optional)    | `boolean`  | `false`       | When set to `true`, changes input background color and border to have disabled styling. |


---



# components/RainbowKitCustomConnectButton.md

---
sidebar_position: 7
---

## RainbowKitCustomConnectButton

Scaffold-ETH 2 uses a custom _"Connect Button"_, based on RainbowKit, that is enhanced with several useful features:

- **Balance Display**: Shows the balance of the native token from the connected address.
- **Chain Name and Color**: Displays the name of the connected blockchain and uses a distinct color for each chain.
- **Custom Modal**: Includes copy address feature, view its QR code, access address details in blockexplorer, and disconnect.

You can extend this component to suit your app's needs.

![RainbowKitCustomConnectButton Example](/img/RainbowKitCustomConnectButton.gif)

### Import

```tsx
import { RainbowKitCustomConnectButton } from "~~/components/scaffold-eth";
```

### Usage

```tsx

```


---



# extensions/availableExtensions.md

---
sidebar_position: 10
---

## Available Extensions

### Core Extensions

Core extensions are extensions built and maintained by Scaffold-ETH 2 team. These extensions can be directly accessed via just extension name without mentioning the github user name and branch name:

```bash
npx create-eth@latest -e 
```

E.g.: `npx create-eth@latest -e subgraph`

Here are the core extensions:

- [subgraph](https://github.com/scaffold-eth/create-eth-extensions/tree/subgraph): Uses the subgraphs from [The Graph](https://thegraph.com/) to index and query blockchain data. Helps you build and test subgraphs locally for your contracts. It also enables interaction with the front-end and facilitates easy deployment to Subgraph Studio.
- [ponder](https://github.com/scaffold-eth/create-eth-extensions/tree/ponder): Pre-configured with [ponder.sh](https://ponder.sh), an open-source framework for blockchain application backends. With Ponder, you can quickly build & deploy an API that serves custom data from smart contracts on any EVM blockchain.
- [onchainkit](https://github.com/scaffold-eth/create-eth-extensions/tree/onchainkit): Pre-configured with [onchainkit](https://onchainkit.xyz/),providing an example to help you get started quickly with the ready-to-use React components and TypeScript utilities built by Coinbase team.
- [erc-20](https://github.com/scaffold-eth/create-eth-extensions/tree/erc-20): An implementation of ERC-20 token contract, allowing you to interact with the contract in a user-friendly manner, including getting a holder balance and transferring tokens.
- [eip-712](https://github.com/scaffold-eth/create-eth-extensions/tree/eip-712): An implementation of EIP-712, allowing you to send, sign, and verify typed messages.

### Third-party Extensions

Third-party extensions are extensions built by the community. To use a third-party extension, use the following format:

```bash
npx create-eth@latest -e {github-username}/{extension-repo-name}:{branch-name} # branch-name is optional
```

E.g.: `npx create-eth@latest -e ChangoMan/charts-extension`

To create your own extension, check out the [Creating Your Own Extension](./createExtensions.md) section.


---



# extensions/createExtensions.md

---
sidebar_position: 11
---

## Creating Your Own Extension

This section will help you develop custom extensions for Scaffold-ETH 2, from simple additions to more complex modifications.

> Video Guide: For a visual walkthrough of the extension development process, check out our [YouTube tutorial](https://youtu.be/XQCv533XGZk?si=dlJH4zd4b99_6soW).

### Extension Structure

Before diving into the development process, let's understand the structure an extension should follow:

```
your-extension/
├── extension/
│   ├── packages/
│   │   ├── hardhat/        # (optional) For Hardhat-specific additions
│   │   ├── foundry/        # (optional) For Foundry-specific additions
│   │   └── nextjs/
│   │       ├── app/        # Any new pages/files
│   │       │   └── my-page
│   │       │       ├── page.tsx
│   │       │
│   │       ├── ...         # Any extra files/directories
│   │       └── package.json  # Only include additional dependencies/scripts
│   ├── package.json        # Monorepo root package.json file
│   └── README.md           # Instance README
└── README.md               # Documentation for your extension
```

### Developing a Simple Extension

For simple extensions, such as adding a new page or component, you can directly create the extension structure without going through the full development workflow. Here's how:

1. Create the directory structure as shown above.
2. Add your new page or component in the appropriate directory.
3. If needed, create a `package.json` with any additional dependencies.
4. Push your extension to GitHub.

That's it! Your simple extension is ready to be used by others via:

```shell
npx create-eth@latest -e {github-username}/{extension-repo-name}:{branch-name} # branch-name is optional
```

### Developing an Advanced Extension

#### Template Files and Args

`create-eth` uses a templating system for advanced extensions that need to modify existing files. This system allows you to inject content into specific files in the base project using the `*.args.mjs` files.

Key points:

- They allow you to add specific content to files in the base project.
- Not all files can be modified this way. See [TEMPLATE-FILES.md](https://github.com/scaffold-eth/create-eth/blob/main/contributors/TEMPLATE-FILES.md) for a list of supported template files.
- To use a template file, create an `*.args.mjs` file in your extension having the same path structure as `*.template.mjs`. For example, to add extra tab in the header, you'd create `extension/packages/nextjs/components/Header.tsx.args.mjs`.

#### Advanced Development Workflow

When creating complex extensions, Scaffold-ETH 2 provides a set of tools to make the process easier. This workflow allows you to develop your extension in a full Scaffold-ETH 2 environment, test it locally, and then package it for distribution.

The workflow consists of two main parts:

1. Extension Development: This process helps you create your extension by modifying a base Scaffold-ETH 2 project.

2. Local Testing: This allows you to test your extension in a full Scaffold-ETH 2 environment before publishing.

#### Extension Development Utility

1. **Clone the `create-eth` Repository:**

   ```bash
   git clone https://github.com/scaffold-eth/create-eth.git
   cd create-eth
   yarn install
   ```

2. **Run the Build Script:**

   ```bash
   yarn build:dev
   ```

   This creates `cli.js` and `create-extension.js` in the `dist` directory.

3. **Run the CLI to Create a New Instance:**

   ```bash
   yarn cli
   ```

   This command will create a **new base instance**, similar to running `npx create-eth@latest`.

   The name mentioned for the "Your project name" question will be used as the **extension name**. For example, if you provide `eip` as the value to the question, then the final extension name will be `eip`.

4. **Develop the Extension:**

   - cd into the instance directory.
   - Make necessary changes to the instance project.
   - Commit the changes in the instance repository.

5. **Create the Extension:**

   Return to the `create-eth` folder.

   ```bash
   yarn create-extension {projectName}
   ```

   Example: `yarn create-extension eip`

   This command gathers all changes from the instance and creates an extension in the `create-eth/externalExtensions/${extensionName}` directory. This directory is the actual extension directory (notice it contains only extra files related to your extension changes), which can be published to GitHub and used by others.

6. **Publish the Extension:**

   - Go inside the extension directory.
   - Push the extension to GitHub.

   ```bash
   cd create-eth/externalExtensions/${extensionName}
   git init
   git add .
   git commit -m "Initial commit of my extension"
   git remote add origin 
   git push -u origin main
   ```

   Now other developers can use your published extension by using:

   ```bash
   npx create-eth@latest -e {github-username}/{extension-repo-name}:{branch-name} # extension-branch-name is optional
   ```

#### Local Testing:

This phase allows you to test your extension locally and see how it works when used by other developers.

> NOTE: If you've already published your extension to GitHub using the "Developing a Simple Extension" approach, make sure to clone that extension repository into the `create-eth/externalExtensions/` directory before proceeding with local testing.

1. **Run the CLI in dev mode:**

   ```bash
   yarn cli -e {extensionName} --dev
   ```

   Example: `yarn cli -e eip --dev`

   The `extensionName` should be present in `create-eth/externalExtensions/${extensionName}`.

   Let's suppose you named your project "my-dev-instance". Then this `my-dev-instance` should contain all your extension changes. `--dev` will symlink the extension to the instance project.

2. **Test and Tweak the Extension:**
   Since the instance is symlinked with the extension, make necessary changes directly in the symlinked files within `my-dev-instance`, and changes should be automatically reflected in the `create-eth/externalExtensions/${extensionName}` directory.

3. **Push the tweaked changes**

   - Go inside the extension directory.
   - Push the changes to GitHub.

   ```bash
   cd create-eth/externalExtensions/${extensionName}
   git add .
   git commit -m "some changes"
   git push
   ```

   Next time users call your extension via `npx create-eth@latest -e`, they will get the updated version.


---



# extensions/extensions.md

---
sidebar_position: 9
---

## 🔌 Extensions

This guide introduces extensions for Scaffold-ETH 2 and explains how to use and create extensions.

### What are Extensions?

Extensions are modular add-ons for Scaffold-ETH 2 that provide additional functionality or serve as examples for specific features. They offer several benefits:

- Seamless integration with the base Scaffold-ETH 2 project
- Quick addition of new features, pages, contracts, or components
- Compatibility with Scaffold-ETH 2 core updates and improvements

Extensions are compact packages containing specific code (such as a smart contract or UI component) that automatically integrate with the latest version of Scaffold-ETH 2 when initializing a new project via npx. They are starting points for your project, not finished products.

### Using Extensions

To use an extension when creating a new Scaffold-ETH 2 project, run:

```bash
npx create-eth@latest -e {github-username}/{extension-repo-name}:{branch-name}
```

The `{branch-name}` is optional. If not specified, it uses the default branch.

E.g.: `npx create-eth@latest -e ChangoMan/charts-extension`


---



# deploying/deploy-nextjs-app.mdx

---
sidebar_position: 2
toc_max_heading_level: 5
---

## Deploy Your NextJS App

:::tip Hint
We recommend connecting your GitHub repo to Vercel (through the Vercel UI) so it gets automatically deployed when pushing to `main`.
:::tip Hint

If you want to deploy directly from the CLI, run this and follow the steps to deploy to Vercel:

```
yarn vercel
```

Once you log in (email, GitHub, etc.), the default options should work. It'll give you a public URL.

If you want to redeploy to the same production URL you can run:

```
yarn vercel --prod
```

If you omit the `--prod` flag it will deploy it to a preview/test URL.

**Make sure to check the values of your Scaffold Configuration before deploying your NextJS App.**

### Scaffold App Configuration

You can configure different settings for your dapp at `packages/nextjs/scaffold.config.ts`.

```ts
export type ScaffoldConfig = {
  targetNetworks: Chain[];
  pollingInterval: number;
  alchemyApiKey: string;
  walletConnectProjectId: string;
  onlyLocalBurnerWallet: boolean;
  walletAutoConnect: boolean;
  // your dapp custom config, eg:
  // tokenIcon : string;
};
```

The configuration parameters are described below. Make sure to update the values according to your needs:

##### - targetNetworks

Array of blockchain networks where your dapp is deployed. Use values that are present on chains object from [viem/chains](https://viem.sh/docs/chains/introduction) eg: `targetNetworks: [chains.optimism]`

To add a custom chain that's not in viem/chains, see the recipe, [Add a custom chain](/recipes/add-custom-chain).

##### - pollingInterval

The interval in milliseconds at which your front-end application polls the RPC servers for fresh data. _Note that this setting does not affect the local network._

##### - alchemyApiKey

Default Alchemy API key from Scaffold-ETH 2 for local testing purposes.
It's recommended to obtain your own API key from the [Alchemy Dashboard](https://dashboard.alchemyapi.io/) and store it in this environment variable: `NEXT_PUBLIC_ALCHEMY_API_KEY` in the `\packages\nextjs\.env.local` file.

##### - walletConnectProjectId

WalletConnect's default project ID from Scaffold-ETH 2 for local testing purposes.
It's recommended to obtain your own project ID from the [WalletConnect website](https://cloud.walletconnect.com) and store it in this environment variable: `NEXT_PUBLIC_WALLET_CONNECT_PROJECT_ID` in the `\packages\nextjs\.env.local` file.

##### - onlyLocalBurnerWallet

Controls the networks where the Burner Wallet feature is available. This feature provides a lightweight wallet for users.

- `true` => Use Burner Wallet only on Hardhat network.
- `false` => Use Burner Wallet on all networks.

##### - walletAutoConnect

Set it to `true` to activate automatic wallet connection behavior:

- If the user was connected into a wallet before, on page reload it reconnects automatically.
- If the user is not connected to any wallet, on reload, it connects to the burner wallet _if it is enabled for the current network_. See `onlyLocalBurnerWallet`

You can extend this configuration file, adding new parameters that you need to use across your dapp **(make sure you update the above type `ScaffoldConfig`)**:

```ts
  tokenIcon: "💎",
```

To use the values from the `ScaffoldConfig` in any other file of your application, you first need to import it in those files:

```ts
import scaffoldConfig from "~~/scaffold.config";
```


---



# deploying/deploy-smart-contracts.mdx

---
sidebar_position: 1
---

import Tabs from "@theme/Tabs";
import TabItem from "@theme/TabItem";

## Deploy Your Smart Contracts

To deploy your smart contracts to a live network, there are a few things you need to adjust.

### 1. Configure your network

Scaffold-ETH 2 comes with a selection of predefined networks. To add your custom network:

```mdx-code-block


```

Go to `packages/hardhat/hardhat.config.ts` and add your network to the `networks` object.

```typescript title="packages/hardhat/hardhat.config.ts"
networks: {
    // ... other networks
    base: {
        url: "https://mainnet.base.org",
        accounts: [deployerPrivateKey]
    },
}
```

```mdx-code-block


```

Go to `packages/foundry/foundry.toml` and add your network to the `rpc_endpoints` object.

```toml title="packages/foundry/foundry.toml"
[rpc_endpoints]
...other chains
base = "https://mainnet.base.org"
```




Here are the [Alchemy docs](https://docs.alchemy.com/docs/how-to-add-alchemy-rpc-endpoints-to-metamask) for information on specific networks.

You can also add your custom network by following the recipe [here](/recipes/add-custom-chain).

### 2. Generate a new account or add one to deploy the contract(s) from.

The deployer account is the account that will deploy your contracts. Additionally, the deployer account will be used to execute any function calls that are part of your deployment script.

You can generate a random account / private key or add your crypto wallet's private key.

To create a random account and add the `DEPLOYER_PRIVATE_KEY` to the `.env` file, run:

```
yarn generate
```

```mdx-code-block


```

If you prefer to manually set your own private key, you will need to add `DEPLOYER_PRIVATE_KEY=yourWalletPrivateKey` to `packages/hardhat/.env`.

```mdx-code-block


```

If you prefer to manually set your own private key, you will need to add `DEPLOYER_PRIVATE_KEY=yourWalletPrivateKey` to `packages/foundry/.env`.




You can check the configured (generated or manually set) account and balances with:

```
yarn account
```

### 3. Deploy your smart contract(s)

By default `yarn deploy` will deploy contract to the local network. You can change `defaultNetwork` in:

```mdx-code-block


```

```sh
packages/hardhat/hardhat.config.ts
```

```mdx-code-block


```

```sh
packages/foundry/foundry.toml
```




Run the command below to deploy the smart contract to the target network. Make sure to have some funds in your deployer account to pay for the transaction.

```
yarn deploy --network network_name
```

eg: `yarn deploy --network sepolia`

### 4. Verify your smart contract

You can verify your smart contract on Etherscan by running:

```
yarn verify --network network_name
```

eg: `yarn verify --network sepolia`

This command **works in both Hardhat and Foundry**, verifying all the deployed contracts. However, the verification method differs depending on the Solidity framework you're using...




Hardhat uses [etherscan-verify from hardhat-deploy](https://www.npmjs.com/package/hardhat-deploy#4-hardhat-etherscan-verify).

Additionally, **in Hardhat**, there's an alternative method for contract verification. You can use [hardhat-verify](https://hardhat.org/hardhat-runner/plugins/nomicfoundation-hardhat-verify) to verify your contracts, passing in the network name, contract address and constructor arguments (if any):

```sh
yarn hardhat-verify --network network_name contract_address "Constructor arg 1"`
```

If the chain you're using is not supported by any of the verifying methods, you can add new supported chains to your chosen method, either [etherscan-verify](https://www.npmjs.com/package/hardhat-deploy#options-2) or [hardhat-verify](https://hardhat.org/hardhat-runner/plugins/nomicfoundation-hardhat-verify#adding-support-for-other-networks).




Foundry uses `VerifyAll.s.sol` script located in `packages/foundry/script`.




### Configuration of Third-Party Services for Production-Grade Apps.

By default, Scaffold-ETH 2 provides predefined API keys for popular services such as Alchemy and Etherscan. This allows you to begin developing and testing your applications more easily, avoiding the need to register for these services.

For production-grade applications, it's recommended to obtain your own API keys (to prevent rate limiting issues). You can configure these at:

```mdx-code-block


```

- `ALCHEMY_API_KEY` variable in `packages/hardhat/.env` and `packages/nextjs/.env.local`. You can create API keys from the [Alchemy dashboard](https://dashboard.alchemy.com/).
- `ETHERSCAN_API_KEY` variable in `packages/hardhat/.env` using your generated API key. You can get your key [here](https://etherscan.io/myapikey).

```mdx-code-block


```

- `ALCHEMY_API_KEY` variable in `packages/nextjs/.env.local`. You can create API keys from the [Alchemy dashboard](https://dashboard.alchemy.com/).
- `ETHERSCAN_API_KEY` variable in `packages/foundry/.env` using your generated API key. You can get your key [here](https://etherscan.io/myapikey).

```mdx-code-block


```

:::tip Hint
It's recommended to store envs for nextjs in Vercel/system env config for live apps and use .env.local for local testing.
:::tip Hint


---



# recipes/GetCurrentBalanceFromAccount.md

---
sidebar_position: 1
title: Get balance of the connected account
description: Learn how to retrieve and display the ETH balance of the connected account in your dApp.
---

## Get the Current Balance of the Connected Account

This recipe shows how to fetch and display the ETH balance of the currently connected account.


Here is the full code, which we will be implementing in the guide below:

```tsx title="components/ConnectedAddressBalance.tsx"
import { useAccount } from "wagmi";
import { Address, Balance } from "~~/components/scaffold-eth";

export const ConnectedAddressBalance = () => {
  const { address: connectedAddress } = useAccount();

  return (
    
      Your Ethereum Balance

      
        Address: 
      

      
        Balance: 
      
    
  );
};
```



### Implementation guide

#### Step 1: Create a new Component

Begin by creating a new component in the "components" folder of your application.

```tsx title="components/ConnectedAddressBalance.tsx"
export const ConnectedAddressBalance = () => {
  return (
    
      Your Ethereum Balance
    
  );
};
```

#### Step 2: Retrieve the Connected Account

Fetch the Ethereum address of the currently connected account using the [useAccount wagmi hook](https://wagmi.sh/react/api/hooks/useAccount) and easily display them using Scaffold ETH-2 [Address](/components/Address) and [Balance](/components/Balance) components.

```tsx title="components/ConnectedAddressBalance.tsx"
// highlight-start
import { useAccount } from "wagmi";
import { Address, Balance } from "~~/components/scaffold-eth";
// highlight-end

export const ConnectedAddressBalance = () => {
  // highlight-start
  const { address: connectedAddress } = useAccount();
  // highlight-end

  return (
    
      Your Ethereum Balance
      
      Address: 
      Balance: 
      
    
  );
};
```


---



# recipes/ReadUintFromContract.md

---
sidebar_position: 3
title: Read a uint from a contract
description: Learn how to read from contract functions which accepts arguments / no arguments and display them on UI.
---

## Read a `uint` from a contract

This recipe demonstrates how to read data from contract functions and display it on the UI. We'll showcase an example that accepts some arguments (parameters), and another with no arguments at all.


Here is the full code, which we will be implementing in the guide below:

```tsx title="components/GreetingsCount.tsx"
import { useAccount } from "wagmi";
import { useScaffoldReadContract } from "~~/hooks/scaffold-eth";

export const GreetingsCount = () => {
  const { address: connectedAddress } = useAccount();

  const { data: totalCounter, isLoading: isTotalCounterLoading } = useScaffoldReadContract({
    contractName: "YourContract",
    functionName: "totalCounter",
  });

  const { data: connectedAddressCounter, isLoading: isConnectedAddressCounterLoading } = useScaffoldReadContract({
    contractName: "YourContract",
    functionName: "userGreetingCounter",
    args: [connectedAddress], // passing args to function
  });

  return (
    
      
        Greetings Count
        
          Total Greetings count:
          {isTotalCounterLoading ? (
            
          ) : (
            {totalCounter ? totalCounter.toString() : 0}
          )}
          Your Greetings count:
          {isConnectedAddressCounterLoading ? (
            
          ) : (
            {connectedAddressCounter ? connectedAddressCounter.toString() : 0}
          )}
        
      
    
  );
};
```



### Implementation guide

#### Step 1: Create a new Component

Begin by creating a new component in the "components" folder of your application.

```tsx title="components/GreetingsCount.tsx"
export const GreetingsCount = () => {
  return (
    
      Total Greetings count:
      Your Greetings count:
    
  );
};
```

#### Step 2: Retrieve total greetings count

Initialize the [useScaffoldReadContract](/hooks/useScaffoldReadContract) hook to read from the contract. This hook provides the `data` which contains the return value of the function.

```tsx title="components/GreetingsCount.tsx"
//highlight-start
import { useScaffoldReadContract } from "~~/hooks/scaffold-eth";
// highlight-end

export const GreetingsCount = () => {
  // highlight-start
  const { data: totalCounter } = useScaffoldReadContract({
    contractName: "YourContract",
    functionName: "totalCounter",
  });
  // highlight-end

  return (
    
      Total Greetings count:
      //highlight-start
      {totalCounter ? totalCounter.toString() : 0}
      //highlight-end
      Your Greetings count:
    
  );
};
```

In the line `const {data: totalCounter} = useScaffoldReadContract({...})` we are using [destructuring asssignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment) to assign `data` to a new name `totalCounter`.

In the contract, `totalCounter` returns an `uint` value, which is represented as a [`BigInt`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/BigInt) in javascript and can be converted to a readable string using `.toString()`.

#### Step 3: Retrieve connected address greetings count

We can get the connected address using the [useAccount](https://wagmi.sh/react/api/hooks/useAccount) hook and pass it to `args` key in the `useScaffoldReadContract` hook configuration. This will be used as an argument to read the contract function.

```tsx title="components/GreetingsCount.tsx"
import { useScaffoldReadContract } from "~~/hooks/scaffold-eth";
//highlight-start
import { useAccount } from "wagmi";
//highlight-end

export const GreetingsCount = () => {
  //highlight-start
  const { address: connectedAddress } = useAccount();
  //highlight-end

  const { data: totalCounter } = useScaffoldReadContract({
    contractName: "YourContract",
    functionName: "totalCounter",
  });

  //highlight-start
  const { data: connectedAddressCounter } = useScaffoldReadContract({
    contractName: "YourContract",
    functionName: "userGreetingCounter",
    args: [connectedAddress], // passing args to function
  });
  //highlight-end

  return (
    
      Total Greetings count:
      {totalCounter ? totalCounter.toString() : 0}
      Your Greetings count:
      //highlight-start
      {connectedAddressCounter ? connectedAddressCounter.toString() : 0}
      //highlight-end
    
  );
};
```

#### Step 4: Bonus adding loading state

We can use `isLoading` returned from the [`useScaffoldReadContract`](/hooks/usescaffoldreadcontract) hook. This variable is set to `true` while fetching data from the contract.

```tsx title="components/GreetingsCount.tsx"
import { useScaffoldReadContract } from "~~/hooks/scaffold-eth";
import { useAccount } from "wagmi";

export const GreetingsCount = () => {
  const { address: connectedAddress } = useAccount();

  // highlight-start
  const { data: totalCounter, isLoading: isTotalCounterLoading } = useScaffoldReadContract({
    // highlight-end
    contractName: "YourContract",
    functionName: "totalCounter",
  });

  // highlight-start
  const { data: connectedAddressCounter, isLoading: isConnectedAddressCounterLoading } = useScaffoldReadContract({
    // highlight-end
    contractName: "YourContract",
    functionName: "userGreetingCounter",
    args: [connectedAddress], // passing args to function
  });

  return (
    
      Total Greetings count:
      // highlight-start
      {isTotalCounterLoading ? (
        
      ) : (
        {totalCounter ? totalCounter.toString() : 0}
      )}
      // highlight-end
      Your Greetings count:
      // highlight-start
      {isConnectedAddressCounterLoading ? (
        
      ) : (
        {connectedAddressCounter ? connectedAddressCounter.toString() : 0}
      )}
      // highlight-end
    
  );
};
```


---



# recipes/WagmiContractWriteWithFeedback.md

---
sidebar_position: 4
title: Wagmi useWriteContract with transaction status
description: Show feedback on transaction status to user by `useWriteContract` along with `useTransactor`
---

## Wagmi `useWriteContract` with transaction status

This recipe demonstrates how to create a button for contract interaction using the "useTransactor" and "useWriteContract" hooks from the "wagmi" library. The interaction includes the capability to provide feedback on the transaction status when using wagmi `useWriteContract`.


Here is the full code, which we will be implementing in the guide below:

```tsx title="components/ContractInteraction.tsx"
import * as React from "react";
import { parseEther } from "viem";
import { useWriteContract } from "wagmi";
import DeployedContracts from "~~/contracts/deployedContracts";
import { useTransactor } from "~~/hooks/scaffold-eth";

export const ContractInteraction = () => {
  const { writeContractAsync, isPending } = useWriteContract();

  const writeContractAsyncWithParams = () =>
    writeContractAsync({
      address: DeployedContracts[31337].YourContract.address,
      abi: DeployedContracts[31337].YourContract.abi,
      functionName: "setGreeting",
      value: parseEther("0.01"),
      args: ["Hello world!"],
    });

  const writeTx = useTransactor();

  const handleSetGreeting = async () => {
    try {
      await writeTx(writeContractAsyncWithParams, { blockConfirmations: 1 });
    } catch (e) {
      console.log("Unexpected error in writeTx", e);
    }
  };

  return (
    
      {isPending ?  : "Send"}
    
  );
};
```



### Implementation

#### Step 1: Set Up Your Component

Create a new component in the "components" folder. The component will show a button that will allow users to interact with your smart contract.

```tsx title="components/ContractInteraction.tsx"
import * as React from "react";

export const ContractInteraction = () => {
  return Send;
};
```

#### Step 2: Configure wagmi's `useWriteContract` hook

Add wagmi's `useWriteContract` hook and configure `writeContractAsync` with the parameters: `abi`, `address`, `functionName`, `value` and `args`. Get the ABI and address of your smart contract from the DeployedContracts or you can grab it from ExternalContracts object, those will be used to set up the contract interaction.

```tsx
import * as React from "react";
// highlight-start
import { parseEther } from "viem";
import { useWriteContract } from "wagmi";
import DeployedContracts from "~~/contracts/deployedContracts";
// highlight-end

export const ContractInteraction = () => {
  // highlight-start
  const { writeContractAsync } = useWriteContract();

  const writeContractAsyncWithParams = () =>
    writeContractAsync({
      address: DeployedContracts[31337].YourContract.address,
      abi: DeployedContracts[31337].YourContract.abi,
      functionName: "setGreeting",
      value: parseEther("0.01"),
      args: ["Hello world!"],
    });
  // highlight-end
  return Send;
};
```

#### Step 3: Initialize `useTransactor` hook and send transaction

Initialize the `useTransactor` hook, and use it to wrap `writeContractAsyncWithParams` function which we got from `useWriteContract` to show feedback transaction status to user.

```tsx
import * as React from "react";
import { parseEther } from "viem";
import { useWriteContract } from "wagmi";
import DeployedContracts from "~~/contracts/deployedContracts";
// highlight-start
import { useTransactor } from "~~/hooks/scaffold-eth";
// highlight-end

export const ContractInteraction = () => {
  const { writeContractAsync } = useWriteContract();

  const writeContractAsyncWithParams = () =>
    writeContractAsync({
      address: DeployedContracts[31337].YourContract.address,
      abi: DeployedContracts[31337].YourContract.abi,
      functionName: "setGreeting",
      value: parseEther("0.01"),
      args: ["Hello world!"],
    });

  // highlight-start
  const writeTx = useTransactor();
  // highlight-end

  // highlight-start
  return  writeTx(writeContractAsyncWithParams, { blockConfirmations: 1 })}>Send;
  // highlight-end
};
```

#### Step 4: Wrap `useTransactor` in a handler async function

Wrap the `writeTx` function in a handler function to start the transaction when the user clicks the button.

```tsx
import * as React from "react";
import { parseEther } from "viem";
import { useWriteContract } from "wagmi";
import DeployedContracts from "~~/contracts/deployedContracts";
import { useTransactor } from "~~/hooks/scaffold-eth";

export const ContractInteraction = () => {
  const { writeContractAsync, isPending } = useWriteContract();

  const writeContractAsyncWithParams = () =>
  writeContractAsync({
    address: DeployedContracts[31337].YourContract.address,
    abi: DeployedContracts[31337].YourContract.abi,
    functionName: "setGreeting",
    value: parseEther("0.01"),
    args: ["Hello world!"],
  });

  const writeTx = useTransactor();

  // highlight-start
  const handleSetGreeting = async () => {
    try {
      await writeTx(writeContractAsyncWithParams, { blockConfirmations: 1 });
    } catch (e) {
      console.log("Unexpected error in writeTx", e);
    }
  };
  // highlight-end


  return (
    // highlight-start
    
      Send
    
    // highlight-end
  );

```

#### Step 5: Bonus adding loading state

We can use `isPending` returned from `useWriteContract` while the transaction is being mined and also `disable` the button.

```tsx
import * as React from "react";
import { parseEther } from "viem";
import { useWriteContract } from "wagmi";
import DeployedContracts from "~~/contracts/deployedContracts";
import { useTransactor } from "~~/hooks/scaffold-eth";

export const ContractInteraction = () => {
  // highlight-start
  const { writeContractAsync, isPending } = useWriteContract();
  // highlight-end

  const writeContractAsyncWithParams = () =>
    writeContractAsync({
      address: DeployedContracts[31337].YourContract.address,
      abi: DeployedContracts[31337].YourContract.abi,
      functionName: "setGreeting",
      value: parseEther("0.01"),
      args: ["Hello world!"],
    });

  const writeTx = useTransactor();

  const handleSetGreeting = async () => {
    try {
      await writeTx(writeContractAsyncWithParams, { blockConfirmations: 1 });
    } catch (e) {
      console.log("Unexpected error in writeTx", e);
    }
  };

  return (
    // highlight-start
    
      {isPending ?  : "Send"}
    
    // highlight-end
  );
};
```


---



# recipes/WriteToContractWriteAsyncButton.md

---
sidebar_position: 2
title: Write to contract with writeContractAsync button
description: Learn how to create a button that executes the writeContractAsync function to interact with a smart contract.
---

## Write to a Contract with `writeContractAsync` button

This recipe shows how to implement a button that allows users to interact with a smart contract by executing the `writeContractAsync` function returned by [useScaffoldWriteContract](/hooks/useScaffoldWriteContract). By following this guide, you can create a user interface for writing data to a contract.


Here is the full code, which we will be implementing in the guide below:

```tsx title="components/Greetings.tsx"
import { useState } from "react";
import { parseEther } from "viem";
import { useScaffoldWriteContract } from "~~/hooks/scaffold-eth";

export const Greetings = () => {
  const [newGreeting, setNewGreeting] = useState("");

  const { writeContractAsync, isPending } = useScaffoldWriteContract("YourContract");

  const handleSetGreeting = async () => {
    try {
      await writeContractAsync(
        {
          functionName: "setGreeting",
          args: [newGreeting],
          value: parseEther("0.01"),
        },
        {
          onBlockConfirmation: txnReceipt => {
            console.log("📦 Transaction blockHash", txnReceipt.blockHash);
          },
        },
      );
    } catch (e) {
      console.error("Error setting greeting", e);
    }
  };

  return (
    <>
       setNewGreeting(e.target.value)}
      />
      
        {isPending ?  : "Send"}
      
    
  );
};
```



### Implementation

#### Step 1: Set Up Your Component

Create a new component in the "components" folder. This component will enable users to write data to a smart contract.

```tsx title="components/Greetings.tsx"
export const Greetings = () => {
  return (
    <>
      
      Send
    
  );
};
```

#### Step 2: Initialize `useScaffoldWriteContract` hook

Initialize the `useScaffoldWriteContract` hook. This hook provides the `writeContractAsync` function for sending transactions, we'll create `handleSetGreeting` function in which we'll call and pass parameters to `writeContractAsync` required to perform contract interaction.

```tsx
// highlight-start
import { useState } from "react";
import { parseEther } from "viem";
import { useScaffoldWriteContract } from "~~/hooks/scaffold-eth";
// highlight-end

export const Greetings = () => {
  // highlight-start
  const [newGreeting, setNewGreeting] = useState("");
  // highlight-end

  // highlight-start
  const { writeContractAsync } = useScaffoldWriteContract("YourContract");
  // highlight-end

  // highlight-start
  const handleSetGreeting = async () => {
    try {
      await writeContractAsync(
        {
          functionName: "setGreeting",
          args: [newGreeting],
          value: parseEther("0.01"),
        },
        {
          onBlockConfirmation: txnReceipt => {
            console.log("📦 Transaction blockHash", txnReceipt.blockHash);
          },
        },
      );
    } catch (e) {
      console.error("Error setting greeting", e);
    }
  };
  // highlight-end

  return (
    <>
      
      Send
    
  );
};
```

#### Step 3: Add input change logic and send transaction when users click the button

Wire up the input field to update the `newGreeting` state when the user types in a new greeting and call `handleSetGreeting` function when user click on the button.

```tsx
import { parseEther } from "viem";
import { useScaffoldWriteContract } from "~~/hooks/scaffold-eth";

export const Greetings = () => {
  const [newGreeting, setNewGreeting] = useState("");

  const { writeContractAsync } = useScaffoldWriteContract("YourContract");

  const handleSetGreeting = async () => {
    try {
      await writeContractAsync(
        {
          functionName: "setGreeting",
          args: [newGreeting],
          value: parseEther("0.01"),
        },
        {
          onBlockConfirmation: txnReceipt => {
            console.log("📦 Transaction blockHash", txnReceipt.blockHash);
          },
        },
      );
    } catch (e) {
      console.error("Error setting greeting", e);
    }
  };

  return (
    <>
       setNewGreeting(e.target.value)}
        // highlight-end
      />
      
        Send
      
    
  );
};
```

#### Step 4: Bonus adding loading state

We can use `isPending` returned from `useScaffoldWriteContract` while the transaction is being mined and also disable the button.

```tsx
import { useState } from "react";
import { parseEther } from "viem";
import { useScaffoldWriteContract } from "~~/hooks/scaffold-eth";

export const Greetings = () => {
  const [newGreeting, setNewGreeting] = useState("");
  // highlight-start
  const { writeContractAsync, isPending } = useScaffoldWriteContract("YourContract");
  // highlight-end

  const handleSetGreeting = async () => {
    try {
      await writeContractAsync(
        {
          functionName: "setGreeting",
          args: [newGreeting],
          value: parseEther("0.01"),
        },
        {
          onBlockConfirmation: txnReceipt => {
            console.log("📦 Transaction blockHash", txnReceipt.blockHash);
          },
        },
      );
    } catch (e) {
      console.error("Error setting greeting", e);
    }
  };

  return (
    <>
       setNewGreeting(e.target.value)}
      />

      
        {isPending ?  : "Send"}
      
    
    // highlight-end
  );
};
```


---



# recipes/add-custom-chain.mdx

---
sidebar_position: 5
title: Add a custom chain
description: Learn how to add custom chains to your project.
---

import Tabs from "@theme/Tabs";
import TabItem from "@theme/TabItem";

## Add a custom chain

This recipe demonstrates how to add a custom chain to your project. We'll use Base as an example, but you can apply this process to any other chain you want to add.
Scaffold-ETH 2 uses [viem/chains](https://viem.sh/docs/chains/introduction) as a list of chains.
Normally, Base already exists in viem/chains and [you can import it and use it](/deploying/deploy-nextjs-app#--targetnetworks), but we're going to add it manually to show you how to do it.

:::info
Scaffold-ETH 2 consists of two parts:

- `packages/nextjs`: nextjs frontend
- `packages/hardhat` or `packages/foundry`: hardhat or foundry to deploy smart contracts

The frontend and the hardhat/foundry project use a different set of chains.
You should add the chain to both the frontend and your hardhat/foundry config. Checkout [deploying your smart contract](/deploying/deploy-smart-contracts) section on how to deploy different chains.

By doing this, you will be able to deploy the contracts to the chain you added and interact with them from the frontend.

:::

#### Step 1: Define the chain

First, create a new file called `customChains.ts` in your `packages/nextjs/utils/` directory.

Open the file with your favorite editor and add the following code to define the chain.

```typescript title="packages/nextjs/utils/customChains.ts"
import { defineChain } from "viem";

// Base chain
export const base = defineChain({
  id: 8453,
  name: "Base",
  nativeCurrency: { name: "Base", symbol: "ETH", decimals: 18 },
  rpcUrls: {
    default: {
      http: ["https://mainnet.base.org"],
    },
  },
  blockExplorers: {
    default: {
      name: "Basescan",
      url: "https://basescan.org",
    },
  },
});
```

In this file, we're defining the Base chain. We're using the `defineChain` function from viem to define the chain. You can add as many chains as you want to the `customChains.ts` file.

#### Step 2: Update `scaffold.config.ts`

Next, update your `scaffold.config.ts` file to include the new chain:

```typescript title="packages/nextjs/scaffold.config.ts"
import { base } from "./utils/customChains";
// ... other imports and type definitions

const scaffoldConfig = {
  targetNetworks: [base],
  // ... other configuration options
} as const satisfies ScaffoldConfig;

export default scaffoldConfig;
```

If you'd like to add multiple chains, you can do so by adding them to the `targetNetworks` array. Below is a simple example of how to add multiple chains.

```typescript title="packages/nextjs/scaffold.config.ts"
import { base, baseSepolia } from "./utils/customChains";

const scaffoldConfig = {
  targetNetworks: [base, baseSepolia],
  // ... other configuration options
} as const satisfies ScaffoldConfig;
```


---



# contributing/Issues.md

---
sidebar_position: 1
---

## Issues

Issues should be used to report problems, request a new feature, or discuss potential changes before a PR is created.

### Solve an Issue

Scan through our [existing issues](https://github.com/scaffold-eth/scaffold-eth-2/issues) to find one that interests you.

If a contributor is working on the issue, they will be assigned to that individual. If you find an issue to work on, you are welcome to assign it to yourself and open a PR with a fix for it.

### Create a New Issue

If a related issue doesn't exist, you can open a new issue.

Some tips to follow when you are creating an issue:

- Provide as much context as possible. Over-communicate to give the most detail to the reader.
- Include the steps to reproduce the issue or the reason for adding the feature.
- Screenshots, videos, etc., are highly appreciated.


---



# contributing/contributing.md

---
sidebar_position: 10
---

## 🙏 Contributing to Scaffold-ETH 2

We welcome contributions to Scaffold-ETH 2!

This section aims to provide an overview of the contribution workflow to help us make the contribution process effective for everyone involved.

:::caution
The project is under active development. You can view the open Issues, follow the development process, and contribute to the project.
:::caution

### Getting Started

You can contribute to this repo in many ways:

- Solve open issues
- Report bugs or feature requests
- Improve the documentation

Contributions are made via Issues and Pull Requests (PRs). A few general guidelines for contributions:

- Search for existing Issues and PRs before creating your own.
- Contributions should only fix/add the functionality in the issue OR address style issues, _not both_.
- If you're running into an error, please give context. Explain what you're trying to do and how to reproduce the error.
- Please use the same formatting in the code repository. You can configure your IDE to do this by using the prettier / linting config files included in each package.
- If applicable, please edit the README.md file to reflect changes.


---



# contributing/pullRequests.md

---
sidebar_position: 2
---

## Pull Requests

### Pull Request Process

We follow the ["fork-and-pull" Git workflow](https://github.com/susam/gitpr)

1. Fork the repo
2. Clone the project
3. Create a new branch with a descriptive name
4. Commit your changes to the new branch
5. Push changes to your fork
6. Open a PR in our repository and tag one of the maintainers to review your PR

Here are some tips for a high-quality pull request:

- Create a title for the PR that accurately defines the work done.
- Structure the description neatly to make it easy to consume by the readers. For example, you can include bullet points and screenshots instead of having one large paragraph.
- Add the link to the issue if applicable.
- Have a good commit message that summarises the work done.

Once you submit your PR:

- We may ask questions, request additional information, or ask for changes to be made before a PR can be merged. Please note that these are to make the PR clear for everyone involved and aims to create a frictionless interaction process.
- As you update your PR and apply changes, mark each conversation resolved.

Once the PR is approved, we'll "squash-and-merge" to keep the git commit history clean.


---



# external-contracts/external-contracts.md

---
sidebar_position: 5
---

## 📡 Interacting with External Contracts

If you need to interact with external contracts (i.e. not deployed with your SE-2 instance, e.g [`DAI`](https://etherscan.io/token/0x6b175474e89094c44da98b954eedeac495271d0f#code) contract) you can add external contract data to your `packages/nextjs/contracts/externalContracts.ts` file, which would let you use Scaffold-ETH 2 [custom hooks](/hooks).

To achieve this, include the contract name, its `address`, and `abi` in `externalContracts.ts` for each chain ID. Ensure to update the [`targetNetworks`](/deploying/deploy-nextjs-app#--targetnetworks) in `scaffold.config.ts` to your preferred chains to enable hooks typescript autocompletion.

This is the structure of `externalContracts` object:

```ts
const externalContracts = {
  1: {
    DAI: {
      address: "0x...",
      abi: [...],
    },
    WETH: {
      address: "0x...",
      abi: [...],
    },
  },
  5: {
    DAI: {
      address: "0x...",
      abi: [...],
    },
    WETH: {
      address: "0x...",
      abi: [...],
    },
  },
} as const;
```


---



# quick-start/environment.mdx

---
sidebar_position: 2
description: How to set up your development environment for Scaffold ETH-2.
---

import Tabs from "@theme/Tabs";
import TabItem from "@theme/TabItem";

## Environment

Now that our installation is complete, let's configure the development environment for Scaffold ETH-2.

#### 1. **Initialize a Local Blockchain**:

In the first terminal, run a local network:

```
yarn chain
```

This command starts a local Ethereum network using Hardhat or Foundry, depending on which one you selected in the CLI. The network runs on your local machine and can be used for testing and development. You can customize the network configuration in:

```mdx-code-block


```

```sh
packages/hardhat/hardhat.config.ts
```

```mdx-code-block


```

```sh
packages/foundry/foundry.toml
```




#### 2. **Deploy Your Smart Contract**:

In the second terminal, deploy the test contract:

```
yarn deploy
```

This command deploys a test smart contract to the local network. The contract can be modified to suit your needs and can be found in:

```mdx-code-block


```

```sh
packages/hardhat/contracts
```

```mdx-code-block


```

```sh
packages/foundry/contracts
```




The `yarn deploy` command uses a deploy script to deploy the contract to the network. You can customize the deployment script located in:

```mdx-code-block


```

```sh
packages/hardhat/deploy
```

```mdx-code-block


```

```sh
packages/foundry/script
```




#### 3. **Launch your NextJS Application**:

In the third terminal, start your NextJS app:

```
yarn start
```

Visit your app on `http://localhost:3000`. You can interact with your smart contract using the contract component or the example ui in the frontend.

### What's Next:

```mdx-code-block


```

- Edit your smart contract:
  - `YourContract.sol` in `packages/hardhat/contracts`
- Edit your deployment scripts:
  - `packages/hardhat/deploy`
- Edit your frontend homepage at `packages/nextjs/app/page.tsx`. For guidance on [routing](https://nextjs.org/docs/app/building-your-application/routing/defining-routes) and configuring [pages/layouts](https://nextjs.org/docs/app/building-your-application/routing/pages-and-layouts) checkout the Next.js documentation.
- Edit the app config in `packages/nextjs/scaffold.config.ts`
- Edit your smart contract test in:
  - `packages/hardhat/test` to run test use `yarn hardhat:test`

```mdx-code-block


```

- Edit your smart contract:
  - `YourContract.sol` in `packages/foundry/contracts`
- Edit your deployment scripts:
  - `packages/foundry/script`
- Edit your frontend homepage at `packages/nextjs/app/page.tsx`. For guidance on [routing](https://nextjs.org/docs/app/building-your-application/routing/defining-routes) and configuring [pages/layouts](https://nextjs.org/docs/app/building-your-application/routing/pages-and-layouts) checkout the Next.js documentation.
- Edit the app config in `packages/nextjs/scaffold.config.ts`
- Edit your smart contract test in:
  - `packages/foundry/test` to run test use `yarn foundry:test`





---



# quick-start/installation.mdx

---
sidebar_position: 1
description: Requirements and installation methods to get started with Scaffold ETH-2.
---

## Installation

### Requirements

Before you begin, you need to install the following tools:

- [Node (>= v18.17)](https://nodejs.org/en/download/)
- Yarn ([v1](https://classic.yarnpkg.com/en/docs/install/) or [v2+](https://yarnpkg.com/getting-started/install))
- [Git](https://git-scm.com/downloads)

### Setup

To get started with Scaffold-ETH 2, you have two options:

1. Use the npx command: `npx create-eth@latest` to bootstrap the project directly.
2. Use git clone to clone the repository.

#### Option 1: Setup using `npx create-eth@latest`

For a simplified setup, Scaffold-ETH 2 offers a npx method that guides you interactively through the setup.

Bootstrap the project:

```
npx create-eth@latest
```

You will be presented with a series of prompts:

- **Project Name:** Input your project name: Enter a name for your project, e.g., my-dapp-example.
- **Solidity Framework** What solidity framework do you want to use?: Choose your preferred solidity framework (Hardhat, Foundry)
- **Install packages?:** Press `Enter` for `yes` (default option) or type `n` and press `Enter` for no

Once the setup is complete, navigate to the project directory:

```
cd project-name
```

:::info Hint
If you choose Foundry as solidity framework in the CLI, you'll also need Foundryup installed on your machine.
Checkout: [getfoundry.sh](https://getfoundry.sh/)
:::info Hint

If you want to use extensions, you can add the -e flag followed by the extension name:

```
npx create-eth@latest -e extension-name
```

For more information about available extensions and how to use them, check out the Extensions section.

#### Option 2: Setup using `git clone`

Clone this repo & install dependencies:

```
git clone https://github.com/scaffold-eth/scaffold-eth-2.git
cd scaffold-eth-2
yarn install
```


---



# hooks/hooks.md

---
sidebar_position: 4
---

## 🛠 Interacting with Your Smart Contracts

Scaffold-ETH 2 provides a collection of custom React hooks designed to simplify interactions with your deployed smart contracts. These hooks are wrappers around Wagmi, an easy-to-use interface with typescript autocompletions for reading from, writing to, and monitoring events emitted by your smart contracts.

To ensure autocompletions function correctly, always update the [`targetNetworks` ](/deploying/deploy-nextjs-app#--targetnetworks) in `scaffold.config.ts` to include the relevant network/chain whenever you deploy your contract using [`yarn deploy --network`](/deploying/deploy-smart-contracts#3-deploy-your-smart-contracts).

:::info
The custom hooks rely on three main files for their functionality and TypeScript autocompletion:

- `packages/nextjs/contracts/deployedContracts.ts`
- [`packages/nextjs/contracts/externalContracts.ts`](/external-contracts)
- `scaffold.config.ts`

The `deployedContracts.ts` file is auto-generated/updated whenever you run `yarn deploy --network`. It organizes contract addresses and abi's based on chainId.

:::

:::note

When having multiple chains configured in [`targetNetworks`](/deploying/deploy-nextjs-app#--targetnetworks), make sure to have same contractName's on other chains as `targetNetworks[0].id`.This ensures proper functionality and autocompletion of custom hooks, as the current setup and types assumes that same contract's are present on other chains as `targetNetworks[0]`.

:::


---



# hooks/useDeployedContractInfo.md

---
sidebar_position: 5
---

## useDeployedContractInfo

Use this hook to fetch details about a deployed smart contract, including the ABI and address.

```ts
const { data: deployedContractData } = useDeployedContractInfo(contractName);
```

This example retrieves the details of the deployed contract with the specified name and stores the details in the `deployedContractData` object.

### Parameters

| Parameter        | Type     | Description           |
| :--------------- | :------- | :-------------------- |
| **contractName** | `string` | Name of the contract. |

#### Return Value

- `data`: Object containing `address` and `abi` of contract.


---



# hooks/useScaffoldContract.md

---
sidebar_position: 6
---

## useScaffoldContract

Use this hook to get your contract instance by providing the contract name. It enables you to interact with your contract methods.
For reading data or sending transactions, it's recommended to use `useScaffoldReadContract` and `useScaffoldWriteContract`.

```ts
const { data: yourContract } = useScaffoldContract({
  contractName: "YourContract",
});
// Returns the greeting and can be called in any function, unlike useScaffoldReadContract
await yourContract?.read.greeting();

// Used to write to a contract and can be called in any function
import { useWalletClient } from "wagmi";

const { data: walletClient } = useWalletClient();
const { data: yourContract } = useScaffoldContract({
  contractName: "YourContract",
  walletClient,
});
const setGreeting = async () => {
  // Call the method in any function
  await yourContract?.write.setGreeting(["the greeting here"]);
};
```

This example uses the `useScaffoldContract` hook to obtain a contract instance for the `YourContract` smart contract.

### Configuration

| Parameter                   | Type                                                               | Description                                                                   |
| :-------------------------- | :----------------------------------------------------------------- | :---------------------------------------------------------------------------- |
| **contractName**            | `string`                                                           | Name of the contract.                                                         |
| **walletClient** (optional) | [`WalletClient`](https://wagmi.sh/react/api/hooks/useWalletClient) | Wallet client must be passed in order to call `write` methods of the contract |

### Return Value

- `data` : Object representing viem's [contract instance](https://viem.sh/docs/contract/getContract.html#return-value). Which can be used to call `read` and `write` of the contract.

- `isLoading` : Boolean indicating if the contract is being loaded.


---



# hooks/useScaffoldEventHistory.md

---
sidebar_position: 4
---

## useScaffoldEventHistory

Use this hook to retrieve historical event logs for your smart contract, providing past activity data, with the option to watch for new events.

```ts
const {
  data: events,
  isLoading: isLoadingEvents,
  error: errorReadingEvents,
} = useScaffoldEventHistory({
  contractName: "YourContract",
  eventName: "GreetingChange",
  fromBlock: 31231n,
  watch: true,
  filters: { greetingSetter: "0x9eB2C4866aAe575bC88d00DE5061d5063a1bb3aF" },
  blockData: true,
  transactionData: true,
  receiptData: true,
});
```

This example retrieves the historical event logs for the `GreetingChange` event of the `YourContract` smart contract, starting from block number 31231 and filtering events where the `greetingSetter` parameter is `0x9eB2C4866aAe575bC88d00DE5061d5063a1bb3aF`.

### Configuration

| Parameter                      | Type      | Description                                                                                                                                                           |
| :----------------------------- | :-------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **contractName**               | `string`  | Name of the contract to read from.                                                                                                                                    |
| **eventName**                  | `string`  | Name of the event to read.                                                                                                                                            |
| **fromBlock**                  | `bigint`  | Block number from which to start reading events.                                                                                                                      |
| **filters** (optional)         | `object`  | Apply filters to the event based on **indexed** parameter names and values `{ [parameterName]: value }`.                                                              |
| **blockData** (optional)       | `boolean` | If set to true it will return the block data for each event (default: false).                                                                                         |
| **transactionData** (optional) | `boolean` | If set to true it will return the transaction data for each event (default: false).                                                                                   |
| **receiptData** (optional)     | `boolean` | If set to true it will return the receipt data for each event (default: false).                                                                                       |
| **watch** (optional)           | `boolean` | If set to true, the events will be refetched every [`pollingInterval`](/deploying/deploy-nextjs-app#--pollinginterval) set at `scaffold.config.ts`. (default: false). |
| **enabled** (optional)         | `boolean` | If set to false, the hook will not fetch any data (default: true).                                                                                                    |

### Return Values

- `data` property of the returned object contains an array of event objects, each containing the event parameters and (optionally) the block, transaction, and receipt data.
- `isLoading` property indicates whether the event logs are currently being fetched.
- `error` property contains any error that occurred during the fetching process (if applicable).


---



# hooks/useScaffoldReadContract.md

---
sidebar_position: 1
---

## useScaffoldReadContract

Use this hook to read public variables and get data from read-only functions of your smart contract.

```ts
const { data: totalCounter } = useScaffoldReadContract({
  contractName: "YourContract",
  functionName: "userGreetingCounter",
  args: ["0xd8da6bf26964af9d7eed9e03e53415d37aa96045"],
});
```

This example retrieves the data returned by the `userGreetingCounter` function of the `YourContract` smart contract.

### Configuration

| Parameter            | Type        | Description                                                                                                         |
| :------------------- | :---------- | :------------------------------------------------------------------------------------------------------------------ |
| **contractName**     | `string`    | Name of the contract to read from.                                                                                  |
| **functionName**     | `string`    | Name of the function to call.                                                                                       |
| **args** (optional)  | `unknown[]` | Array of arguments to pass to the function (if accepts any). Types are inferred from contract's function parameters |
| **watch** (optional) | `boolean`   | Watches and refreshes data on new blocks. (default : `true`)                                                        |

You can also pass other arguments accepted by [useReadContract wagmi hook](https://wagmi.sh/react/api/hooks/useReadContract#parameters).

### Return Values

- The retrieved data is stored in the `data` property of the returned object.
- You can refetch the data by calling the `refetch` function.
- The extended object includes properties inherited from wagmi useReadContract. You can check the [useReadContract return values](https://wagmi.sh/react/api/hooks/useReadContract#return-type) documentation to check the types.


---



# hooks/useScaffoldWatchContractEvent.md

---
sidebar_position: 3
---

## useScaffoldWatchContractEvent

Use this hook to subscribe to events emitted by your smart contract, and receive real-time updates when these events are emitted.

```ts
useScaffoldWatchContractEvent({
  contractName: "YourContract",
  eventName: "GreetingChange",
  // The onLogs function is called whenever a GreetingChange event is emitted by the contract.
  // Parameters emitted by the event can be destructed using the below example
  // for this example: event GreetingChange(address greetingSetter, string newGreeting, bool premium, uint256 value);
  onLogs: logs => {
    logs.map(log => {
      const { greetingSetter, value, premium, newGreeting } = log.args;
      console.log("📡 GreetingChange event", greetingSetter, value, premium, newGreeting);
    });
  },
});
```

This example subscribes to the `GreetingChange` event emitted by the `YourContract` smart contract and logs the parameters from the event to the console when it's emitted.

This hook is a wrapper around wagmi's [useWatchContractEvent](https://wagmi.sh/react/api/hooks/useWatchContractEvent).

:::note
Due to shortcomings of some RPC providers, this hook may or may not fire events always [checkout this discussion](https://github.com/wevm/wagmi/issues/3883) for more details. To update the RPC link checkout [this section](/deploying/deploy-nextjs-app#--alchemyapikey)
:::

### Configuration

| Parameter        | Type       | Description                                                                                                                                                                                                                                                                                                                                                                           |
| :--------------- | :--------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **contractName** | `string`   | Name of the contract to read from.                                                                                                                                                                                                                                                                                                                                                    |
| **eventName**    | `string`   | Name of the event to read.                                                                                                                                                                                                                                                                                                                                                            |
| **onLogs**       | `function` | Callback function to execute when the event is emitted. Accepts an array of `logs` that occurred during the [`pollingInterval`](/deploying/deploy-nextjs-app#--pollinginterval) set at `scaffold.config.ts`. Each array item contains an `args` property, which can be destructured to get the parameters emitted by the event. This function can customized according to your needs. |

:::note

It is recommended to `setState` using [updater function](https://react.dev/reference/react/useState#updating-state-based-on-the-previous-state) in the `onLogs` function to avoid problems due to caching.

:::


---



# hooks/useScaffoldWriteContract.md

---
sidebar_position: 2
---

## useScaffoldWriteContract

Use this hook to send a transaction to your smart contract to write data or perform an action.

```ts
const { writeContractAsync: writeYourContractAsync } = useScaffoldWriteContract("YourContract");
```

The first argument is name of the contract to write to and the second argument is wagmi's `useWriteContract` hook [parameters object](https://wagmi.sh/react/api/hooks/useWriteContract#parameters).

To send the transaction, you can call the `writeContractAsync` function returned by the hook (which we instance as `writeYourContractAsync`). Here's an example usage:

```tsx
 {
    try {
      await writeYourContractAsync({
        functionName: "setGreeting",
        args: ["The value to set"],
        value: parseEther("0.1"),
      });
    } catch (e) {
      console.error("Error setting greeting:", e);
    }
  }}
>
  Set Greeting

```

This example sends a transaction to the `YourContract` smart contract to call the `setGreeting` function with the arguments passed in `args`. The `writeContractAsync` function (`writeYourContractAsync` instance) sends the transaction to the smart contract.

Below is the configuration for `writeContractAsync` function:

### Configuration

| Parameter                          | Type        | Description                                                                                                          |
| :--------------------------------- | :---------- | :------------------------------------------------------------------------------------------------------------------- |
| **functionName**                   | `string`    | Name of the function to call.                                                                                        |
| **args** (optional)                | `unknown[]` | Array of arguments to pass to the function (if accepts any). Types are inferred from contract's function parameters. |
| **value** (optional)               | `bigint`    | Amount of ETH to send with the transaction (for payable functions only).                                             |
| **onBlockConfirmation** (optional) | `function`  | Callback function to execute when the transaction is confirmed.                                                      |
| **blockConfirmations** (optional)  | `number`    | Number of block confirmations to wait for before considering transaction to be confirmed (default : 1).              |

You can also pass other arguments accepted by [writeContractAsync from wagmi](https://wagmi.sh/react/api/hooks/useWriteContract#mutate-async).

### Return Values

- `writeContractAsync` function sends the transaction to the smart contract.
- `isMining` property indicates whether the transaction is currently being mined.
- The extended object includes properties inherited from wagmi useWriteContract. You can check the [useWriteContract return values](https://wagmi.sh/react/api/hooks/useWriteContract#return-type) documentation to check the types.


---



# hooks/useTransactor.md

---
sidebar_position: 7
---

## useTransactor

Use this hook to interact with the chain and give UI feedback on the transaction status.

![Transaction success](/img/transactorSuccess.gif)

Any error will instead show a popup with nice error message.

![Error Example](/img/transactorFail.gif)

```ts
const transactor = useTransactor();
const writeTx = transactor({
  to: "0x97843608a00e2bbc75ab0C1911387E002565DEDE", // address of buidlguidl.eth
  value: 1000000000000000000n,
});
await writeTx();
```

This example tries to send 1 ETH to the address `buidlguidl.eth`, prompting the connected [`WalletClient`](https://wagmi.sh/react/api/hooks/useWalletClient#usewalletclient) for a signature. And in the case of a successful transaction, it will show a popup in the UI with the message: "🎉 Transaction completed successfully!".

You can pass in anything that is a valid parameter to [Viem's `sendTransaction` function](https://viem.sh/docs/actions/wallet/sendTransaction#parameters) to callback function. It also possible to pass it an promise that resolves in with a transaction hash for example promise from [Wagmi's `writeContractAsync` function](https://wagmi.sh/react/api/hooks/useWriteContract#mutate-async).

[Refer to this recipe](/recipes/WriteToContractWriteAsyncButton) for a more detailed example.

### Configuration

#### useTransactor

| Parameter                     | Type                                                       | Description                                                                                                                                                                       |
| :---------------------------- | :--------------------------------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **\_walletClient** (optional) | [`WalletClient`](https://viem.sh/docs/clients/wallet.html) | The wallet client that should sign the transaction. Defaults to the connected wallet client, and is only needed if the transaction is not already sent using `writeContractAsync` |

#### callback function

| Parameter                                    | Type                                                                                                              | Description                                                                                                                                                                                                                                                                                    |
| :------------------------------------------- | :---------------------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **tx**                                       | [`sendTransaction`-parameters](https://viem.sh/docs/actions/wallet/sendTransaction#parameters) or `Promise` | Either valid parameters for [`sendTransaction`-parameters](https://viem.sh/docs/actions/wallet/sendTransaction#parameters) or a promise that resolves with the transaction hash, e.g. [Wagmi's `writeContractAsync` function](https://wagmi.sh/react/api/hooks/useWriteContract#mutate-async). |
| **options** (optional)                       | `object`                                                                                                          | Additional options for the confirmation.                                                                                                                                                                                                                                                       |
| **└─options.blockConfirmations** (optional)  | `number`                                                                                                          | The number of block confirmations to wait for before resolving. Defaults to 1.                                                                                                                                                                                                                 |
| **└─options.onBlockConfirmation** (optional) | `function`                                                                                                        | A callback function that is called once all `blockConfirmations` is reached.                                                                                                                                                                                                                   |

### Return Values

#### useTransactor

- The callback function that is used to inialize the UI feedback flow.

#### callback function

- A promise that resolves with the transaction hash once the transaction is mined.


---

