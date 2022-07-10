# Starknet Name Service contracts

## ABOUT `For any contacts, please message TURBO#6141 on Discord.`
Starknames is the first full-end name service on Starknet! We are live on Testnet and allow users to name and lookup account names. As Starknet has an amazing and emerging gaming/NFT scene, this raises several reasons as to why a name service is even more important here than on L1, and thus, brings along an ecosystem-wide responsibility for creating a sustainable UX environment. 

#### Why a name service? (SUMMARY)
Starknames is important because it simplifies the use of Starknet blockchain addresses.
Imagine being able to easily remove the need for long addresses like `0x000F3b380EA218688Ca19E3b5F0fds0abAA4faDEd5f5C5803a4173b5Ab314fds`, and simplify your account to `hello.stark`! This is the first major step for onboarding new blockchain users. UX.
#### Partnering with projects
How is it possible to create this simplification? 
It's simple. Other Starknet protocols would look up a user's account address through the Starknames registry, which would resolve to the user's existing name. Or vice-versa. Through this ecosystem adoption, there will be no need for netizens to even look at their addresses, the bane for onboarding new users from web2. For example, they could legibly observe their name on a scoreboard and profile on one gaming protocol, or perhaps on another NFT marketplace with the same naming records. 
The jarring issue with Starknet is that there is no sense of interopability in the ecosystem, yet. Starknames will serve as the base layer of account names under the mutual bond that dAPPS are incentivised to integrate it.

Credit must go to ENS for their pioneering work in name services' contracts, and significantly, 42 Labs' initial deployment, although they stopped. Live contracts are based off of those same deployments; currently, Starknames is steadily developing more expansive functionalities for Mainnet. Stay tuned!🤫
### How to use Starknames
As recent focus has been concentrated in UX, the Starknames website is up and running smoothly! Click [here](https://www.google.com/) to register your own name on testnet.
## Usage
### Contract Interfacing
The `contracts/registry/IRegistry.cairo` file contains the Interface spec (`IRegistry`) for the registry contract. To look up, one would call the registry's `get_resolver` or `get_resolver_by_name` functions to retrieve the address of the resolver for that domain.
### Domain resolving
The resolver for a domain might then provide different data for the domains it resolves. To check if a resolver implements a given method, determine the hash for the method you are interested in and call the resolver's `supports_interface` function. A method's hash is the namehash of the primary getter function, without `func`, implicit args or the colon (see `contracts.name.library.hash_name` for a Cairo implementation and `tests.utils.hash_name` for the Python equivalent). The   `supports_interface` function returns `TRUE` (1) if the function is supported, and `FALSE` (0) if not.

Currently, the following resolver methods are supported:
`get_starknet_address(namehash : felt) -> (starknet_address : felt)` with hash `2820744738538176835336224571064374651047813236984662977660834172684259369636`. This method resolves a domain name to a Starknet address. Thus, to check if a given resolver provides starknet addresses for a domain, call `supports_interface(2820744738538176835336224571064374651047813236984662977660834172684259369636)`.

