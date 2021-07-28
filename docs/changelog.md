# Changelog

## [bosagora/agora](https://github.com/bosagora/agora)

### [v0.15.0: Signature fixes, flash fees, better stats & config](https://github.com/bosagora/agora/releases/tag/v0.15.0) <small>_ 2021-07-27</small>

Major improvements since v0.14.0:

- Blocks are not only signed after SCP's EXTERNALIZE, instead of COMMIT;
- `block_interval_sec` is now a parameter of `consensus` instead of `node`;
- Flash: Funding tx fee and closing tx fees are now supported;
- Block stats will now always be generated, even when no block has been generated yet;

### [v0.14.0: Guaranteed block time, integration fixes, many preimages, timer optimizations](https://github.com/bosagora/agora/releases/tag/v0.14.0) <small>_ 2021-07-24</small>

Major improvements since v0.13.0:

- Agora will now produce blocks at the right interval, even if empty;
- The agora_preimages_gauge stats entry has been renamed to agora_preimages_counter;
- Fixed the VoterCard signature scheme to only hash once, not twice;
- Fixed QR admin methods to not escape the returned string;
- Nodes will now generate a large (5M) of pre-images on startup, allowing them to stay validators for longer timer before switching UTXOs;
- Various timers used for recurring tasks have been optimized to only fire when necessary, instead of a fixed regular interval;
- Agora will now longer automatically sign blocks when catching up, to avoid potential double signatgure issues;

### [v0.13.0: Signature adjustment, DoS prevent, Talos & SCP overhaul](https://github.com/bosagora/agora/releases/tag/v0.13.0) <small>_ 2021-07-19</small>

Major improvements since v0.12.0:

- Fixed a bug that allowed validators to sign an extra block before slashing actually happened;
- SCP layer now requires C++17 support;
- Inconsistency between ConsensusParams' ValidatorCycle and the Genesis block's will now error out;
- Fixed a bug which would lead to the Logger throwing when being called from SCP in some rare cases;
- Fixed a bug which would crash the node (abort) if the Logger threw an Exception;
- Libconsensus: The validator set now include the validator's preimage;
- The SCP integration has been overhaul and greatly simplified, removing a lot of dead code;
- Nodes will only start gossipping transactions if they have a validator peer to avoid tx getting stuck;
- Nodes will now always keep connection to validators, regardless of min_peers;
- FullNode API now includes a `handshake` method which replaces `getPublicKey` as handshake method;
- Talos: Correctly show the error message if Agora returns an error;
- Talos: Update the config format to match current format;
- Stoa handlers have been combined in a single module;
- Outgoing requests now support proxy;
- Fixed a bug in the nomination protocol where a vote would change from yes to no when there were nodes to slash;
- Signatures can now only be added for the blocks that have been produced since the last payment;
- The bitfield in the BlockHeader used to record validators have been modified to unambiguously store the length;
- Fixed a DoS vector where a node could crash when asked invalid data;
- SCP now uses the UTXO as node ID instead of public key;
- Stoa: Block headers are now pushed when a new signature is received (block_header_updated handler);
- Fixed a DoS attack where a node would crash when receiving a specifically crafted signature;
- Fixed a DoS attack where a node would crash upon receiving alphanumeric but non-hex characters in large binary values;
- Added Swagger API specification to allow fuzzing the node;
- Added opt-out fuzzing component to the network integration tests;
- Talos: Improved dependency tree to reduce security risks;
- Talos: Fixed vulnerability with `target=blank` links;
- Talos: Improved first screen UX and fixed network address parsing;
- Talos now requires node 16;
- Flash: Add on-chain fees related endpoints to support fees in uncollaborating close attempts;
- Fixed a bug where signature catchup was dependent on the order of the returned items;
- Changed the admin interface methods (`loginQR`, `encryptionKeyQR`) to be GET instead of POST;
- Pre-images are now shared during SCP nomination to reduce the odds of slashing;
- Removed FullNode's `getPreimage` endpoint, obsoleted by `getPreimages`;

### [v0.12.0: Better stats, `TxBuilder` improvements and bugfix, `/validators` endpoint](https://github.com/bosagora/agora/releases/tag/v0.12.0) <small>_ 2021-06-17</small>

Major improvements since v0.11.0:

- The minimum required version of LDC / DUB are now 1.26.0 and 1.25.0, respectively;
- The genesis timestamp can now be configured as `consensus.genesis_timestamp`;
- Configuring `validator.slash_penalty_amount` is no longer supported;
- The stats now include the genesis timestamp;
- `TxBuilder` has been simplified, with multiple parameters of `sign` now being functions;
- Flash: The remaining funds in a funding tx will now be properly credited back;
- Registry payload that fail signature validation will now be more verbose and prominent;
- A bug where the wrong key was used to verify the signature of a registry payload,
  leading to rejecting valid registry payload, has been fixed.
- All endpoints now provide endpoint stats (some were previously missing);
- Nodes now expose `GET /validators[?height=$height]` to get the list of validators at a given height;
- `TxBuilder` now properly sorts the inputs, fixing a bug where it would sign the wrong input;

Along with many internal changes to improve efficiency and reduce the risk of error.

### [v0.11.0: Better Flash notifications, runtime logger configuration, SCP cleanup](https://github.com/bosagora/agora/releases/tag/v0.11.0) <small>_ 2021-06-10</small>

Major changes since v0.10.0:

- Flash: Discovery now includes Channel updates;
- Flash: Channels are now gossipped to new peers;
- Flash: Fixed a possible race condition between state change and notification to listener;
- Quorum balancing: The hash used as seed is now that of the externalized block, instead of the ledger state;
- TxBuilder now correctly orders inputs when creating a transaction;
- The SCP internals have been revamped, leading to lower memory footprint and easier integration;
- `Validator.receiveEnvelope` now longer blocks, it uses a queue for processing envelope asynchronously instead;
- Loggers can now be dynamically reconfigured through an endpoint in the admin interface;
- Serialization now always serialize to little endian regardless of the host;
- Multiple stability improvements / race conditions fixed;

### [v0.10.0: Extra syntax checks on lock script, improved Votera support, HTTPS](https://github.com/bosagora/agora/releases/tag/v0.10.0) <small>_ 2021-06-06</small>

Major changes since v0.9.0:

- Admin interface now use the right pre-image to generate the encryption key for Votera;
- Transaction payload is now a simple array instead of a struct (breaking change for JSON serialization);
- Agora will now perform additional syntaxical validation on the lock script to ensure it is not malformed;
- Votera: Admin interface now include signature and public key with voter card;
- Disabled a new upstream behavior to prevent double destruction of GC-allocated object;
- Better diagnostics will be provided when Agora fails to start for abnormal reasons,
  such as corrupted disk state;
- Logger configuration will now propagate to child logger by default;
- Discovery / registry registration task is now more efficient;
- Support for HTTPS communication has been added;
- Consensus: Validators will now reject blocks with non-monotonic `missing` validators;

### [v0.9.0: Passive slashing, per-output type, better setup and debug experience](https://github.com/bosagora/agora/releases/tag/v0.9.0) <small>_ 2021-06-01</small>

Major changes since v0.8.1:

Pre-images are now used to generate block signatures

- Block signatures are now based on pre-images for the "signature noise" derivation.
This implements one of the aspect of Agora's passive slashing policy,
which is that signing two blocks for the same height reveal a validator's private key.

Transaction type has been moved to Output

- Previously, transactions had a "type" field that would indicate the type of its output:
payment (the default), freeze, or coinbase. This created issues as payment and freeze
needed to be mixed (e.g. to avoid creating a refund transaction that was frozen).
The `type` field is now part of the `Output`, and may be extended in the future.

Multiple Talos (setup interface) bug fixes

- The setup interface had a few issues, where some field would be empty when
run in a particular way, making navigating between menus impossible.
Those issues have been fixed and the interface now works as expected on all devices.

Agora will now dynamically export its symbol

- Agora now use the `export-dynamic` linker option by default, which should result
in proper stack traces on Alpine Linux (and potentially other platforms),
at the cost of slightly bigger binary. Stripping the binary will still work.

### [v0.8.1: Always enable TRACY_ON_DEMAND](https://github.com/bosagora/agora/releases/tag/v0.8.1) <small>_ 2021-05-26</small>

This is an internal fix that might reduce memory usage for some clients.

### [v0.8.0: Random seed correction, sorted transactions, RBF](https://github.com/bosagora/agora/releases/tag/v0.8.0) <small>_ 2021-05-26</small>

Notable changes since last release (v0.7.1):

- Well known keypairs have been updated (this affect users running test networks);
- An intermittent error in UTXODB will no longer be silence, instead the node will properly report it;
- Nodes will now replace transactions in their TxPool if it fulfill certain conditions (e.g. higher fee);
- Random seed calculation was wrong (involved an extra `Hash.init` parameter) and has been fixed;
- Transactions will now sort their inputs and outputs;
- Ledger will now do a full reset if the validator set is empty, regardless of the UTXOSet being non-empty;

### [v0.7.1: Improved logging for nomination](https://github.com/bosagora/agora/releases/tag/v0.7.1) <small>_ 2021-05-20</small>

This release mainly contains enhancements on logging during the nomination phase,
along with a couple internal improvements.

### [v0.7.0: Major SCP upgrade](https://github.com/bosagora/agora/releases/tag/v0.7.0) <small>_ 2021-05-17</small>

Changes since v0.6.1:

- SCP has been upgraded from v11.2.0 (2019-06-26) to v16.0.0 (2021-04-08).

### [v0.6.1: Minor CI fix on tags push](https://github.com/bosagora/agora/releases/tag/v0.6.1) <small>_ 2021-05-14</small>

This release fixes a minor issue that triggered when a tag was pushed.
One of the test would previously fail to run because it expected a different git object.

### [v0.6.0: Absolute PreImage offsets, greatly improved Flash API, transaction fees](https://github.com/bosagora/agora/releases/tag/v0.6.0) <small>_ 2021-05-14</small>

Notable changes since the last release:

- Validator now authenticate themselves upon connecting to one another;
- The random seed algorithm has been changed to be simpler;
- The node hashing algorithm has been changed to be stable at a given height/state;
- Many bugs in the shutdown procedure have been fixed, and things should never hang now;
- The consensus protocol now supports a minimum fee;
- Default development compiler is now LDC 1.26 (LDC 1.25 works for building, but not in unittest mode);
- Windows builds have been disabled due to limitations in the CI memory capacity;
- PreImages now uses absolute index (height) instead of relative index (relative to enrollment);
- The Flash layer now supports managing multiple keys from the same node;
- It is now possible to list flash channels through the API;
- The node now exposes 4 config parameters to control and limit transactions propagation;
- Flash: Settlement is now always published after timeout is reached;
- Talos, the setup interface, is now integrated in Agora and can be started with `--initialize=address_to_bind`;
- The API now allows to get detailes informations about a list of Flash channels;
- The Flash control API can now be configured to bind to a specific address/port;
- Rules for nomination has been improved to take fees into account and better handle time differences;
- Loggers can now be reconfigured dynamically through the admin interface;
- Nodes will now prioritize their own Enrollment instead of waiting to hear back from other nodes;
- DataPayload now uses Base64 for the REST API;
- `DataPayload.data` was renamed to `bytes`;
- SCP is now built with clang++ on all platforms;
- The random seed check no longer mistakenly uses the node state over the block state;

### [v0.5.0: Fixed nomination timer, improved flash API](https://github.com/bosagora/agora/releases/tag/v0.5.0) <small>_ 2021-04-22</small>

- Network discovery period is now configurable (`node.network_discovery_interval_secs`);
- Nomination interval is now configurable (`validator.nomination_interval`, in seconds);
- Nomination interval is now 5s by default, up from 1s; this should improve liveness;
- Flash can now use a registry;
- Flash API now includes `onRequestedChannelOpen` to query if a node will accept a channel open;
- Fixed a race condition preventing envelopes with valid signature to be accepted after externalization;
- Periodic catchup will now longer ask for signatures from slashed nodes;
- Flash: `changeFee` was only implemented in test, moved to production;
- Vanity miner now supports Bech32, and well-known keypairs have been changed accordingly;
- The node will now stop nominating as soon as it starts shutting down;

### [v0.4.1: Minor build script fixes](https://github.com/bosagora/agora/releases/tag/v0.4.1) <small>_ 2021-04-19</small>

Fixes an issue with the build script that led to the version being rendered incorrectly.

### [v0.4.0: Configurable logger, readable SQL databases](https://github.com/bosagora/agora/releases/tag/v0.4.0) <small>_ 2021-04-19</small>

- UTXO set is now stored in `utxo` database, validator set in `validator` table;
- Most tables now use text fields instead of binary ones;
- UTXO's `pubkey_hash` field is now called `pubkey`;
- Nomination protocol now takes into account missing validator pre-images;
- Some log messages have been cleaned up to be less confusing / alarming;
- Loggers can now be configured individually in the config file;

### [v0.3.0: Improved Flash with Wallet API, better catch-up, database restructuring](https://github.com/bosagora/agora/releases/tag/v0.3.0) <small>_ 2021-04-16</small>

- Vibe.d & other libraries have been updated to remove some networking bugs;
- Flash layer documentation and tests have been enhanced;
- Validators will no longer re-enroll at every block during catchup, only the recent ones;
- The Flash layer API has been extended for wallet usage;
- Payment paths now have configurable timeouts and better error reporting;
- Validators will now properly shut down and finalize all objects without error;
- Pre-image member 'enroll_key' has been renamed to 'utxo';
- Node state have been unified in two databases, 'stateDB' and 'cacheDB', instead of multiple scattered ones;
- Logging has been improved, especially w.r.t. block signatures;
- Default and example values for various configuration parameters have been adjusted to be more realistic;
- A block storage corruption preventing nodes from restarting has been fixed;
- Validators will no longer ban validators, even if they are not responding;
- The logic around pre-images has been improved, leading to more tolerance in what is accepted;
- BitBlob has been updated to v2.0.0, removing a DoS vector when using the REST interface;
- Flash retry logic now uses a configurable exponential backoff algorithm instead of simple retry;
- The 'random_seed' member of 'Enrollment' has been renamed to commitment;
- Flash: Channel gossipping has been improved;
- Flash: Channel updates are now sequenced, preventing replays;
- Nodes will no longer query already externalized blocks from nodes when retrying after seeing an invalid block;
- TxBuilder is now available in its own module for client code to use;
- Flash: Onion payload has been simplified and some unused fields have been removed;
- Flash: Error messages are now authenticated (and ignored if not coming from a peer);
- Flash: A channel notification API is now available (e.g. `onChannelNotify`, `monitorBlockchain`...);
- Name registry: Added CLI argument to set verbose mode;
- Flash: Make sure Payee sets enough lock_time;
- Flash: Channel closing has been improved;
- Congress: Voter card's expiry now comes with ISO8601 suffix;
- Agora can now listen to multiple interfaces, not just one, allowing to bind to e.g. different IPs;
- Nodes will now longer fetch all pre-images during catchup, only the latest ones;
- Nodes will no longer nominate data that would slash all validators;

[All commits since v0.2.0](https://github.com/bosagora/agora/compare/v0.2.0...v0.3.0)

### [v0.2.0: Flash layer, slashing, block signatures, Bech32, Schnorr everywhere, and more](https://github.com/bosagora/agora/releases/tag/v0.2.0) <small>_ 2021-03-30</small>

The following is a non-exhaustive list of major changes since last release:

- Agora now stores version information (`agora --version`);
- Transaction Fees and Coinbase have been added;
- Block signatures are now fetched during periodic catchup;
- SCP nomination is now based on hashes of transaction instead of the whole object;
- Nodes that do not reveal pre-images will now get slashed;
- Nodes are now better at enrolling (retry, delays, etc...);
- A beta version of the Flash layer is now available;
- Full nodes now have a simpler REST endpoint to query a single block;
- Block storage has been improved;
- Test networks can now run on less than 6 validators;
- The crypto and serialization code are now the4ir own libraries;
- Periodic catch up has been improved;
- Allow refund outputs of freezing tx to not be frozen if < 40k;
- Nodes will rather crash than slash themselves;
- The minimum required DUB & LDC version is now v1.25.0;
- A basic Tracy integration has been added;
- Agora memory usage can now be profiled at runtime via an instrumented GC;
- All transactions are now signed using Schnorr, Ed25519 is not used anymore;
- Agora now works better with its network registry, reducing the need for manual configuration;
- Blocks will now store a time offset from Genesis instead of an absolute timestamp;
- Key pair will now perform additional safety and validity checks;
- PreImage implementation have been improved;
- An endpoint to validate the config file is now available for the setup interface;
- Onion routing is used in the Flash layer;
- Agora will now store its state in a more readable manner in the DB;
- Flash persistence has been implemented;
- Logger overhead has been reduced;
- Public keys are now encoded using Bech32 rather than Stellar-style format;

[All commits since v0.1.0](https://github.com/bosagora/agora/compare/v0.1.0...v0.2.0)

### [v0.1.0: Pre-slashing alpha version](https://github.com/bosagora/agora/releases/tag/v0.1.0) <small>_ 2021-01-08</small>

This release is the first tagged alpha version of Agora.
Agora has been deployed to a test environment for months now,
however no tag has existed yet.
In order to allow for the development of a more stable versioning
and deployment scheme, a first tag needs to be introduced.
